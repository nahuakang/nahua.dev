---
title: "Go Template: Using Execute vs. ExecuteTemplate"
date: 2020-08-28T21:59:26+02:00
slug: "golang-template-execute-vs-executetemplate"
draft: false
toc: false
images:
tags: [go, golang, web development]
---

Rendering the correct template is an important step in building a web application. If you are new to web programming in Go, chances are you might have come across two methods in the `html/template` package: [`func (*Template) Execute`](https://golang.org/pkg/html/template/#Template.Execute) and [`func (*Template) ExecuteTemplate`](https://golang.org/pkg/html/template/#Template.ExecuteTemplate).

You might have also wondered: What are the differences between these two methods? The quick answer is to look up the official documentation:

- `func (t *Template) Execute(wr io.Writer, data interface{}) error`:
Execute applies a parsed template to the specified data object, writing the output to `wr`.
- `func (t *Template) ExecuteTemplate(wr io.Writer, name string, data interface{}) error`:
ExecuteTemplate applies the template associated with t that has the given name to the specified data object and writes the output to wr.

I don't know about you, but while the Go documentation is well-written, I could not understand the differences, especially what `name string` is. 

So read on to find out how these two methods differ and when to use them. 

## Setup
To answer this question, let's take a look at a simple example. Suppose we have a very mini web app `app` in the following file structure:
```
.
├── layouts
│   └── index.html
└── main.go
```

Inside `index.html` we have a very basic homepage:
```html
<!-- app/layouts/index.html -->
<h1>Welcome to my Go Web App!</h1>
```

## template.Execute

To make this homepage appear on our localhost virtual server, we have to perform the following steps:

1. Create a handler function, e.g. `index`, that would render `index.html`
2. Register this handler `index` to our localhost server via [`http.HandleFunc`](https://golang.org/pkg/net/http/#HandleFunc)
3. Start the server with [`http.ListenAndServe`](https://golang.org/pkg/net/http/#ListenAndServe) and listen on a port for requests

Here's a generic boilerplate for our mini Go app with 1 route:
```go
// app/main.go

package main

import (
	"html/template"
	"net/http"
)

func index(w http.ResponseWriter, r *http.Request) {
	t, err := template.ParseFiles("layouts/index.html")
	if err != nil {
		panic(err)
	}
	t.Execute(w, nil)
}

func main() {
	http.HandleFunc("/", index)
	http.ListenAndServe(":8080", nil)
}
```

Notice that we are parsing one HTML file with [`template.ParseFiles`](https://golang.org/pkg/html/template/#ParseFiles), with the parsed result returned as a `* Template` and assigned to our variable `t`. Because of this, we could immediately execute on the parsed template `t` and send its content as well as data (in this case `nil`, or none) to the `http.ResponseWriter`, which then displays the HTML content when localhost server responds to a request from us on the browser.

Inside your terminal, run the following command in your project's root directory and then type in `localhost:8080` in your browser, you should see this very simple app running:
```console
$ go run main.go
```

## Expanding Our Mini Web App
Imagine your mini web app has gained traction among users and now you want to refactor it so that you can build it in a more scalable manner. You looked around the app carefully and decides that, for each new page you create, you'd want to add a header and a footer. 

What's more, you want a base template `layout.html` that would include the header, the footer, and then render the content of any page based on the request. If a user requests `index.html`, they'll get it with the header and footer attached. If they decide to request a new `contact.html`, they'll get it with the header and footer attached as well.

Our app now looks like this:
```console
.
├── layouts
│   ├── contact.html
│   ├── footer.html
│   ├── header.html
│   ├── index.html
│   └── layout.html
└── main.go

```

So for our current `index.html`, we'd have:

- Layout Template
  - Header Template
  - Content Template (of Index or of Contact)
  - Footer Template

How do we achieve this with HTML? Well, we can't easily, but Go's built-in template language helps us to organize our HTML pages nicely. To define a template is as simple as:
```html
{{ define "templateName"}}
  <!-- HTML code -->
{{ end }}
```

So we could define our basic header and footer templates as:
```html
<!-- app/layouts/header.html -->
{{define "header"}}
<nav>Navbar</nav>
{{end}}
```
```html
<!-- app/layouts/footer.html -->
{{define "footer"}}
<footer>Copyright 2020</footer>
{{end}}
```

And let's move the HTML code in our `index.html` into a template definition as well:
```html
<!-- app/layouts/index.html -->
{{define "content"}}
<h1>Welcome!</h1>
{{end}}
```

To use a template, we simply insert it into a new layout template, but this time using the pattern:
```html
<!-- app/layouts/layout.html -->
{{define "layout"}}

  {{template "header"}}

  {{template "content"}}

  {{template "footer"}}

{{end}}
```

Before we move on, let's create our contact page and modify our index page:
```html
<!-- app/layouts/index.html -->
{{define "content"}}
<h1>Welcome!</h1>
{{end}}
```
```html
<!-- app/layouts/contact.html -->
{{define "content"}}
<h1>Contact Us</h1>
{{end}}
```


## template.ExecuteTemplate
Woah! Have you noticed that now we have a bunch of HTML files using Go's template language syntax? If you re-run `$ go run main.go` in your terminal and visit `localhost:8080`, you won't see anything!

This is because we've wrapped all of our HTML code inside these `define` and `template` blocks and our Go app does not know what to render for the user anymore. If we had just one HTML file that isn't completely wrapped in Go template, we would still be fine using `template.Execute`, but now we must somehow tell our Go app which template to execute.

Inside an HTML file, we could specify the rendering of our header by `{{template "header"}}`. But now our `layout.html`, which would dynamically generate either the content of `index` or `contact`, is itself wrapped in a define statement.

Here's where `template.ExecuteTemplate` comes in. We could parse as many files as we wish and then ask the parsed template to execute a specific template which it has parsed:
```go
t, err := template.ParseFiles(...files)
t.executeTemplate(w, "layout", nil)
```

The new `main.go` looks like this:
```go
// app/main.go
// Ignoring package main and import lines
func index(w http.ResponseWriter, r *http.Request) {
	t, err := template.ParseFiles(
		"layouts/layout.html",
		"layouts/header.html",
		"layouts/index.html",
		"layouts/footer.html",
	)
	if err != nil {
		panic(err)
  }
  // Now we must set the header to "text/html" to render properly
	w.Header().Set("Content-Type", "text/html")
	t.ExecuteTemplate(w, "layout", nil)
}
```

We can do the same for our contact page and update our handler:
```go
func contact(w http.ResponseWriter, r *http.Request) {
	t, err := template.ParseFiles(
		"layouts/layout.html",
		"layouts/header.html",
		"layouts/contact.html",
		"layouts/footer.html",
	)
	if err != nil {
		panic(err)
  }
  // Now we must set the header to "text/html" to render properly
	w.Header().Set("Content-Type", "text/html")
	t.ExecuteTemplate(w, "layout", nil)
}

func main() {
	http.HandleFunc("/", index)
	http.HandleFunc("/contact", contact)
	log.Fatal(http.ListenAndServe(":8080", nil))
}
```

## Refactor (Optional)
The smart and diligent as you are, you can not tolerate duplicated code and want to follow through with the DRY (Don't Repeat Yourself) principle. So let's extract out some elements of the code above to make it cleaner while using `template.ExecuteTemplate`.

First, let's re-organize our HTML files like this:
```
.
├── main.go
└── views
    ├── contact.html
    ├── index.html
    └── layouts
        ├── footer.html
        ├── header.html
        └── layout.html
```

Next, we'll use Go's [filepath.Glob](https://golang.org/pkg/path/filepath/#Glob) to glob all the layout files, `layout`, `header`, and `footer`, as a slice of strings.
```go
// app/main.go
var (
	layoutDir = "views/layouts/"
	fileExt   = ".html"
)

func layoutFiles() []string {
	// Using the pattern "layouts/*.html" to glob all files
	files, err := filepath.Glob(layoutDir + "*" + fileExt)
	if err != nil {
		panic(err)
	}
	fmt.Println(files)
	return files
}
```

Let's also create a new data structure `view` that we'll use to store all necessary information to render our HTML files and give it the `render` method:
```go
// app/main.go
// Declare the pointer to view variables to be used in main()
var homeView *view
var contactView *view

// This is our new data structure to store all information about our views
type view struct {
	Template *template.Template
	Layout   string
}

// This is a method for the receiver type *view
func (v *view) render(w http.ResponseWriter, data interface{}) error {
	return v.Template.ExecuteTemplate(w, v.Layout, data)
}
```

On top of that, we'll create a `newView` function to generate a new view:
```go
// app/main.go

// newView generates a new *view with parsed template and layout type stored
func newView(layout string, files ...string) *view {
	files = append(
		files,
		layoutFiles()...,
	)

	t, err := template.ParseFiles(files...)
	if err != nil {
		panic(err)
	}

	return &view{
		Template: t,
		Layout:   layout,
	}
}
```

Finally, we'll update our handler:

```go
// app/main.go
// A helper function to panic if error occurs when rendering
func must(err error) {
	if err != nil {
		panic(err)
	}
}

// New home handler
func index(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html")
	must(homeView.render(w, nil))
}

// New contact handler
func contact(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html")
	must(contactView.render(w, nil))
}

func main() {
	homeView = newView("layout", "views/index.html")
	contactView = newView("layout", "views/contact.html")

	http.HandleFunc("/", index)
	http.HandleFunc("/contact", contact)

	log.Fatal(http.ListenAndServe(":8080", nil))
}
```

As a final step, maybe we'll extract some of the above-mentioned refactoring into a new file `app/views/view.go`. That's left for the reader to do as a mini-exercise.

## The End
Hopefully by now, you'll see why sometimes we might need to use `template.ExecuteTemplate` instead of `template.Execute`. These two methods are very common and will repeatedly occur in your Go web apps, so play around with the code and take all the time you need to digest the information.

Happy programming in Go!
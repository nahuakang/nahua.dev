# New Blog

Shortly before 2020 came to an end, I decided that I was done with the [Hugo](https://gohugo.io/) template I was using for my personal blog. I did not understand most of the code in the theme, so customizing it was cumbersom. Most importantly, using Hugo felt always like a non-intuitive fight.

I want a simple blog with a clean, simple, and responsive design. I want a blog that is _personal_, meaning I know how it works and I know _every_ line that goes into making the blog.

After a quick look around, I chose [Zola](https://www.getzola.org/), a static site generator written in [Rust](https://www.rust-lang.org/). Zola feels simpler than Hugo with fewer features. But it suits my needs and desires for a personal blog.

On the first day of 2021, this new blog was live.

## Setup

To check out this blog locally, first install Zola:

```
# OS X
$ brew install zola

# Ubuntu
$ snap install --edge zola
```

Then, download the repository and get into the directory:

```
# SSH version
$ git clone git@github.com:nahuakang/zola-blog.git

# HTTP version
$ git clone https://github.com/nahuakang/zola-blog.git

$ cd zola-blog
```

Once inside the directory, do:

```
$ zola build && zola serve
```

Enjoy.

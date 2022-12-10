+++
title = "[Open Source] Code Walk-Through: Write a Rust Clippy Lint"
date = 2022-12-10
draft = false

slug = "open-source-walk-through-with-rust-clippy"
aliases = [
    "blog/open-source-walk-through-with-rust-clippy/"
]

[extra]
lang = "en"
toc = true
+++

In this blog post, I'll walk you through a Rust Clippy lint and teach you how to write [Clippy lints][clippy_lints].

<!-- more -->

I have been contributing to [Rust Clippy][rust_clippy] on and off for more than 1 year now. A while ago, I discussed with two Clippy core team members about [updating the Clippy documentation][update_clippy_docs] so that we focus on the [`LateLintPass`][LateLintPass], which is more often developed in Clippy than [`EarlyLintPass`][EarlyLintPass].

While the progress on updating the documentation is slow, I've written an example on how to write a lint with `LateLintPass`. So I have decided to publish this tutorial on writing Clippy lint and hope that more Rustaceans might contribute to Clippy.

**Note:** This lint is actually implemented in Clippy. If you are curious, feel free to check out the actual implementation of this lint example here: [trim_split_whitespace].

## Short Intro of Clippy

If a reader is not familiar with Clippy yet, it is a collection of lints that catches common mistakes in your Rust code and gives you suggestions on writing more idiomatically.

### Clippy Usage

To use Clippy, simply run the following in your project and Clippy will examine all your code to see if any snippets can be improved:

```sh
$ rustup update
$ rustup component add clippy
$ cargo clippy  # display lint suggestions only
$ cargo clippy --fix  # display and apply lint suggestions
```

For more information, feel free to check Clippy's [README][rust_clippy].

## Overview of Clippy Lint Development Process

Generally speaking, we can follow a checklist to develop Clippy lints:

1. Define the Lint
    - Name the Lint
    - Choose a Lint Group
    - Choose `EarlyLintPass` or `LateLintPass`
    - Generate Lint Files
2. Write Clippy UI Tests
    - Choose a scope for the lint
    - Cover edge cases
3. Implement the Lint Logic
    - Choose a `EarlyLintPass/LateLintPass` method to implement
    - Choose a way to emit the lint suggestions
4. Improve UI Tests
    - Iteratively check the lint progress by running UI tests
5. Write/Update Lint Documentation

### A Brief Explanation on `LateLintPass` vs. `EarlyLintPass`

Since we have already encountered some technical terms, let's explain them briefly without getting bogged down by technicalities.

The Rust compiler first parses the source code into Abstract Syntax tree (AST) before passing it into High Level Intermediate Representation (HIR). `EarlyLintPass` is for linting in the AST stage and `LateLintPass` is for linting in the HIR stage. 

**Note**: If you wonder what AST or HIR is in the context of `rustc`, feel free to read [_Rustc Overview_] as well as [_High-Level Intermediate Representation (HIR)_] for a quick review.

`EarlyLintPass` is for Clippy lints that only deal with the grammar (on the AST level) while `LateLintPass` contains type information and should be used for Clippy lints that must have access to such information.

Take a look at the following code:

```rust
let x = OurUndefinedType;
x.non_existing_method();
```

From the Rust AST perspective, both lines are "gramatically" correct. The assignment uses a `let` and ends with a semicolon. The invocation of a method looks fine, too. If we only want to check that these 2 lines of code are gramatically correct, we can use `EarlyLintPass` when writing a lint.

However, we might raise a few questions about these 2 lines of code. For instance, is the `OurUndefinedType` defined or undefined? Does this type implement the `non_existing_method` method? If these questions concern us, we must use `LateLintPass` when writing a lint.

## An Example for Lint: Unnecessary Whitespace Trimming

Have you met a cautious Rustacean who are obsessed with leading and trailing whitespaces in their `String`/`str` that they would perform [trim]/[trim_start]/[trim_end] before [split_whitespace]:

```rust
" A B C ".trim().split_whitespace();
```

Hey, it is okay to be extra careful. But as it turns out, `split_whitespace` would already ignore leading and trailing whitespaces. So our careful Rustacean could have written instead the following code (go to this [playground] for an example):

```rust
" A B C ".split_whitespace();
```

This presents a perfect opportunity for a lint that could inform other cautious Rustaceans that they only need to perform one method call if that call is `split_whitespace`.

## Define the Lint

Let us name our lint `trim_split_whitespace`, which is an accurate description of the unnecessary method call.

### Diagnostic Items

Thinking about the problem at hand, it seems that we need to somehow ascertain that a Rustacean's code is sequentially calling the `trim`/`trim_start`/`trim_end` and `split_whitespace` methods defined for the [primitive type `str`][str_primitive_type].

Very importantly, we only want the lint to be triggered if `trim`/`trim_start`/`trim_end` and `split_whitespace` methods that are defined for `str` are invoked. So if we have a custom type that implements methods with the same names, the lint will not falsely trigger because we simply don't know how these custom `trim`/`trim_start`/`trim_end`/`split_whitespace` methods are defined and should instead ignore them.

To do so, we need access to [diagnostic items][diagnostic_items], which are specific types, traits, and functions that are manually added into the Rust language. Diagnostic items are our way to check for specific types, traits and, in our present case, functions/methods.

Conveniently, in `rustc_span` there is a [symbol list][sym_list] that documents all the symbols for Rust's diagnostic items. For instance, `split_whitespace` is defined as the symbol `str_split_whitespace`.

When Clippy parses the expressions in a code base, it will give us an [expression struct][rustc_hir_expr] which contains an `hir_id` that we can turn into a [`DefId`][DefId]. We could then check if that expression's `DefId` corresponds to a symbol associated with a Rust diagnostic item.

If we run into an expression containing custom `trim`/`trim_start`/`trim_end`/`split_whitespace` methods, then their `DefId` will not match the diagnostic items's symbols because these custom methods are not registered as Rust language's diagnostic items.

If all of this sounds confusing, it's okay. Keep reading the blog. We will go into the code, which will make everything clearer. Also, refer to the documentation links, which can be helpful.

**Note:** Take a quick look at [Using Diagnostic Items][using_diagnostic_items] if you want to have an overview of how they work.

### Chossing `LateLintPass`

Because we need access to diagnostic items, we are going to use [LateLintPass] for implementing this new lint.

Looking at `LateLintPass`'s documentation, we see many trait methods defined for this trait, such as `check_fn`, which can be used if we only care about standalone invocation of functions, or `check_stmt`, which examines any statement in the code. For Clippy, `check_expr` is likely the most commonly implemented method.

Additionally, since this `trim_split_whitespace` lint will examine chained method calls, it is quite convenient to implement the [check_expr] method for `LateLintPass` when working on this new lint. This is because chained method calls are treated as expressions in Rust and `LateLintPass::check_expr` will examine these expressions in any code that is given to Clippy.

### Choosing a Lint Category

Since this lint is more related to writing idiomatic Rust, we can consider putting it in the `clippy::style` category. In the [README][rust_clippy] you will find a list of Clippy categories, such as `correctness`, `pedantic`, etc.

### Generate New Lint Files with `LateLintPass`

Once you have cloned `rust-clippy` repository to your local environment and checked out a new git branch, we can run `cargo dev new_lint` command to generate some files:

```sh
$ git checkout -b new_lint_trim_split_whitespace

$ cargo dev new_lint --name=trim_split_whitespace --pass=late --category=style
    Finished dev [unoptimized + debuginfo] target(s) in 0.07s
     Running `target/debug/clippy_dev new_lint --name=trim_split_whitespace --pass=late --category=style`
Generated lint file: `clippy_lints/src/trim_split_whitespace.rs`
Generated test file: `tests/ui/trim_split_whitespace.rs`
```

Examine the changes with `git status` carefully, we see that most of the important files have been created by the command so that we can focus on developing the new lint:

```sh
$ git status
On branch new_lint_trim_split_whitespace

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   CHANGELOG.md
	modified:   clippy_lints/src/lib.register_all.rs
	modified:   clippy_lints/src/lib.register_lints.rs
	modified:   clippy_lints/src/lib.register_style.rs
	modified:   clippy_lints/src/lib.rs
	modified:   src/docs.rs

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	clippy_lints/src/trim_split_whitespace.rs
	src/docs/trim_split_whitespace.txt
	tests/ui/trim_split_whitespace.rs

no changes added to commit (use "git add" and/or "git commit -a")
```

Feel free to experiment with the command and check what the `cargo dev new_lint` command did for us. Most importantly, it has done quite a bit of heavy-lifting and we have a `clippy_lints/src/trim_split_whitespace.rs` file to implement the lint logic as well as a `tests/ui/trim_split_whitespace.rs` file to implement the UI tests in.

## Understand HIR with `#[clippy::dump]`

Before we move further with our UI test cases as well as the lint implementation, it is important to note that it is helpful to first understand the internal representation that rustc uses. Clippy has the `#[clippy::dump]` attribute that prints the [_High-Level Intermediate Representation (HIR)_] of the item, statement, or expression that the attribute is attached to.

To attach the attribute to expressions you often need to enable `#![feature(stmt_expr_attributes)]`.

[Here][print_hir_example] you can find an example. To see how an expression like `" A ".trim().split_whitespace()` looks like in HIR, select _TOOLS_ from the upper right corner of Rust Playground and click _Clippy_.

Overall, you should see a structure that resembles the following:

```rust
Expr {
    hir_id: HirId { // fields },
    kind: MethodCall(
        PathSegment {
            ident: split_whitespace#0,
            hir_id: HirId { // fields },
            // fields
        },
        Expr {
            hir_id: HirId { // fields },
            kind: MethodCall(
                PathSegment {
                    ident: trim#0,
                    hir_id: HirId { // fields },
                    // fields
                },
                Expr {
                    hir_id: HirId { // fields },
                    kind: Lit(
                        Spanned {
                            node: Str(
                                " A ",
                                Cooked,
                            ),
                            span: src/main.rs:5:13: 5:18 (#0),
                        },
                    ),
                    span: src/main.rs:5:13: 5:18 (#0),
                },
                [],
                src/main.rs:5:19: 5:25 (#0),
            ),
            span: src/main.rs:5:13: 5:25 (#0),
        },
        [],
        src/main.rs:5:26: 5:44 (#0),
    ),
    span: src/main.rs:5:13: 5:44 (#0),
}
```

It might take some getting used to but, if we observe carefully, we see that there are 2 [MethodCall]s, one for `split_whitespace`, where the `PathSegment.ident` is `split_whitespace#0`, and one for `trim`,
where the `PathSegment.ident` is `trim#0`. We might also notice an expression `Expr` whose `kind` is [Lit] with a `Spanned { node: Str(" A "), ..}`.

In essence, when an expression has chained method calls like:

```rust
" A ".trim().split_whitespace()
```

Its HIR representation would look like the following, with the last method `split_whitespace` being the most outer element, the method `trim` being the second most outer element, and the method call receiver `" A "` being the most inner element.

```rust
// Note that this is an extremely simplified pseudo-HIR structure
Expr {
    kind: MethodCall(
        split_whitespace,             // This is the last method call
        Expr {
            kind: MethodCall(
                trim,                 // This is the first method call
                Expr {
                    kind: Lit(" A ")  // This is the receiver of the first method call
                }
            )
        }
    )
}
```

Let us keep this information in our head as we move on to the next steps in writing a new Clippy lint.

## Write UI Tests

With some knowledge of the kind of expression we are working with, let us write down some cases which we expect the lint to warn. The following could be a reasonable starting point for us:

```rust
// tests/ui/trim_split_whitespace.rs

#![warn(clippy::trim_split_whitespace)]

fn main() {
    // &str
    let _ = " A B C ".trim().split_whitespace(); // should trigger lint
    let _ = " A B C ".trim_start().split_whitespace(); // should trigger lint
    let _ = " A B C ".trim_end().split_whitespace(); // should trigger lint

    // String
    let _ = (" A B C ").to_string().trim().split_whitespace(); // should trigger lint
    let _ = (" A B C ").to_string().trim_start().split_whitespace(); // should trigger lint
    let _ = (" A B C ").to_string().trim_end().split_whitespace(); // should trigger lint

}
```

### Edge Cases for UI Tests

## Implement Lint Logic

We have decided to implement [check_expr] for `LateLintPass` when implementing this lint. Imagine that we examine an expression `expr` for a line of code such as `" A ".trim().split_whitespace()`, we can check for the usage of `trim` and `split_whitespace` like the following:

```rust
use clippy_utils::diagnostics::span_lint_and_sugg;
use rustc_errors::Applicability;
use rustc_hir::{Expr, ExprKind};
use rustc_lint::{LateContext, LateLintPass};
use rustc_span::sym;

impl<'tcx> LateLintPass<'tcx> for TrimSplitWhitespaces {
    fn check_expr(&mut self, cx: &LateContext<'tcx>, expr: &Expr<'_>) {
        if let ExprKind::MethodCall(path, [split_recv], split_ws_span) = expr.kind
            && path.ident.name == sym!(split_whitespace)
            && let ExprKind::MethodCall(path, [_trim_recv], trim_span) = split_recv.kind
            && let trim_fn_name @ ("trim" | "trim_start" | "trim_end") = path.ident.name.as_str()
            && let Some(trim_def_id) = tyckres.type_dependent_def_id(split_recv.hir_id) {
                span_lint_and_sugg(
                    cx,
                    TRIM_SPLIT_WHITESPACES,
                    trim_span.with_hi(split_ws_span.lo()),
                    &format!("found call to `str::{}` before `str::split_whitespace`", trim_fn_name),
                    &format!("remove `{}()`", trim_fn_name),
                    String::new(),
                    Applicability::MachineApplicable,
                );
        }
    }
}
```

**Note**: We rely heavily on pattern matching in developing Clippy lints. Make sure you read up on [Expr] and [ExprKind] to understand the code snippet above.

Let us dissect this code block quickly.

[check_expr]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_lint/trait.LateLintPass.html#method.check_expr
[clippy_lints]: https://rust-lang.github.io/rust-clippy/master/
[diagnostic_items]: https://rustc-dev-guide.rust-lang.org/diagnostics/diagnostic-items.html
[DefId]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_span/def_id/struct.DefId.html
[EarlyLintPass]: https://doc.rust-lang.org/nightly/nightly-rustc/rustc_lint/trait.EarlyLintPass.html
[Expr]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_hir/hir/struct.Expr.html
[ExprKind]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_hir/hir/enum.ExprKind.html
[_Rustc Overview_]: https://rustc-dev-guide.rust-lang.org/overview.html
[_High-Level Intermediate Representation (HIR)_]: https://rustc-dev-guide.rust-lang.org/hir.html
[LateLintPass]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_lint/trait.LateLintPass.html
[Lit]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_hir/hir/enum.ExprKind.html#variant.Lit
[MethodCall]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_hir/hir/enum.ExprKind.html#variant.MethodCall
[playground]: https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=62c07194aada06aecb7c600123fd5786
[print_hir_example]: https://play.rust-lang.org/?version=nightly&mode=debug&edition=2021&gist=a32d1fa3bfc35607db75e226e5fe475b
[rustc_hir_expr]: https://doc.rust-lang.org/beta/nightly-rustc/rustc_hir/struct.Expr.html
[rust_clippy]: https://github.com/rust-lang/rust-clippy
[split_whitespace]: https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace
[str_primitive_type]: https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace
[sym_list]: https://doc.rust-lang.org/beta/nightly-rustc/rustc_span/symbol/sym/index.html
[type_dependent_def_id]: https://doc.rust-lang.org/stable/nightly-rustc/rustc_middle/ty/context/struct.TypeckResults.html#method.type_dependent_def_id
[trim]: https://doc.rust-lang.org/std/primitive.str.html#method.trim
[trim_end]: https://doc.rust-lang.org/std/primitive.str.html#method.trim_end
[trim_start]: https://doc.rust-lang.org/std/primitive.str.html#method.trim_start
[trim_split_whitespace]: https://github.com/rust-lang/rust-clippy/blob/9a6eca5f852830cb5e9a520f79ce02e6aae9a1b1/clippy_lints/src/strings.rs#L464-L517
[update_clippy_docs]: https://github.com/rust-lang/rust-clippy/issues/9311
[using_diagnostic_items]: https://rustc-dev-guide.rust-lang.org/diagnostics/diagnostic-items.html#using-diagnostic-items

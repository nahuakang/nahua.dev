+++
title = "Open Source Walk-Through with Rust & SeaORM"
date = 2022-05-28
draft = false

slug = "open-source-walk-through-with-rust-seaorm"

[taxonomies]
categories = ["Tech"]
tags = ["programming", "opensource", "rust", "sql"]

[extra]
lang = "en"
toc = true
show_comment = true
math = false
mermaid = false
cc_license = true
outdate_warn = true
outdate_warn_days = 365
+++

In this blog post, I'll walk you through an open source PR I submitted to SeaORM with Rust.

<!-- more -->

This is a transparent and honest story that serves as a walk-through of my first open source issue after a long break from the open source world. The aim of this blog post is to demystify the process of contributing to open source projects and help the readers realize that open source contribution is (often) challenging but rewarding and fun.

While I use a contribution to Rust’s [`SeaORM`](https://github.com/SeaQL/sea-orm) as an example, you do not need any knowledge in Rust to follow this post’s thought process and procedure to take away lessons that might help you start your open source journey in any language or ecosystem.

If you like this post or have questions, feel free to share the post and interact with [my Twitter handle](https://twitter.com/nahuakang).

Alrighty, hop on the wagon and let us begin this story!

## Tl;dr

I know many of you won’t have the time or patience to read my blah blah, so here’s the main take-aways for contributing to open source projects:

1. Pick a project that not only relates to your work or hobby but is also beginner-friendly with maintainers who are willing to offer mentorship and guidance.
2. Pick an issue that’s beginner-friendly, well-scoped (size small to medium) to make sure you can understand the issue at hand without being overwhelmed.
3. Communicate with the maintainers actively about the issue and possible solutions so that they are onboard with your ideas, vice versa. This way, you save both the maintainers’s and your time when it comes to code review.
4. If you ran into a wall, never hesitate to ask the maintainers for help with detailed, well-formulated questions. If one doesn’t answer, ask another. Maintainers are usually helpful and friendly humans.
5. Don’t forget to be polite, communicative, and helpful to others in the open source community 🫶

## Motivation to write about open source contribution

As software engineers, we are often advised to contribute to open source projects as a way to hone our reading and writing skills as well as to give back to the community. However, many new programmers, including myself, tend to feel very intimidated by open source codebases that might appear foreign, abstract, or overwhelming.

Because of this, I decided to create this blog post (and maybe more future posts) to show other open source enthusiasts my process as well as my inner dialogue when working on open source contributions.

To make the post more readable and less fragmented, I presented the entire story in more or less a linear storyline. Please keep in mind that the reality is much more complex, complicated, and iterative. There is usually a lot more struggles going into a first contribution to an unfamiliar project, but it is all worth the effort.

## Pick a beginner-friendly project

I was trying out Rust Tokio’s [axum](https://github.com/tokio-rs/axum/) web framework for building APIs when I encountered a mild issue: ***I am not particularly good at raw SQL***.

In my previous job, I worked mostly in [Django](https://www.djangoproject.com/) (with a little bit of Go), which has an amazing ORM that spoiled me. I am certainly happy and willing to hone my SQL skills, but I also wondered if there was a decent ORM framework in Rust.

By chance, I landed on the homepage of [SeaQL](https://github.com/SeaQL), the project behind the Rust crate [SeaORM](https://github.com/SeaQL/sea-orm), an async, dynamic, and testable ORM that supports Postgres, MySQL, and SQLite at the time this blog post was written. It seems like a project with a lot of care from its creators, so I decided to see if there’s an opportunity for doing some open source contribution.

It’s good to iterate on an important point in open source contribution: ***Choose a project that matters to us!*** Working on a codebase means that we must play with the code ourselves. If the project does not relate to our work or hobby, then we’d be reluctant to play with the code or to test the code we write for the project. I’m a backend engineer and I interact with databases all the time, so an ORM for Rust seems meaningful to me and I’d love to play with SeaORM.

## Choose a beginner-friendly issue

The first thing I did was skimming through the [open issues](https://github.com/SeaQL/sea-orm/issues) of SeaORM. Luckily, SeaORM’s maintainers are very active and it was easy for me to spot a [`good first issue`](https://github.com/SeaQL/sea-orm/issues/661): **Add flag to `sea-orm-cli` to generate code for `time` crate #661.**

Keep in mind that some projects aren’t actively labelling `good first issue` issues and some maintainers don’t have the time or capacity to mentor or guide new contributors.

I personally avoid those projects because I didn’t see myself as very good at navigating on foreign terrain in a codebase due to having programmed professionally for only 2 years. With more years of experience, we’d become better at this.

## Understand the issue

Back to the story. As the issuer suggested in [the link](https://github.com/SeaQL/sea-orm/issues/661): Since the `time` crate is supported as alternative to `chrono`, it should be possible to generate code for `time` crate.

For those who don’t know enough about Rust, there are 2 crates in Rust that deal with time and date, [`time`](https://crates.io/crates/time) and [`chrono`](https://crates.io/crates/chrono) (*note that a `crate` is the equivalent of a `gem` in Ruby or `package` in Python and Javascript*).

The problem at hand seems to be that `sea-orm-cli`, the command line tool for `SeaORM`, appeared to generate only code that corresponds to `chrono`'s `datetime` types and some users would like to have a feature in the command line tool to generate `time`'s `datetime` types without having to write custom code themselves.

## Define questions for solving the issue

Having had very little experience writing `CLI` tools in Rust (or any language for that matter), I laid down some bullet points that I needed clarification in order to work on this issue:

1. Where in the codebase is the `chrono`'s `datetime` types being generated?
2. How do I use `sea-orm-cli` to reproduce the reported issue so that I can progressively iterate towards a solution?
3. What kind of a flag would the maintainers be happy to accept for the finished feature?

## Find the relevant code for the issue at hand

I posted [the first question](https://github.com/SeaQL/sea-orm/issues/661#issuecomment-1118845064) to the issue’s thread:

> I'm looking for a `good first issue` :) Just wondering how one is generating code for `chrono` right now?

Billy, one of the maintainers, was quick to reply [an answer](https://github.com/SeaQL/sea-orm/issues/661#issuecomment-1119393055):

> Hey **[@nahuakang](https://github.com/nahuakang)**, welcome! You can take a look at:

```rust
// sea-orm/sea-orm-codegen/src/entity/column.rs
// https://github.com/SeaQL/sea-orm/blob/86e7e808b37179315a1cc5c6c852764830c04661/sea-orm-codegen/src/entity/column.rs#L47-L51
 
 ColumnType::Date => "Date".to_owned(), 
 ColumnType::Time(_) => "Time".to_owned(), 
 ColumnType::DateTime(_) => "DateTime".to_owned(), 
 ColumnType::Timestamp(_) => "DateTimeUtc".to_owned(), 
 ColumnType::TimestampWithTimeZone(_) => "DateTimeWithTimeZone".to_owned(),
```

Okay, at least now I have some code that I can read. I felt some adrenaline kicking into my system now that I got the first thread of code to investigate. But my dearest enemy, ***imposter syndrome***, also kicked in.

I started questioning myself and wondered if I’d be able to actually come up with a solution? After all, some `good first issue` issues aren’t that easy. What if I can’t solve it and embarrass myself? Because of this, I ***procrastinated***.

## Communicate with maintainers before coding

As a seasoned procrastinator, I waited for a day before I posted [the next two questions](https://github.com/SeaQL/sea-orm/issues/661#issuecomment-1120210927):

> **[@billy1624](https://github.com/billy1624)** Thanks! I'm reading the docs as well as trying to understand the workflow with `sea-orm` now. Are there any examples/tests that demonstrate how to use `sea-orm-cli` to generate code for entities involving `chrono`? I haven't seen a `chrono`
 flag in `sea-orm-cli` so I wonder if the solution here is to add a flag for `time` crate or something else (like handling `time` types)?
> 

Luckily, it was the weekend so it took Billy a few days [to respond](https://github.com/SeaQL/sea-orm/issues/661#issuecomment-1121839813), by which time I had calmed down from my imposter anxiety:

> Hey **[@nahuakang](https://github.com/nahuakang)**, you can simply create a database table with timestamp / datetime columns. Then, follow the steps on [https://www.sea-ql.org/SeaORM/docs/generate-entity/sea-orm-cli](https://www.sea-ql.org/SeaORM/docs/generate-entity/sea-orm-cli), to generate entity files with `sea-orm-cli`.
> We don't have a `chrono` flag for `sea-orm-cli`, since it's the default crate to represent datetime crate as of now. I think we can add an option, `--date-time-crate`, to `sea-orm-cli generate entity`. It will take values such as `chrono` / `time` with `chrono` being the default. This way it's backward compatible and users can opt-in to it.
> Thoughts?

Okay, so the flag for this option should be `--date-time-crate` and we should run the new feature like:

```rust
# To use the time crate for the command
$ sea-orm-cli generate entity --date-time-crate=time -u postgres://nahua:password@localhost:5432/timetest -o src/entity

# To use the chrono crate for the command
$ sea-orm-cli generate entity --date-time-crate=chrono -u postgres://nahua:password@localhost:5432/timetest -o src/entity
```

This is good. So I claimed this issue and began working towards a solution in a format that I knew the maintainers would be willing to accept.

## Familiarize ourselves with the documentation

Quick pause to clarify some important details before jumping into the solution section.

During this entire time as I communicated with Billy, I was actively reading [SeaORM’s documentation](https://www.sea-ql.org/SeaORM/docs). It’s a new ORM and it does things differently from what I did in the Python world.

The most important bits I learned from the documentation that helped me solve the issue were:

1. [`Entity`](https://www.sea-ql.org/SeaORM/docs/generate-entity/entity-structure): The representation of a table in SeaORM. In the [column types section](https://www.sea-ql.org/SeaORM/docs/generate-entity/entity-structure#column-type), I found out about how the `time` and `chrono` Rust `datetime` types correspond to SeaORM’s types.
2. [`sea-orm-cli`](https://www.sea-ql.org/SeaORM/docs/generate-entity/sea-orm-cli): I learned how to use the `CLI` tool that I was now supposed to fix.

## Reproduce the issue

To reproduce the existing issue, I needed to do a few things:

1. A minimal Rust cargo project to generate the `entities` in
2. A running database of my choice that `SeaORM` can connect to (Postgres)
3. Generate a table full of date & time types
4. Run the command to confirm the issue
5. Investigate the code more to understand where I could add the feature to solve the issue

### 1. Create a minimal cargo project

This is really easy in Rust. I simply ran the following command:

```bash
$ cargo new playground
$ cd playground
$ tree
.
├── Cargo.toml
├── README.md
└── src
    └── main.rs
```

Since I know I’ll be only generating entity files (in any directory of my choice) to observe whether `sea-orm-cli` could generate code that has the correct types for `chrono` or `time` given the user’s choice, this barebone project would suffice without any extra boilerplate code.

I installed the latest distribution of `sea-orm-cli` with the following command:

```bash
$ cargo install sea-orm-cli
```

### 2. Spin up a Postgres DB

I have Postgres installed on my Macbook, but I really like using Docker for spinning up a garbage DB that I can test in, so I copy-pasted a very simple `docker-compose` file that I use a lot for job interviews:

```Dockerfile
version: "3.3"
services:
  db:
    image: postgres:latest
    container_name: postgres
    restart: always
    ports:
      - 5432:5432
    environment:
      - POSTGRES_USER=nahua
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=timetest
    volumes:
      - timetest:/var/lib/postgres/data
  
  adminer:
    image: adminer:latest
    restart: always
    ports:
      - 8080:8080

volumes:
  timetest:
```

This is not a tutorial on Docker so the gist is that with this `docker-compose` file, I can spin up a `postgres` database by simply running the following command:

```bash
# Using -d flag for detach mode
$ docker compose up -d
```

The database would have a user `nahua` with a password `password` as well as a DB named `timetest` that’s listening on the port 5432. To examine the database easily, I could login onto `adminer` on [`localhost:8080`](http://localhost:8080).

### 3. Create a test DB table

With the DB spinning, I procrastinated again because I dreaded writing raw SQL commands, not knowing exactly which types I should write.

About a day later, I overcame my inertia and logged in to the database to create the following test table that was filled with some relevant date & time types:

```bash
# Access the running database as the user "nahua" for the DB "timetest"
# Then run SQL command to create a table called "time_tests"
$ docker exec -it postgres /usr/bin/psql -U nahua -d timetest
psql (14.2 (Debian 14.2-1.pgdg110+1))
Type "help" for help.

timetest=# CREATE TABLE time_tests (
  id SERIAL NOT NULL PRIMARY KEY,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  created_date DATE NOT NULL DEFAULT NOW(),
  created_time TIME NOT NULL DEFAULT NOW()
);
timetest=# \q
```

### 4. Reproduce the issue for sanity check

I ran the following commands per specification of the documentation and confirmed that I had everything set up properly for testing my code later on:

```bash
$ sea-orm-cli generate entity -u postgres://nahua:password@localhost:5432/timetest -o .
```

In essence, `sea-orm-cli` would connect to the DB table I spun up and fetch the schema of the `time_tests` table and translate it into Rust code, i.e. `entities` files in my barebone project’s `src/` directory.

This would generate the following files:

```bash
$ tree
.
├── Cargo.toml
├── mod.rs
├── prelude.rs
├── seaql_migrations.rs
├── src
│   └── main.rs
└── time_tests.rs
```

And `time_tests.rs` is the file of interest here:

```bash
$ cat time_tests.rs
//! SeaORM Entity. Generated by sea-orm-codegen 0.8.0

use sea_orm::entity::prelude::*;

#[derive(Clone, Debug, PartialEq, DeriveEntityModel)]
#[sea_orm(table_name = "time_tests")]
pub struct Model {
    #[sea_orm(primary_key)]
    pub id: i32,
    pub created_at: DateTimeWithTimeZone,
    pub created_date: Date,
    pub created_time: Time,
}

#[derive(Copy, Clone, Debug, EnumIter)]
pub enum Relation {}

impl RelationTrait for Relation {
    fn def(&self) -> RelationDef {
        panic!("No RelationDef")
    }
}

impl ActiveModelBehavior for ActiveModel {}
```

When I’m done with my feature, I’d be able to specify a `--date-time-crate` flag with a value so that the values in the `time_tests` model would be the following for `chrono` crate:

```rust
pub id: i32,
pub created_at: DateTimeWithTimeZone,
pub created_date: Date,
pub created_time: Time,
```

and the following for `time` crate:

```rust
pub id: i32,
pub created_at: TimeDateTimeWithTimeZone,
pub created_date: TimeDate,
pub created_time: TimeTime,
```

This information was gathered from the documentation for [column types](https://www.sea-ql.org/SeaORM/docs/generate-entity/entity-structure#column-type).

## Work towards a feature

Now I started investigating the code snippet Billy gave me more carefully. A few things I kept in mind were:

1. How the `sea-orm-cli` code works and how I could insert a new flag `--date-time-crate`?
2. Once the user could specify `--date-time-crate` value, how do I pass this information down to the part of [the code that Billy shared](https://github.com/SeaQL/sea-orm/blob/86e7e808b37179315a1cc5c6c852764830c04661/sea-orm-codegen/src/entity/column.rs#L47-L51), i.e. into the `Column.get_rs_type` method that was in charge of converting `chrono` types or `time` types and translate it into Rust types for the output files we had above?
3. Which other functions or objects are using `Column.get_rs_type` because I must adjust these functions as part of the clean-up after implementing the new feature?

### 1. The Structure of SeaORM project

As the [`Cargo.toml`](https://github.com/SeaQL/sea-orm/blob/master/Cargo.toml) suggests, `sea-orm` has the following workspaces:

```toml
[workspace]
members = [".", "sea-orm-macros", "sea-orm-codegen"]
```

Examining the structure, we can see that `sea-orm-cli` is sort of a stand-alone project living inside `sea-orm` and `sea-orm-codegen` is the workspace that contains the [`Column.get_rs_type`](https://github.com/SeaQL/sea-orm/blob/86e7e808b37179315a1cc5c6c852764830c04661/sea-orm-codegen/src/entity/column.rs#L47-L51) method that Billy originated pointed me to.

```bash
$ pwd
/path/to/our/seaql/sea-orm

$ tree -L 1
...
├── Cargo.toml
...
├── sea-orm-cli
├── sea-orm-codegen
...
├── src
...
└── tests
```

This means that my feature would almost exclusively reside in `sea-orm-cli/` and `sea-orm-codegen/` directories.

### 2. Adding a new CLI flag

By examining the file [`sea-orm/sea-orm-cli/src/cli.rs`](https://github.com/SeaQL/sea-orm/blob/6f4f3a76effc4633cfe5aeb91d164bae819da9b6/sea-orm-cli/src/cli.rs), I quickly familiarized myself with how the project uses `clap` to generate CLI commands and flags and wrote a new flag for `--date-time-crate` (click for [a Github view](https://github.com/SeaQL/sea-orm/pull/724/files#diff-a07d755f2f721c1b06b1c33b45a507b6c55cc99746e69b036ac7b08788aaac98)):

```rust
// sea-orm-cli/src/cli.rs

pub fn build_cli() -> App<'static, 'static> {
    ...
    ).arg(
        Arg::with_name("DATE_TIME_CRATE")
            .long("date-time-crate")
            .help("The datetime crate to use for generating entities.")
            .takes_value(true)
            .possible_values(&["chrono", "time"])
            .default_value("chrono")
    ),
...
}
```

### 3. Refactor; add a context struct and date time crate enum

I also traced the usage of `Column.get_rs_type` all the way back to [`sea-orm/sea-orm-cli/src/commands.rs`](https://github.com/SeaQL/sea-orm/blob/9d2cae44b3612b6fdc3dee7d030ae43916150e6d/sea-orm-cli/src/commands.rs#L155-L156) where the following lines would generate the entities:

```rust
// sea-orm-cli/src/commands.rs

pub async fn run_generate_command(matches: &ArgMatches<'_>) -> Result<(), Box<dyn Error>> {
    ...
    let output = EntityTransformer::transform(table_stmts)?
        .generate(expanded_format, WithSerde::from_str(with_serde).unwrap());
    ...
}
```

So I somehow needed to pass the user’s `date-time-crate` choice into `EntityWriter.generate` method so that `Column.get_rs_type` would eventually pick up this data and act accordingly. Essentially, I needed some sort of a context struct for this job.

I talked with Billy about this and he pointed me to [his comment](https://github.com/SeaQL/sea-orm/pull/680#discussion_r860780963) on another standing PR:

> Hey **[@negezor](https://github.com/negezor)**, thanks for the updates! I think the semantic isn't seems right. The transformer, `EntityTransformer::transform(table_stmts, name_resolver)`, don't need name resolver. Instead, we could have introduce a new struct called `EntityWriterContext` which contains three things...
> 

```rust
pub struct EntityWriterContext {
    pub(crate) expanded_format: bool,
    pub(crate) with_serde: WithSerde,
    pub(crate) name_resolver: NameResolver,
}
```

> Then, `EntityWriter::generate` method would take an `EntityWriterContext`. Thoughts?
> 

This was very helpful! So I wrote the following struct with a `new` method that specified the variables needed by `EntityWriter.generate` to generate the entities:

```rust
// sea-orm-codegen/src/entity/writer.rs

#[derive(Debug)]
pub struct EntityWriterContext {
    pub(crate) expanded_format: bool,
    pub(crate) with_serde: WithSerde,
    pub(crate) date_time_crate: DateTimeCrate,
}

impl EntityWriterContext {
    pub fn new(
        expanded_format: bool,
        with_serde: WithSerde,
        date_time_crate: DateTimeCrate,
    ) -> Self {
        Self {
            expanded_format,
            with_serde,
            date_time_crate,
        }
    }
}
```

Meanwhile, let’s also work out a `DateTimeCrate` enum so that we could store information about which crate the user chooses:

```rust
// sea-orm-codegen/src/entity/writer.rs

#[derive(Debug)]
pub enum DateTimeCrate {
    Chrono,
    Time,
}

impl FromStr for DateTimeCrate {
    type Err = crate::Error;

    fn from_str(s: &str) -> Result<Self, Self::Err> {
        Ok(match s {
            "chrono" => Self::Chrono,
            "time" => Self::Time,
            v => {
                return Err(crate::Error::TransformError(format!(
                    "Unsupported enum variant '{}'",
                    v
                )))
            }
        })
    }
}
```

These changes are all [available here](https://github.com/SeaQL/sea-orm/pull/724/files#diff-d81f32c93a7a9410aefd84070a18ef2ebfd49391151444fad1a752158b6384c7) on Github.

With the `EntityWriterContext` struct and the `DateTimeCrate` enum ready, I could basically write the following in `sea-orm-cli` to let the command pass the `--date-time-crate` information to the code that generates the entities files:

```rust
// sea-orm-cli/src/commands.rs

pub async fn run_generate_command(matches: &ArgMatches<'_>) -> Result<(), Box<dyn Error>> {
    ...
    let date_time_crate = args.value_of("DATE_TIME_CRATE").unwrap();
    ...
    let writer_context = EntityWriterContext::new(
        expanded_format,
        WithSerde::from_str(with_serde).unwrap(),
        DateTimeCrate::from_str(date_time_crate).unwrap(),
    );
    let output = EntityTransformer::transform(table_stmts)?.generate(&writer_context);
}
```

### 4. Sew the thread

Now that we’ve introduced an `EntityWriterContext`, we must update all the methods that would be affected by it until we’ve reached `Column.get_rs_type` method. This part was quite mechanical and rather easy and the changes can be found [here](https://github.com/SeaQL/sea-orm/pull/724/files#diff-cf7963a581865b246e6f94d87d21770aeb273df05aa79d1c060decd82b15c3fc) and [here](https://github.com/SeaQL/sea-orm/pull/724/files#diff-d81f32c93a7a9410aefd84070a18ef2ebfd49391151444fad1a752158b6384c7), mostly in the `sea-orm-codegen/src/entity/base_entity.rs` file and `sea-orm-codegen/src/entity/writer.rs` file.

### 5. Translate different crate types into correct column types

Finally, we have arrived at the beginning of this story when Billy showed me the original code that should be impacted by this feature change:

```rust
// sea-orm-codegen/src/entity/column.rs

pub fn get_rs_type(&self) -> TokenStream {
    ...
    #[allow(unreachable_patterns)]
    let ident: TokenStream = match &self.col_type {
        ColumnType::Char(_)
        ...
        ColumnType::Float(_) => "f32".to_owned(),
        ColumnType::Double(_) => "f64".to_owned(),
        ColumnType::Json | ColumnType::JsonBinary => "Json".to_owned(),
        ColumnType::Date => "Date".to_owned(),
        ColumnType::Time(_) => "Time".to_owned(),
        ColumnType::DateTime(_) => "DateTime".to_owned(),
        ColumnType::Timestamp(_) => "DateTimeUtc".to_owned(),
        ColumnType::TimestampWithTimeZone(_) => "DateTimeWithTimeZone".to_owned(),
    ...
}
```

I decided to just do some nested match expressions to translate the types properly given the variable `date_time_crate` that we’ve passed down from the command line via the `EntityWriterContext` struct:

```rust
// sea-orm-codegen/src/entity/column.rs

pub fn get_rs_type(&self, date_time_crate: &DateTimeCrate) -> TokenStream {
    ...
    #[allow(unreachable_patterns)]
    let ident: TokenStream = match &self.col_type {
        ColumnType::Char(_)
        ...
        ColumnType::Float(_) => "f32".to_owned(),
        ColumnType::Double(_) => "f64".to_owned(),
        ColumnType::Json | ColumnType::JsonBinary => "Json".to_owned(),
        ColumnType::Date => match date_time_crate {
            DateTimeCrate::Chrono => "Date".to_owned(),
            DateTimeCrate::Time => "TimeDate".to_owned(),
        },
        ColumnType::Time(_) => match date_time_crate {
            DateTimeCrate::Chrono => "Time".to_owned(),
            DateTimeCrate::Time => "TimeTime".to_owned(),
        },
        ColumnType::DateTime(_) => match date_time_crate {
            DateTimeCrate::Chrono => "DateTime".to_owned(),
            DateTimeCrate::Time => "TimeDateTime".to_owned(),
        },
        ColumnType::Timestamp(_) => match date_time_crate {
            DateTimeCrate::Chrono => "DateTimeUtc".to_owned(),
            // ColumnType::Timpestamp(_) => time::PrimitiveDateTime: https://docs.rs/sqlx/0.3.5/sqlx/postgres/types/index.html#time
            DateTimeCrate::Time => "TimeDateTime".to_owned(),
        },
        ColumnType::TimestampWithTimeZone(_) => match date_time_crate {
            DateTimeCrate::Chrono => "DateTimeWithTimeZone".to_owned(),
            DateTimeCrate::Time => "TimeDateTimeWithTimeZone".to_owned(),
        },
    ...
}
```

Changes can be viewed on Github [here](https://github.com/SeaQL/sea-orm/pull/724/files#diff-63bc9c1369063e383c3fd1ab5fa18f670946c43dccf172c8919c01028b340993).

### 6. Test the code and try it out

Before finishing up, I wrote [some unit tests](https://github.com/SeaQL/sea-orm/blob/6f4f3a76effc4633cfe5aeb91d164bae819da9b6/sea-orm-codegen/src/entity/column.rs#L344-L384) for distinguishing `time` from `chrono` types in the `Column.get_rs_type` method.

Now, since everything is ready, we should test the end product. Let’s install `sea-orm-cli` from our updated local source code by running:

```bash
$ pwd
/path/to/our/seaql/sea-orm/sea-orm-cli

# This installs `sea-orm-cli` from our local source code
$ cargo install --path .
```

Finally, I ran the `sea-orm-cli` command in my barebone project to see if I could generate the correct entity files with the correct types given `chrono` or `time` crate specification:

```bash
$ sea-orm-cli generate entity --date-time-crate time -u postgres://nahua:password@localhost:5432/timetest -o .

$ cat time_tests.rs
//! SeaORM Entity. Generated by sea-orm-codegen 0.8.0

use sea_orm::entity::prelude::*;

#[derive(Clone, Debug, PartialEq, DeriveEntityModel)]
#[sea_orm(table_name = "time_tests")]
pub struct Model {
    #[sea_orm(primary_key)]
    pub id: i32,
    pub created_at: TimeDateTimeWithTimeZone,
    pub created_date: TimeDate,
    pub created_time: TimeTime,
}

#[derive(Copy, Clone, Debug, EnumIter)]
pub enum Relation {}

impl RelationTrait for Relation {
    fn def(&self) -> RelationDef {
        panic!("No RelationDef")
    }
}

impl ActiveModelBehavior for ActiveModel {}
```

Awesome. So I wrote up [a PR](https://github.com/SeaQL/sea-orm/pull/724) for this issue. Let’s wait and see what the code reviewers say 😉

## Final words

Congratulations! You’ve gone through my long and winding blah blah. I hope you’ve learned something from my walk-through and, perhaps, you’ve realized that open source contribution does not need to be that intimidating!

I want to give the good people at [SeaQL](https://github.com/SeaQL) a quick shout-out and tell the world that they’re awesome for doing open source works! If you can, please sponsor them so that they can continue doing open source works and mentor new contributors.

In the near future, I hope to write a few more walk-throughs for different projects so as to provide you with a wide range of examples on open source contribution.

Remember, you are well-equipped both mentally and skill-wise to contribute to open source. Take your time, don’t get anxious, and enjoy the process!
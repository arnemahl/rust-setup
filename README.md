# Rust project setup for a good Developer Experience

I wanted a setup that made it as easy to work with Rust as it is to work with frontend development using npm, webpack and eslint. Here's a few utilities I put together to achieve that.

### What do each of these uitilities do for you?

1. Rust itself comes with a compiler and a package manager named _Cargo_ (think npm). Cargo lets you easily install Rust packages by running `cargo install &lt;package>` in the terminal. If you want a full intro to the basics of Rust, check the [Getting Started](https://doc.rust-lang.org/book/getting-started.html) page.
1. [Racer](https://github.com/phildawes/racer#racer---code-completion-for-rust) provides code completion and should be hooked into your editor.
1. [cargo-watch](https://github.com/passcod/cargo-watch#-cargo-watch) lets you watch your project for changes so that you don't have to manually trigger a build to see if you code compiles every time you save a document.
1. [rustfmt](https://github.com/rust-lang-nursery/rustfmt#rustfmt--) helps you format Rust code according to style guidelines (think eslint), and you can either hook it into your editor or run it in the terminal.
1. [dybuk](https://github.com/Ticki/dybuk) makes the terminal output nicer when compiling Rust. Unfortunately, though, it doesn't work together with rustfmt, so you can't use both at the same time.

### How to install

1. [Install Rust](https://www.rust-lang.org/en-US/downloads.html)
    * Add a [Rust plugin](https://forge.rust-lang.org/ides.html) to your editor/IDE.
    * Add `~/.cargo/bin` to your $PATH ― when you install packages with `cargo install`, this is where the packages end up (at least on unix systems). If you don't add this directory to your $PATH, rustfmt, Racer and any other cargo packages will not be found.
1. [Install Racer](https://github.com/phildawes/#installation) with `cargo install racer` (may take a few minutes).
    * Also be sure to [configure Racer](https://github.com/phildawes/racer#configuration) or else it won't work (I suggest getting Rust sources by cloning the [github repo](https://github.com/rust-lang/rust)).
    * Add a [Racer plugin](https://github.com/phildawes/racer#editorsides-supported) to your editor/IDE.
    * PS: If you see a bunch of temporary files with garbled names showing up when editing a Rust file, simply resarting the editor/IDE might fix it. If not, [take a look at this](https://github.com/defuz/RustAutoComplete/issues/19).
1. [Install cargo-watch](https://github.com/passcod/cargo-watch#install) with `cargo install cargo-watch` (may take a few minutes).
1. [Install rustfmt](https://github.com/rust-lang-nursery/rustfmt#installation) with `cargo install rustfmt` (may take a few minutes).
1. Install [dybuk](https://github.com/Ticki/dybuk):
    1. cd to where you want to keep the dybuk repo
    1. Run `git cone https://github.com/ticki/dybuk.git`
    1. Run `cargo install --path dybuk`

### How to use

1. Having installed Rust you can run `cargo build` to build your project and `cargo run` to build and run it.
1. With Racer and editor/IDE plugin installed, you should get code completion in your editor. Open [src/main.rs](src/main.rs) in your editor and type in `hello::`, and you should get a suggestion to use the function `hello::print_hello()` if it is set up correctly.
1. [Use cargo watch](https://github.com/passcod/cargo-watch#usage) by running `cargo watch` in your project directory to watch for changes. While `cargo watch` is running, make a change in one of the `src/` files and save, and you should see it update it's output.
1. [Use rustfmt](https://github.com/rust-lang-nursery/rustfmt#running) by running `cargo fmt`. You can also use rustfmt with cargo-watch by running `cargo watch [test] fmt`. Note that if you want to configure rustfmt's write mode when using `cargo watch` you must do so in a `rustftm.toml` file, as the --write-mode flag would then be interpreted by rust-watch instead of rustfmt. In this project there [rustftm.toml](rustftm.toml) sets the write mode to `diff` instead the default `replace`.
1. Use [dybuk](https://github.com/Ticki/dybuk) by appending `|& dybuk` when building or watching, respectively: `cargo build |& dybuk` or `cargo watch |& dybuk`. Unfortunately it doesn't work with `cargo watch test fmt` because dybuk ignores the output of fmt.

If you want to use both rustfmt and dybuk, there's a few ways you can do that:

- Have to terminals for running `cargo watch |& dybuk` and `cargo watch fmt`. Then you get prettyfied build output in one and rustfmt output in the other.
- Run `cargo watch |& dybuk` while developing. Then run `cargo fmt --watch-mode=replace`. (`--watch-mode=replace` is the default, so you only need to add it if you want to override the setting from `rustfmt.toml`). Personally I'd `git add -A` all the changes first so I can `git diff` to see what changes rustfmt is making.

### That's it

Now you're ready to start hacking! Check out the [Rust guessing game tutorial](https://doc.rust-lang.org/book/guessing-game.html) if you need some inspiration, or go straight to the [Syntax and Semantics](https://doc.rust-lang.org/book/syntax-and-semantics.html).

If you have any feedback og suggestions for how to get a better (or maybe just different?) setup, let me know.

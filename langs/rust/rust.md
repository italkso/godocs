

# Rust

## Install Rust Using rustup

````shell
# Install rustup
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Test if install rustup successfully
$ rustc -V
$ rustc --version

# View offline docs
$ rustup doc

# Update
$ rust update

# Uninstall Rust
$ rustup self uninstall
````

In the Rust development environment, all tools are installed to the      `~/.cargo/bin`     directory, and this is where you will find the Rust toolchain,  including `rustc`, `cargo`, and `rustup`.



## Hello World

````bash
mkdir ~/projects
cd ~/projects
mkdir helloWorld
cd helloWorld
````

````rust
fn main() {
    println!(Hello, world!);
}//main.rs
````

````bash
$ rustc main.rs
$ ./main
````



## Cargo

| Command                   | Description                                                  |
| ------------------------- | ------------------------------------------------------------ |
| `$ cargo --version`       | Check the version of Rust and Cargo                          |
| `$ cargo new hello_cargo` | Create a project named hello_cargo with Cargo                |
| `$ cargo build`           | Build the project (Dependencies will be intsalled, `Cargo.lock` will be created) |
| `$ cargo run`             | Run the project                                              |
| `$ cargo test`            | Test the project                                             |
| `$ cargo doc`             | Create a document for project                                |
| `$ cargo publish`         | Publish the project to [crates.io](https://crates.io/)       |

Use the command`rustup docs —book` to get the offline version of book [The Rust Programming Language](https://doc.rust-lang.org/book/#the-rust-programming-language).

````shell
$ cargo new hello-rust
$ cargo run
````

| File          | Description          |
| ------------- | -------------------- |
| `Cargo.toml`  | Configuration file   |
| `src/main.rs` | Write your code here |

[TOML](https://toml.io/en/) is data format. Here’s the content in `Cargo.toml`.

````shell
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

[dependencies]
ferris = "0.2.0"
````

Use dependency in `main.rs`.

````rust
use ferris_says::say; 				// from the previous step
use std::io::{stdout, BufWriter};

fn main() {
    let stdout = stdout();
    let message = String::from("Hello fellow Rustaceans!");
    let width = message.chars().count();

    let mut writer = BufWriter::new(stdout.lock());
    say(message.as_bytes(), width, &mut writer).unwrap();
}
````



***Reference***

- <https://www.rust-lang.org/>
-  <https://www.rust-lang.org/zh-CN/learn/get-started>

- <https://doc.rust-lang.org/book/title-page.html>

-  <https://crates.io/>


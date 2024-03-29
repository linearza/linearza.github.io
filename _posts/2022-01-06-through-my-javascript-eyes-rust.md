---
layout: post
title:  "Through Javascript Eyes: Rust"
description: "My notes on learning Rust as an experienced javascript developer"
date:   2022-01-06 10:28:00
categories: rust javascript learning
---

Its been a minute since I've attempted to blog something, gosh! I've decided to embark on a journey of exploring some new languages and frameworks, starting with Rust. If time allows this will be the first of many such posts. This post will be updated as I progress, keeping all my notes in one place.

Primarily my goal is to explore a few backend frameworks such as [Rocket][rocket], and brush up my experience with a few old familiars such as Ruby on Rails, Phoenix and so on.

I am specifically approaching this from the perspective of a javascript engineer so my notes will be rooted in that context and from that perspective. For the purpose of this exercise, I am following the official [Rust docs][rust-lang].

Anyway, enough waffling, these posts will be in short form and will simply contain notes on things that I find interesting or confusing as I undertake this learning journey. Here we go...

## Rust
#### Notes

* Compiled app runs in all supported environments, without requiring interpreter/compiler setup first, unllike pyhon, ruby etc.
* Variables are immutable by default in Rust, as opposed to js
* Rust also has References, similar to prototypal inheritance in js, but they are also immutable by default.
* `cargo docs --open` generates and opens offline docs for all used crates. This is pretty amazing!
* The chaining and imports in Rust I'm finding a bit confusing, but as noted much of this requires knowledge of the imported library.
* Rust allows for 'shadowing' variables, where you basically redefine a variable which was previously defined. This is a bit weird, but I guess somewhat like extending classes on a micro level.
* Similar to javascript variables are defined with `let` and constants with `const` though constants require a type always being set
* Methods can have deeply nested inner scopes `(){... {... {...}}}`  as opposed to javascript which only has contextual scope with hoisting
* Main difference between shadowing and mutable variable is that a mutated variables cannot change type, but shadowing allows it
 

[rocket]: https://rocket.rs/
[rust-lang]: https://doc.rust-lang.org/stable/book/


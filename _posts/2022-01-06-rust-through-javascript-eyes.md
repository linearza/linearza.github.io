---
layout: post
title:  "Rust through javascript eyes"
description: "My notes on learning Rust as an experienced javascript developer"
date:   2022-01-06 10:28:00
categories: rust javascript learning
---

Its been a minute since I've attempted to blog something, but I thought this might be worthwhile sharing.

I decided to expand my development repertoire but exploring new languages and frameworks. Primarily my goal is to explore a few backend frameworks such as [Rocket][rocket], and brush up my experience with others such as Ruby on Rails and Phoenix.

I am approaching this from the perspective of a, primarily, javascript engineer so my notes will be rooted in that context. For the purpose of this exercise, I am exploring the official [Rust docs][rust-lang].

Anyway, enough waffling, these posts will be in short form and will simply contain notes on things that I find interesting or confusing as I undertake this learning journey. Here we go...

#### Notes

* Compiled app runs in all supported environments, without requiring interpreter/compiler setup first, unllike pyhon, ruby etc.
* Variables are immutable by default in Rust, as opposed to js
* Rust also has References, similar to prototypal inheritance in js, but they are also immutable by default.
* `cargo docs --open` generates and opens offline docs for all used crates. This is pretty amazing!
* The chaining and imports in Rust I'm finding a bit confusing, but as noted much of this requires knowledge of the imported library.
* Rust allows for 'shadowing' variables, where you basically redefine a variable which was previously defined. This is a bit weird, but I guess somewhat like extending classes on a micro level.



[rocket]: https://rocket.rs/
[rust-lang]: https://doc.rust-lang.org/stable/book/


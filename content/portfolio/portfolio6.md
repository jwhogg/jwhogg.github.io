---
title: 'why-rs: A Causal Inference Library in Rust'
date: "2025-12-07"
draft: false
# math: true
# katex: true
---

[Github🔗](https://github.com/jwhogg/why-rs)

An under-development project, where I'm trying to build out a Causal Inference library in Rust. I found there wasn't much in the way of CI libraries in Rust, and
I was underwhelemed with the level of support for the ones I've used in Python, so I decided to try and build my own, which I hope to make use of throughout
my PhD and extend to suit my purposes.

So far, I've implemented basic data structures for DAGs and FCMs, and the ability to define custom functions, and sample from a model. I plan next to develop a
simple PC implementation for Causal Discovery.

In terms of roadmap, I'll be adding things when I need them, but I hope to build a performant foundation that can be used by Python bindings, expecially with the
ability to support very large graphs (as far as I'm aware, other libraries can't do this too well).
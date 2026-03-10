+++
title = "Parallel ANF"
date = 2026-03-10
description = "A description of an ANF-like intermediate representation that is better suited for parallel evaluation"

[taxonomies]
tags = ["Compilers", "Programming Languages"]
+++

## Standard ANF

ANF is an expression-based language form used in intermediate representation of programs. It is a good choice for functional programming language compilers, because it allows functions to be represented as expression trees while still describing the evaluation order of computations like static single assignment. However, the encoded evaluation order does not necessarily describe data dependencies. A simple example is function `f` shown below that takes parameters `a`, `b`, `c`, and 
`d` and returns `(a + b)(c + d)`

```
function f(a, b, c, d)
	let x = a + b in
	let y = c + d in
	let result = x * y in
	result
```

## Binding Blocks

paragraph

```
function f(a, b, c, d)
	let x = a + b, y = c + d in
	let result = x * y in
	result
```

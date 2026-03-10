+++
title = "Parallel ANF"
date = 2026-03-10
description = "A description of an ANF-like intermediate representation that is better suited for parallel evaluation"

[taxonomies]
tags = ["Compilers", "Programming Languages"]
+++

## Standard ANF

ANF is an expression-based language form used in intermediate representation of programs. It is a good choice for functional programming language compilers, because it allows functions to be represented as expression trees while still describing the evaluation order of computations through sequenced bindings. However, the encoded evaluation order does not necessarily describe data dependencies. A simple example is function `f` shown below that takes parameters `a`, `b`, `c`, and 
`d` and returns `(a + b) ⋅ (c + d)`.

```
function f(a, b, c, d)
	let x = a + b in
	let y = c + d in
	let result = x ⋅ y in
	result
```

Variable `x` is first bound to the sum of `a` and `b`, and then variable `y` is bound to the sum of `c` and `d`. Despite `y` not being dependent on `x`, it is still represented as a separate evaluation step in the binding chain.

## Binding Blocks

In many programs, multiple computations do not depend on each other and could be evaluated concurrently on a parallel processor. Pure functions (functions that do not have side effects) may be evaluated in any order while preserving determinism. Standard ANF represents non-dependent computations as separate steps in the expression tree, which can obscure opportunities for concurrent evaluation.

A solution for this is to modify ANF to use "binding blocks", which represent groups of independent computations. The bindings in a block may be evaluated in any order, or potentially at the same time, because none of them may reference each other.

```
function f(a, b, c, d)
	let x = a + b, y = c + d in
	let result = x ⋅ y in
	result
```

This example demonstrates how binding blocks can be used to rewrite function `f` in a way that indicates to a compiler or runtime that both additions can be done out of order or at the same time before being used as factors in the multiplication.

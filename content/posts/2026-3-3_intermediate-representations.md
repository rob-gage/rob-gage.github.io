+++
title = "Intermediate Representations"
date = 2026-03-03
description = "A description of three common intermediate representation forms used in compilers"

[taxonomies]
tags = ["Programming Languages"]
+++

## Compiler Intermediate Representations

Modern programming language compilers usually do not generate code from or do optimizations on the syntax structure produced by parsing the language. They usually first validate it and translate it to a intermediate representation (IR), a more simple structure that can be manipulated and optimized by the compiler, and eventually translated into the compiler's target language.

To demonstrate three common IR forms, we will use the following Rust function as an example, which takes an integer and returns `true` if it is greater than or equal to `0`, otherwise returning `false`.

```rust
fn is_not_negative(integer: i64) -> bool {
	if integer >= 0 { true } else { false }
}
```

## Static Single Assignment

Static single assignment ([SSA](https://en.wikipedia.org/wiki/Static_single-assignment_form)) is an IR form that allows variables to be assigned only once. SSA is very explicit about control flow and data dependencies, which makes it ideal for imperative languages.

```
function is_not_negative(integer)
	entry_block:
		comparison := integer >= 0
		branch comparison, then_block, else_block
	then_block:
		then_result := true
		goto merge
	else_block:
		else_result := false
		goto merge
	merge:
		result := φ(then_result, else_result)
		return result
```

Note: `φ` denotes a phi-node, a construct that selects a value associated with the branch taken to reach the current block.

## Continuation Passing Style

In continuation passing style ([CPS](https://en.wikipedia.org/wiki/Continuation-passing_style)), functions take the function that consumes their result as a parameter. CPS eliminates the need for phi-nodes and expresses control flow via continuations, which is convenient for functional programming languages. Every function call being a tail call allows the compiler or runtime to reuse stack frames.

```
function is_not_negative(integer, continuation)
	entry_block:
		comparison := integer >= 0
		branch comparison, then_block, else_block
	then_block:
		call continuation(true)
	else_block:
		call continuation(false)
```

## A-normal Form

A-normal form ([ANF](https://en.wikipedia.org/wiki/A-normal_form)) is based on expressions, unlike SSA and CPS, which are based on control flow. ANF functions only take as parameters values that represent constants or variables that have already been bound. As a result, ANF preserves the structure of expression-based functions, but still encodes evaluation order like SSA.

```
function is_not_negative(integer)
	let comparison = integer >= 0 in
	let result = if comparison then true else false in
	result
```

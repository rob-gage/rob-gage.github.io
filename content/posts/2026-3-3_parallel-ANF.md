+++
title = "Parallel ANF"
date = 2026-03-03
description = "A description of an ANF-like normal form modified for parallelism"

[taxonomies]
tags = ["Programming Languages"]
+++

## Compiler Intermediate Representations

Modern programming language compilers usually do not generate code from or do optimizations on the syntax structure produced by parsing the language. They usually first validate it and translate it to a intermediate representation (IR), a more simple structure that can be manipulated and optimized by the compiler, and eventually translated into the compiler's target language. Static single assignment ([SSA](https://example.com)) is an IR form that allows variables to be assigned only once. In continuation passing style ([CPS](https://example.com)), functions take the function that consumes their result as a parameter. Functions in A-normal form ([ANF](https://example.com)) only take as parameters values that represent constants or the results of previously evaluated functions.

# Standard A-normal Form

```
<Expression> :=
		let <Variable> = ... in <Expression>
		return <Value>
		
<Value> :=
		<Variable>
		<Constant>
```

Standard ANF encodes evaluation order of computations by requiring that functions only take previously defined values as parameters. Sequenced computations are denoted by nested `<Binding>` expressions.

The example below represents a function body that does the following:
+ Defines lambda `f` that squares a number
+ Applies `f` to each number in a list and defines `a` as the result
+ Defines lambda `g` that takes a number and creates a lambda that returns the sum of its parameter and that number
+ Applies `g` to an accumulator initially set to `0` and the next number in `a` until there are no more numbers in `a` to be summed and defines `b` as the result
+ Returns `b`

```
let f = ꟛx. x * x
let a = map f [2, 3, 4, 5, 6] 
let g = ꟛx. ꟛy. x + y
let b = fold g 0 a
return b
```

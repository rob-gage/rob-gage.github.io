+++
title = "Symbolic Differentiation & Computer Algebra Systems"
date = 2025-12-08
description = "About symbolic differentiation and computer algebra systems"

[taxonomies]
tags = ["Mathematics"]
+++

## Symbolic Differentiation

Symbolic differentiation is the process of transforming the algebraic syntax tree of a function into a syntax tree for it's derivative function. A function implementing derivative rules can be recursively applied to a syntax tree to transform it into an accurate, but often unnecessarily complex derivative function. The result must be reduced into simplest form with another set of rules.

## Computer Algebra Systems

A computer algebra system (CAS) is a general purpose tool for working with algebraic expressions. They are often used to graph functions, or manipulate equations to isolate variables. They typically implement reduction rules for algebraic syntax structures that perform a reasonable number of simplifications on the structure.

## Canonicalization of Algebraic Expressions

Complete canonicalization of algebraic expressions is not always possible. This is a consequence of the equality of algebraic expressions being computationally undecidable (see [Richardson's Theorem](https://en.wikipedia.org/wiki/Richardson's_theorem)). Mature CASes implement very many simplification rules to be able to reduce most potential expressions, but there will always exist an expression that a CAS cannot fully simplify.

## My Differentiation Engine

I am working on a differentiation engine that can correctly differentiate multivariable functions,
and graph single variable functions and their derivatives. It is still a prototype, and implementing a sufficient set of simplification rules still needs to be done.

Try it: [Differentiation Engine](https://calculus.dogwood.cloud)

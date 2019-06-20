# Lambda Calculus
Def. a mathematical logic for expressing computation based on fucntion abstraction and application.
Formula. 
Think lambda calculus as function:
```javascript
λ x. t => def f (x) { t }
```
## Syntax for a term
1. Variable --- `x`
    - A character or string representing a parameter or mathematical/logical value.
2. Abstraction --- `λ x. t`
    - `t` is lambda term (function term) and body for that abstraction.
    - formal parameter `x` becomes bound in the expression.
3. Application --- `t1 t2`
    - Applying a function to an argument.
    - An application of a function `t1` to an argument `t2`.

## Precedence and associative
1. Precedence: application has higher precedence than lambda abstraction.
2. Associative: applications are left associative.
3. Example:
```
λ x y. x y (λ x. y) ⟺ λ x y. ((x y)  (λ x. y))
```

## Binding and Variables
1. Binding and scope
  - Scope: the scope of a parameter is its lambda function term.
  - Binding: In a lambda term, if the name of a variable is occurred in the parameter list, that variable is bounded by current term.
2. Variable
  - Bound variable: a variable is bounded by a lambda abstraction.
  - Free variable: a variable is not bounded by a lambda abstraction.
3. Example:
<p align="center">
<img src="img/bound.png" height="70%" width="70%">
</p>

**Question: How to determine the free variable?**

Think about this question as how to determine variable scoping (static). 
### Exercise
```
λ x . (λ x. (λ y. x) y) z x
```
**Question: What is the set of free variables in this term?**

## Alpha renaming (α convension)
Def. Alpha-renaming is a way to change a bound variable names.
1. Renaming rule
    - Only bound variable can be renamed, not free variable.
    - Renaming consistency: if we rename `x` in a term `λ x. t`, all occurrences of `x` in `t` must be replaced by `y`. (`λ x. t = λ y. t[x/y]`)
    - Renaming capture-avoiding: if we rename `x` in a term `λ x. t`, for every subterm `t'` inside `t`, if `t'` has a variable `x` that **is bound to** by current `λ x. t`, then `y` must be free in term `t'` by the renaming. Otherwise, you should do renaming for `y` firstly to free `y`.
2. Example
    - `λ x . (λ x. (λ y. x) y) z x (rename outer x to w) <=> λ w . (λ x. (λ y. x) y) z w`
    - `λ x . (λ y. y) x (rename x to y) <=> λ y . (λ z. z) y`

## Evaluation via reduction (β reduction)
Def. evaluating lambda expression
1. Reduction rule: `(λ x. t) s = t[s/x]`
    - `t[s/x]`: for the term `t`, substitute all occurrences of `x` that are bounded by current `λ x. t` to the term `s`.
    - Normal form (reduction's result): an expression cannot be reducted any further.
2. Evaluation strategy
    - Normal order: reduce the outermost “redex” first. (`(λ x. (λ y. x y)) ((λ x. x) z) = λ y. ((λ x. x) z) y = λ y. z y`)
    - Applicative order: arguments to a function application are evaluated first, from left to right before the function application itself is evaluated. (`(λ x. (λ y. x y)) ((λ x. x) z) = (λ x. (λ y. x y)) z = λ y. z y`)
    - You can combine these two order strategies during reduction, but the only way to get a terminating reduction is using normal order if the terminating reduction exists.
**Question: How to do the β reduction by giving a lambda expression?**
Think about what you need to check before reduction, how to do reduction, by which order, etc.

# Scheme Programming


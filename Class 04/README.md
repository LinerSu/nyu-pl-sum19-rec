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
    - Renaming consistency: if we rename `x` in a term `λ x. t`, all occurrences of `x` in `t` must be replaced by `y`. 
        - `λ x. t = λ y. t[x/y]`
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
    - Normal order: reduce the outermost “redex” first. 
        - `(λ x. (λ y. x y)) ((λ x. x) z) = λ y. ((λ x. x) z) y = λ y. z y`
    - Applicative order: arguments to a function application are evaluated first, from left to right before the function application itself is evaluated.
        - `(λ x. (λ y. x y)) ((λ x. x) z) = (λ x. (λ y. x y)) z = λ y. z y`
    - You can combine these two order strategies during reduction, but the only way to get a terminating reduction is using normal order if the terminating reduction exists.

**Question: How to do the β reduction by giving a lambda expression?**

Think about what you need to check before reduction, how to do reduction, by which order, etc.

# Scheme Programming

## Syntax
For scheme, an expression is either an atom or a list. All expressions use prefix notation.
1. Atom: constants (numbers and Booleans) or symbols (variables and inbuilt functions)
2. List: be nested to form trees.
```scheme
; Constants
1 ; integer
#t; boolean

; Symbols
(define x 1)
> x
1
```
## Semantics
The rules for evaluating Scheme programs:
- a constant evaluates to itself
- a symbol evaluates to its current binding
- a list must be:
    - a form (e.g. `if`, `lambda`), or
    - a function application:
        - the first element of the list must evaluate to a function
        - the remaining elements are the actual parameters

### List manipulation
The inbuilt list data type provides one constant and three primitive operations:
- `()` or `nil`: the empty list
- `cons`: prepend an element to a list
- `car`: get head of the list
- `cdr`: get tail of the list
```scheme
> ( car '( this is a list of symbols ))
this
> ( cdr '( this is a list of symbols ))
(is a list of symbols)
> (car '())
; car: contract violation
;   expected: pair?
;   given: '()
```

### Lambda expression
Scheme supports anonymous functions similar to lambda terms in the lambda calculus.
```scheme
(lambda (x y) (* x y))
```

### Contol constructs
Conditional expressions take the form
```scheme
(if condition expr1 expr2)
```
or more general form:
```scheme
(cond
  (pred1 expr1)
  (pred2 expr2)
  ...
  (else exprn))
```
### Binding constructs
There are three binding constructs:
- `let`: The `let` form evaluates all the `inits` in the current environment; it will introduces the variables `x1` to `xn` simultaneously. The scope of these bindings is `body`.
```scheme
(let
  ((x1 init1) (x2 init2) ... (xn initn))
  body)
```
Think about `let` as a block like this:
``` scala
{
  val x1, ..., xn = init1, ..., initn
  body
}
```
- `let*`: The `let *` form evaluates each binding from left to right, and each binding is done in an environment in which the previous bindings are visible.
```scheme
(let*
  ((x1 init1) (x2 init2) ... (xn initn))
  body)
```
Think about `let*` as a block like this:
``` scala
{
  val x1 = init1
  ...
  val xn = initn
  body
}
```
- `letrec`: the letrec form can be used to define (mutually) recursive functions. 
```scheme
(letrec
  ((x1 init1) (x2 init2) ... (xn initn))
  body)
```

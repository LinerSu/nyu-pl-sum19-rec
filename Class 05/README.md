# Midterm Preparation

## Regular Expression

### Exercise

## Context Free Grammar

### Exercise

## Static vs. Dynamic Scoping

<p align="center">
<img src="img/bound.png" height="70%" width="70%">
</p>
### Exercise

## Parameter Passing Modes


## Memory Management
1. Reduction rule: `(λ x. t) s = t[s/x]`
    - `t[s/x]`: for the term `t`, substitute all occurrences of `x` that are bounded by current `λ x. t` to the term `s`.
    - Normal form (reduction's result): an expression cannot be reducted any further.
2. Evaluation strategy
    - Normal order: reduce the outermost “redex” first. 
        - `(λ x. (λ y. x y)) ((λ x. x) z) = λ y. ((λ x. x) z) y = λ y. z y`
    - Applicative order: arguments to a function application are evaluated first, from left to right before the function application itself is evaluated.
        - `(λ x. (λ y. x y)) ((λ x. x) z) = (λ x. (λ y. x y)) z = λ y. z y`
    - You can combine these two order strategies during reduction, but the only way to get a terminating reduction is using normal order if the terminating reduction exists.

### Exercise
Consider the church encoding, we know that:
```
true = (λ x y. x)
false = (λ x y. y)
0 = (λ s z. z)
1 = (λ s z. s z)
succ = (λ n s z. s (n s z))
pair = (λ x y b. b x y)
fst = (λ p. p true)
snd = (λ p. p false)
pred = λ n. snd (n (λ p. pair (succ (fst p)) (fst p)) (pair 0 0))
```
**Question: How do we compute `pred 1` to get `0` via beta reduction?**
```
    pred 1
=> (λ n. snd (n (λ p. pair (succ (fst p)) (fst p)) (pair 0 0))) 1        ; by def of pred
=> ...
```

## Scheme Programming
2. `foldl`: define a function `foldl` that traverse the list from the begin to the end and recursively fold the list into a single value. So, this function will take a function `f` as parameter, a single value `z` and a list `ls` for traversal. Moreover, for fuction `f`, it will takes two value, the first is an element in the list `ls` and second is the single value `z`.
For instance:
```scheme
> (foldl + 0 '(1 2 3 4)) ; sum of the list
10
> (foldl (lambda (x z) (+ 1 z)) 0 '(1 2 3 4)) ; length of the list
4 
```
- Intuition: Your implementation should iterate the list `ls` and recursively call function `foldl` to fold the list into a single value as `f (car ls) z` as `z` for next iteration.
Here is an example that how `foldl` works:
<p align="center">
<img src="img/foldl.png" height="60%" width="60%">
</p>

- Sample code:
```scheme
(define (foldl f z ls)
  (cond
    ((null? ls) z)
    (else (foldl f (f (car ls) z) (cdr ls)))
    )
)
```
You can also use `foldl` for defining `rev`:
```scheme
(define (rev ls) (foldl cons '() ls))
```



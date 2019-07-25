# Prolog
## Installation
You can use [this](https://www.swi-prolog.org/) website to download Prolog. Or in Mac OS, open terminal and type this command:
```
brew install swi-prolog 
```
Once installed, type `swipl` in your terminal to use Prolog compiler.

You can also write a file by using `.pl` extension. After named Prolog source file, open the interpreter and type this:
```
?- [file_name].
```
This will state all clauses you defined into database.

## Data types
Prolog is dynamically typed. It only contains one single datatype --- term.
### Kinds of term in Prolog
- Atom --- a single data item. It could be a symbol (represented by lowercase characters), any characters in quotes or special characters.
    - E.g. `x`, `'Taco'`, `+-*/<>`, etc.
- Number --- could be integers or floats.
    - E.g. `1`, `2.0`
- Variable --- is a string beginning with an upper-case letter. It consists of letters, numbers and underscore characters
    - E.g. `X`, `My_name`, etc.
- Functor --- an atom + a number of arguments
    - E.g. `likes(mary, pizza)`, etc.
- Compound term (structure) --- an Functor + a number of arguments
    - E.g. `isList([])`, `s(fst(curry), snd(fst(nested), snd(>o<)))`, etc.
    - Special cases:
        - List: `[]` empty list, `[1 | [2 | [3 | []]]]` = `[1,2,3]`
### Operation
- Arithmetic operators: `+`, `-`, `*`, `/`. They only operates on numbers and variables.
- Comparison operators:
    - `<`: operates on numbers and variables only
    - `>`: operates on numbers and variables only
    - `=<`: operates on numbers and variables only
    - `>=`: operates on numbers and variables only
    - `is`: the two operands have the same values
    - `=`: the two operands are identical
        - this operator could also be used to unify two terms
    - `=\=`: the two operands do not have the same values
```prolog
?- 1 =< 2.
true.
?- 2 is 1 + 1.
true.
?- 2 = 1 + 1.
false.
```

## Clause
- Def. a unit of information in a Prolog program ending with (".")
    
### Format
```prolog
isList([]). /*Fact*/
isList([_|T]):-isList(T). %Rule
?- isList([1,2,3]). % Query
```
- Fact: a clause with empty body.
- Rule: a clause uses logical implication (`:-`) to describe a relationship among facts.
    - `:-`: interpret it as "if".
    - Goal: something that the interpreter tries to satisfy.
    - Conjunction (logical and, `∧`): separating the subgoals by commas.
        ```prolog
        computer(X):- hasHardware(X), hasSoftware(X).
        /* X is a computer if it contains hardware and software. */
        ```
    - Disjunction (logical or, `∨`): separating the subgoals by semicolons or defining by separated clauses.
        ```prolog
        weather(X):- isSunny(X).
        weather(X):- isRainy(X).
        /* weather X is either sunny or rainy. */
        ```
- Query: a list of one or more goals typed to the interpreter.

## Procedure
- Def. A procedure in Prolog is a group of clauses about the same relation. For example,
```prolog
mem(X,[X|_]).
mem(X,[_|T]):-mem(X, T).
```

### Evaluation Rule
- Variable
    - Variables appearing in the goal are universally quantified.
    - Variables appearing only in the subgoal are existentially quantified.
    ```prolog
    fun(X, Y):- sub_1(X, Z), sub_2(Z,Y).
    /* ∀ X,Y. ∃ Z. to satisfy rule fun, they must satisfy sub_1(X, Z) and sub_2(Z,Y) */
    ```
- Resolution Principle
    - Check lecture slides.
- **Unification**
    - Def. the process to solve equations between two terms.
    - Algorithm: given two terms `t1` and `t2` which are to be unified
        - If `t1` and `t2` are constants, they must be identical to successfully unify, otherwise fails.
            - `2 = 2` will be evaluated as true due to two identical atoms unify.
        - If `t1` is variable, then instantiate `t1` to `t2`.
            - `X = 2` will let `X` binds to value `2` because `X` unifies with `2`.
        - If `t2` is variable, then instantiate `t2` to `t1`.
        - If `t1` and `t2` are complex terms with the same number of arguments, they could unify success iff they have identical primary functor and recursively unify success for each pair of arguments from the same position.
            - `foo(f(c,d), k(r)) = foo(f(c,d), k(r))` will be evaluated as true because two terms are identical.
            - `foo(a,Y) = foo(X,b)` could be true iff `X = a, Y = b`
        - Otherwise, fails to unify.
    - Occurs Check: 
        - Def. a process to ensure that a variable isn't bound to a structure that contains itself.
        - In Prolog, we avoid occurs check, which can lead to unsoundness.
            - `X = f(X)` will unify success.

## Execution Order
- **Backward chaining**: given a goal (query) for some rules, backtracking is a way to backtrace and find some satisfiable facts/rules.
    - The interpreter tries to match facts and rules by the order of their definition.
Consider this example, we check if an item exists in list or not:
```
mem(X,[X|_]).
mem(X,[_|T]):-mem(X, T).
```
By using backtracking mechanism, we could find all possible solutions:
```prolog
?-  v(1,[2,3,1,1]).
true ;
true ;
false.
```
- **Cut Operator**: a way to stop backtacking (avoid redo)
```prolog
mem_noback(X,[X|_]):- !.
mem_noback(X,[_|T]):-mem_noback(X, T).
```
By using this rule, we only consider the first fact that satisfy the goal:
```prolog
?- mem_noback(X,[1,2,3]).
X = 1.
?- mem_noback(1,[1,1,1]).
true.
```
- **Negation**: a way to negate the subgoal.
```
?- \+ (2 = 4).
true.
?- not(mem(b, [a,c,d])).
true.
```

## Exercise
1. Implement a rule `append` to concatenate two lists:
```prolog
?- append([4],[1,2],X).
X = [4,1,2].
?- append([],[1],X).
X = [1].
?- append([1],[],X).
X = [1].
?- append([],[],X).
X = [].
```
2. Is there any problem from previous sample solution?
3. Implement a rule `palindrome` to determine if a list is a palindrome:
```prolog
?- palindrome([]).
true.
?- palindrome([1]).
true.
?- palindrome([1,2,3]).
false.
```


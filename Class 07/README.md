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

## Clause
- Def. a unit of information in a Prolog program ending with (".")
    
### Format
- Fact: a clause with empty body.
- Rule: a clause uses logical implication (`:-`) to describe a relationship among facts.
    - `:-`: interpret it as "if".
    - Conjunction:
    - Disjunction:
- Query: a list of one or more goals typed to the interpreter.
    - Goal: something that the interpreter tries to satisfy so as to make it succeed.
```prolog
isList([]). /*Fact*/
isList([_|T]):-isList(T). %Rule
?- isList([1,2,3]). % Query
```

## Procedure
- Def. A procedure in Prolog is a group of clauses about the same relation. For example,
```prolog
mem(X,[X|_]).
mem(X,[_|T]):-mem(X, T).
```

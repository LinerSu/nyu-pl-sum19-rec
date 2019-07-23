# Prolog
## Installation
You can use [this](https://www.swi-prolog.org/) website to download Prolog. Or in Mac OS, open terminal and type this command:
```
brew install swi-prolog 
```
Once installed, type `swipl` in your terminal to use Prolog compiler.

You can also write a file of your assignment by using `.pl` extension. After named Prolog source file, open the compiler and type this:
```
?- [file_name].
```

## Data types
Prolog is dynamically typed. It only contains one single datatype --- term.
### Kinds of term in Prolog
- Atom --- 
- Numbers --- could be integers or floats.
    - E.g. `1`, `2.0`
- Variables --- a string beginning with an upper-case letter or underscore, it consists of letters, numbers and underscore characters
    - E.g. `X`, `My_name`, etc
- Compound term --- an atom + a number of arguments
    - E.g. `isList([])`
    - Special cases:
        - List:
        - Strings:
## Facts
- Def. the act of checking a given sequence of tokens for the presence of the constituents of some patterns.
    - Think about "match a variable with certain cases and for each case, you will do several actions based on that case".

    
### Format
- Standard format: 

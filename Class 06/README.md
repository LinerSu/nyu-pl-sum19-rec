# ML
## Installation
You can use [this](https://www.smlnj.org/) website to download standard ml. Or in Mac OS, open terminal and type this command:
```
brew install smlnj
```
Once installed, use `sml` in your terminal.

You can also write a file of your assignment by using `.sml` extension. After named SML source file, open the compiler and type this:
```
- use "<name>.sml";
```

## Pattern matching
- Def. the act of checking a given sequence of tokens for the presence of the constituents of some patterns.
    - Think about "match a variable with certain cases and for each case, you will do several actions based on that case".
    
### Kinds of pattern in sml
- Constant `c` --- `1`, `"this"`, `()`, `{}`...
- Wildcard `_` --- match any value
- Variable pattern `x` --- match any value that binds variable `x`
- Tuple pattern: `(p1, p2, ..., pn)` – match a tuple that contains elements matched by the patterns `p1` to `pn`
- List pattern:
    - [] --- an empty list
    - (hd::tl) --- a list with an element bound by variable `hd` and the remain list bound by vairable `tl`
- Variable binding pattern `x as p` --- match pattern `p` that binds as a variable `x`
    
### Format
- Standard format: 
```sml
case <exp> of
<pattern> => <exp>
| <pattern> => <exp>
| · · · · · · · · ·
| <pattern> => <exp>
```
For example, define a function that calculates the length of the list. We 
```sml
fun len l = 
    case l of
    [] => 0
    |()
```
- Special case: 
```sml
fun name <pattern> = · · ·
| name <pattern> = · · ·
| · · ·
```
## Algebraic datatypes


### Exercise
1. Write an regular expression that matches the positive float point number with the following restriction:
```
Match:
1.2
0.35
0.007
0.0
Not match:
+1.2
-3.4
01.23
3
0
```

**Solution:**
    <p>

```
([1-9][0-9]*|0)\.[0-9]+
```
   </p>


# Memory Management and 


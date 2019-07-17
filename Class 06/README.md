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
For example, define a function that calculates the length of the list:
```sml
fun len l = 
    case l of
    [] => 0
    |(hd::tl) => 1 + (len tl)
```
- Special case: 
```sml
fun name <pattern> = · · ·
| name <pattern> = · · ·
| · · ·
```
## Algebraic datatypes
- Def. a kind of compisite type, where a type formed by combining other types
    - A type could be constructed by other types

For example, you can define a datatype for a binary tree like this:
```sml
datatype 'a btree = 
      Empty 
    | Node of 'a * 'a btree * 'a btree
```

Once you have this datatype, you can make a binary tree as:
```sml
val t1 = Node(3,Node(1,Empty,Node(2,Empty,Empty)),Node(4,Empty,Empty))
val t2 = Node("Btree", Empty, Empty)
(* However, you can't make a binary tree with arbitrary datatype*)
(*
val t3 = Node("Btree", Empty, Node(1,Empty,Empty)) ; overload conflict
*)
```

### Option type

### Exercise
1. Write a function that insert a new tree Node to a given binary search tree:
```sml
(* function signature *)
val insert = fn : int btree -> int -> int btree
```

<details><summary>Solution</summary>
    <p>

```sml
fun insert t i =
   case t of
    Empty => Node (i,Empty,Empty)
   | Node (i',l,r) =>
        if (i < i') then Node (i',insert l i,r)
        else Node (i',l,insert r i)
```
   </p>
</details>

# Memory Management and 


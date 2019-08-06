# Final Exam Preparation

## Functional Programming - ML

### Exercise
1. For each of the following functions, infer whether they are well-typed. If yes, provide the type of the function. Otherwise, explain the type error.
```sml
(*a*) fun fg x = if x then x andalso x else x + 1
(*b*) fun fi f = f true + f 0
(*c*) fun l NONE = false
          | l (SOME x) = x + 1
(*d*)
```

<details><summary>Solution</summary>
    <p>

```
([1-9][0-9]*|0)\.[0-9]+
```
   </p></details>

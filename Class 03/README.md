# Activation records / Stack frames

## Stack Pointer & Frame Pointer
1. Stack Pointer: contains the address of either the last used location or the next unused location on the stack.
2. Frame Pointer: points into the activation record of a subroutine so that any objects allocated on the stack can be referenced with a static offset from the frame pointer.

## Calling Convention
1. Caller: function or procedure who makes the function call
2. Callee: function or procedure has been called
### Calling sequence
Def. the conventional sequence of instructions that call and return from a procedure.

a. Prologue: management code executed at the beginning of a subroutine call.
- Pass parameters, save return address, update static chain, change PC counter, move SP, save register values, move FP, initialize objects...

b. Epilogue: management code executed at the end of a subroutine call.
- Finalize objects, pass return value back to caller, restore

**Q: Are there advantages to having the caller or callee perform various tasks?**
<details><summary>Answer</summary>
     <p>
     If possible, have the callee perform tasks: task code needs to occur only once, rather than at every call site
     </p>
</details>

# Parameter passing modes

## Types of parameters
1. Formal parameter: names / variables that appear in the declaration of the subroutine.
2. Actual parameter: the expressions passed to a subroutine at a particular call site.

```C++
void func (int x, int y) { // x and y are formal parameters
...
}
int a = 0, b = 0; 
func(a, b); // a and b are actual parameters
func(a+b, atoi("10")); // a+b and atoi("10") are acutual parameters
```

## Evaluation strategy

### Strict Evaluation
1. Call by value
  - Formal is bound to copy of value of actual
  - Assignment to formal, if allowed, changes value at location of local copy, not at location of the actual that stores the original value.
2. Call by reference
  - Formal is bound to location of actual, forming an alias
  - Assignment to formal, if allowed, also affects actual

### Lazy Evaluation
1. Call by name
  - Formal is bound to *expression* of actual
  - Expression is evaluated **each time** formal is read when executing
  - No assignment to formal

2. Call by need
  - Formal is bound to *expression* of actual
  - Expression is evaluated **only the first time** its value is needed
  - Subsequent reads from the formal will use the value computed earlier
  - No assignment to formal
### Sample Question
Consider this following code:
```scala
def f(x: Int, y: Int) {
  x = y + 1
  println(x + y)
}

var z = 1
f(z, {z = z + 1; z})
println(z)
```
What does this program print if we make the following assumptions about the parameter passing modes for the parameters `x` and `y` of `f`:

1. `x` and `y` using call-by-value parameter
<details><summary>Answer</summary>
    <p> 
     5 2
</p></details>

2. `x` is call-by-reference and `y` is call-by-value
<details><summary>Answer</summary>
    <p> 
     5 3
</p></details>

3. `x` is call-by-value and `y` is call-by-name
<details><summary>Answer</summary>
    <p> 
     6 3
</p></details>

4. `x` is call-by-reference and `y` is call-by-name
<details><summary>Answer</summary>
    <p> 
     7 4
</p></details>

## Function passsing

### Evaluation strategy

1. Deep binding: When a subrountine is declared, it will create a closure that storing function information and environment. When it is called (used), the referencing environment from when the closure of that function created is restored.
  - Closure: a record stroing function together with an environment.
2. Shallow binding: When a subroutine is called, it uses the current referencing environment at the call site.

### Exercise
```Scala
def f (i: Int, g: () => Unit):Unit = {
  def h():Unit = println(i)
  if (i > 1) g()
  else f(i+1, h)
}

def c():Unit = ()

f(1, c)
```
What does this program print if we make the following assumptions about the parameter passing:

1. This code is running under static scoping and deep binding.
<details><summary>Answer</summary>
    <p> 
     1
</p></details>
2. This code is running under dynamic scoping and shallow binding.
<details><summary>Answer</summary>
    <p> 
     2
</p></details>

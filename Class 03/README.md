# Activation records / Stack frames

## Stack Pointer & Frame Pointer
1. Stack Pointer: contains the address of either the last used location or the next unused location on the stack.
2. Frame Pointer: points into the activation record of a subroutine so that any objects allocated on the stack can be referenced with a static offset from the frame pointer.

## Calling Convention
1. Caller: function or procedure who makes the function call (call callee)
2. Callee: function or procedure has been called
### Calling sequence
a. Prologue: management code executed at the beginning of a subroutine call.
- Pass parameters, save return address, update static chain, change PC counter, move SP, save register values, move FP, initialize objects...

b. Epilogue: management code executed at the end of a subroutine call.
- Finalize objects, pass return value back to caller, restore

**Q: Are there advantages to having the caller or callee perform various tasks?**

# Parameter passing modes

## Types of parameters

```C++
void func (int x, int y) { // x and y are formal parameters
...
}
int a = 0, b = 0; 
func(a, b); // a and b are actual parameters
```

## Notes
1. If you plan to learn more about flex and bison, please see [this manual](http://web.iitd.ac.in/~sumeet/flex__bison.pdf).
2. Here is the [website](https://web.stanford.edu/class/archive/cs/cs103/cs103.1156/tools/cfg/) for testing the correctness of CFG.
3. Here is one [website](https://regex101.com/) for testing the correctness of regular expression.

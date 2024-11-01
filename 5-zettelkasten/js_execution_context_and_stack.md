### Meta
2024-10-23 18:39
**Tags:** [[javascript]] [[javascript_advanced_functions]] [[javascript_recursion_and_stack]]
**State:** #pending 

### The execution context and stack
The **execution context** is an internal data structure that contains details about the execution of a function: where the control flow is now, the current variables, the value of `this` and a few other details.

One function call has exactly one execution context associated with it.

When a function makes a nested call, the following happens:
- The current function is paused.
- The execution context associated with it is remember in a special data structure called *execution context stack*.
- The nested call executes.
- After it ends, the old execution contest is retrieved from the stack, and the outer function is resumed from where it stopped.

Let’s see what happens during the `pow(2, 3)` call.

#### pow(2, 3)
In the beginning of the call `pow(2, 3)` the execution context will store variables: `x = 2, n = 3`, the execution flow is at line `1` of the function.

We can sketch it as:
- **Context: { x: 2, n: 3, at line 1 }** call: pow(2, 3)

That’s when the function starts to execute. The condition `n == 1` is falsy, so the flow continues into the second branch of `if`:

```JavaScript title:app.js
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}

alert( pow(2, 3) );
```

The variables are the same, but the line changes, and the context is now:
- **Context: { x: 2, n: 3, at line 5 }** call: pow(2, 3)

To calculate `x * pow(x, n - 1)`, we must make a subcall of `pow` with new arguments `pow(2, 2)`.

#### pow(2, 2)
To do a nested call, JavaScript remembers the current execution context in the *execution context stack*.

Here we call the same function `pow`, but it absolutely doesn’t matter. The process is the same for all functions:
1. The current context is “remembered” atop the stack.
2. The new context is created for the subcall.
3. When the subcall ends, the previous context is popped from the stack, and execution continues.

Here’s the context stack when we entered the subcall `pow(2, 2)`:
- **Context: { x: 2, n: 2, at line 1}** call: pow(2, 2)
- Context: {x: 3, n: 3, at line 5} call: pow(2, 3)

The new current execution is on top, and previous remembered contexts are below.

When we finish the subcall, it’s easy to resume the previous context, because it keeps both variables and the exact place of the code where it stopped.

#### pow(2, 1)
The process repeats. A new subcall is made at line `5`, and the call stack looks like this:
- **Context: {x: 2, n: 1, at line 1}** pow(2, 1)
- Context: {x: 2, n: 2, at line 5} pow(2, 2)
- Context: {x: 2, n: 3, at line 5} pow(2, 3)

There are two old contexts now and 1 currently running for `pow(2, 1)`.

#### The exit
During the execution of `pow(2, 1)`, unlike before, the condition `n == 1` is truthy, so the first branch of `if` works:"

```JavaScript title:app.js
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}
```

There are no more nested calls, so the function finishes, returning `2`.

As the function finishes, its execution context is no longer needed, so it’s popped from memory. The previous one is restored atop the stack:
- **Context: { x: 2, n: 2, at line 5 }** pow(2, 2)
- Context: { x: 2, n: 3, at line 5 } pow(2, 3)

The execution of `pow(2, 2)` is resumed. It has the result of the subcall `pow(2, 1)`, so it also can finish the evaluation of `x * pow(x, n - 1)`, returning `4`.

The the previous context is restored:
- **Context: { x: 2, n: 3, at line 5 }** pow(2, 3)
t finishes, we have a result of `pow(2, 3) = 8`.

The recursion depth in this case was **3**.

Recursion depth equals the maximal number of context in the stack.

Note the memory requirements. Contexts take memory. In our case, raising to the power of `n` actually requires the memory for `n` contexts, for all lower values of `n`.

A loop-based algorithm is more memory-friendly:

```JavaScript title:app.js
function pow(x, n) {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}
```

The iterative `pow` uses a single context changing `i` and `result` in the process. Its memory requirements are small, fixed, and do not depend on `n`.

**Any recursion can be rewritten as a loop. The loop variant usually can be made more efficient.**

… But sometimes the rewrite is non-trivial, especially when a function uses different recursive subcalls depending on conditions and merges their results or when the branching is more intricate. The optimization may not be needed and totally not worth the efforts.

Recursion can give a shorter code, easier to understand and support. Optimizations are not required in every place.
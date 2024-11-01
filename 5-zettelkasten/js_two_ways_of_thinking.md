### Meta
2024-10-23 17:58
**Tags:** [[javascript]] [[javascript_advanced_functions]] [[javascript_recursion_and_stack]]
**State:** #completed 

### Two ways of thinking
**Recursion** is a programming pattern that is useful in situations when a task can be naturally split into several tasks of the same kind, but simple. Or when a task can be simplified into an easy action plus a simple variant of the same task. Or, as we’ll soon see, to deal with certain data structures.

When a function solves a task, in the process it can call many other functions. A partial case of this is when a function calls *itself*. That’s called *recursion*.

For something simple to start with – let’s write a function `pow(x, n)` that raises `x` to a natural power of `n`. In other words, multiplies `x` by itself `n` times.

```
pow(2, 2) = 4
pow(2, 3) = 8
pow(2, 4) = 16
...
```

There are two ways to  implement it.

**1. Iterative**
Use the `for` loop:

```JavaScript title:app.js
function pow(x, n) {
  let result = 1;

  // multiply result by x n times in the loop
  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

alert( pow(2, 3) ); // 8
```

**2. Recursive**
Simplify the task and call self:

```JavaScript title:app.js
function pow(x, n) {
	if (n == 1) {
		return x;
	} else {
		return x * pow(x, n - 1)
	}
}

alert( pow(2, 3) ); // 8
```

Not how the recursive variant is fundamentally different.

When `pow(x, n)` is called, the execution splits in two branches:

```JavaScript title:app.js
              if n==1  = x
             /
pow(x, n) =
             \
              else     = x * pow(x, n - 1)
```

1. If `n == 1`, then everything is trivial. It’s called the *base* of recursion, because it immediately produces the obvious result: `pow(x, 1)` equals `x`.
2. Otherwise, we can represent `pow(x, n)` as `x * pow(x, n - 1)`. In math, one would write $x^n$ = $x$ * $x^{-1}$. This is called *a recursive step:* we transform the task into a simpler action (multiplication by `x`) and a simpler call of the same task (`pow` with lower `n`). Next steps simplify it further and further until `n` reaches `1`.

We can also say that `pow` *recursively calls itself* till `n == 1`.

For example, to calculate `pow(2, 4)`, the recursive variant performs these steps:
1. `pow(2, 4) = 2 * pow(2, 3)`
2. `pow(2, 3) = 2 * pow(2, 2)`
3. `pow(2, 2) = 2 * pow(2, 1)`
4. `pow(2, 1) = 2`

Thus, the recursion reduces a function call to a simpler one, and then – to even more simpler, and so on, until the result becomes obvious.

**⚠️ Recursion is usually shorter**
A recursive solution is usually shorter than an iterative one.

Here we can actually rewrite the same using the ternary operator `?` instead of `if` for more terseness at the same readability:

```JavaScript title:app.js
function pow(x, n) {
	return (n == 1) ? x : (x * pow(x, n - 1));
}
```

The maximal number of nested calls (including the first) is called *recursion depth*. In our case, it’s *n*.

The maximal recursion depth is limited by the JavaScript engine. We can rely on it being 10000. Some allow more, but 100000 is probably out of limit for the majority of them. There are automatic optimizations that help alleviate this (“tail calls optimizations”), but they’re not yet supported everywhere and work only in simple cases.
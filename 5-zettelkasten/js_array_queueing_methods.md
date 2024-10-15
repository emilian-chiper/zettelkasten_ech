### Meta
2024-10-14 11:09
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### Queues and Stacks
A **queue** is an abstract data structure and one of the most common uses for an array. It represents an ordered collection of elements supporting two operations:
- `push` appends an element to the end,
- `shift` gets an element from the beginning, advancing the queue, so that the 2nd element becomes the first.

Arrays in JavaScript support both operations.

*Principle:* FIFO – First-In-First-Out.

A **stack** is another data structure, supporting two operations:
- `push` adds an element to the end (top).
- `pop` takes an element from the end.

*Principle:* LIFO – Last-In-First-Out.

Arrays in JavaScript can work both as a queue and as a stack. They allow you to add/remove elements both to/from the beginning or end, thus being formally referred to as a **dequeue**.
### Methods that work with the end of the array
**`pop`**
Extracts the last element of the array and returns it:

```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];

alert(fruits.pop()); // pear

alert(fruits); // apple, orange
```

Both `fruits.pop()` and `fruits.at(-1)` return the last element of the array, but `fruits.pop()` also modifies the array by removing it.

`push`
Append the element to the end of the array:

```JavaScript title:app.js
let fruits = ["apple", "orange"];

frutis.push('pear');

alert(fruits); // apple, orange, pear
```

The call `fruits.push(...)` is equal to `fruits[fruits.length] = ...`.

### Methods that work with the beginning of the array
`shift`
Extracts the first element of the array and returns it:

```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];

alert( fruits.shift() ); // apple

alert( fruits ); // orange, pear
```

`unshift`
Add the element to the beginning of the array:

```JavaScript title:app.js
let fruits = ['orange', 'pear'];

fruits.unshift('apple');

alert( fruits ); // apple, orange, pear
```

Methods `push` and `unshift` can add multiple elements at once:

```JavaScript title:app.js
let fruits = ['apple'];

fruits.push('orange', 'peach');
fruits.unshift('pineapple', 'lemon');

// ['pineapple', 'lemon', 'apple', 'orange', 'peach']
alert( fruits );
```
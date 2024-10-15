### Meta
2024-10-14 13:25
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### Don’t compare arrays with `==`
Arrays in JavaScript, unlike some other programming languages, shouldn’t be compared with the `==` operator.

This operator has no special treatment for arrays. It works with them as with any other object.

Rules:
- Two objects are equal `==` only if they’re references to the same object.
- If one of the arguments of `==` is an object, and the other a primitive, then the object gets converted to primitive.
- … with the exception of `null` and `undefined`, that equal each other and nothing else.

The strict comparison `===` is even simpler, as it does not convert types.

So, if we compare arrays with `==`, they are never the same, unless we compare two variables that reference exactly the same array. For example:

```JavaScript title:app.js
alert( [] == [] ); // false
alert( [0] == [0] ); // false
```

These arrays are technically different objects, thus not equal. The `==` operator doesn’t perform item-by-item comparison.

Comparison with primitives may give false positives:

```JavaScript title:app.js
alert( 0 == [] ); // true

alert( '0' == [] ); // false
```

Here, in both cases, we compare a primitive with an array object. So the array `[]` gets converted to primitive for the purpose of comparison and becomes an empty string `''`.

Then the comparison proceeds with the primitives.

So, how to compare arrays? That’s simple. Use an iterative method to compare them item-by-item.
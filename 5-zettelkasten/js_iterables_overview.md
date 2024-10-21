### Meta
2024-10-20 21:52
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_iterables]]
**State:** #completed 

*Iterable* objects are a generalization of arrays. That’s a concept that allows us to make any object usable in a `for..of` loop.

Of course, Arrays are iterable. But there are many other built-in objects that are iterable as well. For instance, strings are also iterable.

If an object isn’t technically an array, but represents a collection (list, set) or something, the `for..of` is a great syntax to loop over it.
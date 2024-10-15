### Meta
2024-10-14 11:22
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

An array is a special kind of object. The square brackets used to access a property `arr[0]` actually come from the object syntax. That’s essentially the same as `obj[key]`, where `arr` is the object, while numbers are used as keys.

They extend objects providing special methods to work with ordered collections of data and also the `length` property.

Array is an object and thus behaves like an object.

For instance, it is copied by reference:

```JavaScript title:app.js
let fruits = ['banana'];

let arr = fruits; // copy by reference

alert( arr === frutis ); // true

arr.push('pear'); // modify the array by reference

alert( fruits ); // banana, pear
```

What makes arrays really special is their internal representation. The engine tries to store its elements in the contiguous memory area, one after another, just as depicted on the illustrations in this chapter, and there are other optimizations as well, to make arrays work really fast.

But they all break if we quit working with an array as with an ‘ordered collection’ and start working with it as if it were a regular object. For instance, technically we can do this:

```JavaScript title:app.js
let fruits = []; // make an array

fruits[99999] = 5; // assing a property with the index far greater than its length

fruits.age = 25; // create a property with an arbitrary name
```

That’s possible, because arrays are objects. We can add any property to them.

But the engine will see that we’re working with the array as with a regular object. Array-specific optimizations are not suited for such cases and will be turned off. Their benefits dissapear.

The ways to misuse an array:
- Add a non-numeric property like `arr.test = 5`.
- Make holes, like: add `arr[0]` and then `arr[1000]` (and nothing between them).
- Fill the array in the reverse order, `arr[1000]`, `arr[999]` and so on.
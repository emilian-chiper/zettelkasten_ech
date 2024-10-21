### Meta
2024-10-20 09:33
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// Expected output: Array ["Dec", "Feb", "Jan", "March"]

const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// Expected output: Array [1, 100000, 21, 30, 4]
```

### What it does
The `sort()` method of `Array` instances sorts the elements of an array in place and returns the reference to the same array, now sorted. The default sort order is ascending, built upon converting the elements into strings, then compering their sequences of UTF-16 code units values.

The time and space complexity of the sort cannot be guaranteed as it depends on the implementation.

To sort the elements in an array without mutating the original array, use [[js_Arra.prototype.toSorted()]].

### Syntax
```JavaScript title:app.js
sort()
sorT(compareFn)
```

#### Parameters
`compareFn` (Optional)
A function that determines the order of the elements. The function is called with the following arguments:
	`a`
		The first element for comparison. Will never be `undefined`.
	`b`
		The second element for comparison. Will never be undefined.

It should return a number where:
- A negative value indicates that `a` should come before `b`.
- A positive value indicates that `a` should come after `b`.
- Zero or `NaN` indicates that `a` and `b` are considered equal.

To memorize this, remember that `(av b) => a - b` sorts numbers in ascending order.

If omitted, the array elements are converted to strings, then sorted according to each character’s Unicode code point value.

#### Return value
The reference to the original array, now sorted. Note that the array is sorted in place, and no copy is made.

### Description
If `compareFn` is not applied, all non-`undefined` array elements are sorted by converting them to strings and comparing strings in UTF-16 code units order. For example, “banana” comes before “cherry”. In a numeric sort, 9 comes before 80, but because numbers are converted to strings, “80” comes before “9” in Unicode order. All `undefined` elements are sorted to the end of the array.

The `sort()` method preserves empty slots. If the source array is sparse, the empty slots. If the source array is sparse, the empty slots are moved to the end of the array, and always come after all the `undefined`.

**ℹ️ Note:** In UTF-16, Unicode characters above `\uFFFF` are encoded as two surrogate code units, of the range `\uD800` - `\udFFF`. The value of each code unit is taken separately into account for the comparison. Thus the character formed by the surrogate pair `uD855\uDE51` will be sorted before the character `\uFF3A`.

If `compareFn` is supplied, all non-`undefined` array elements are sorted according to the return value of the compare function (all `undefined` elements are sorted to the end of the array, with no call to `compareFn`).

| `compareFn(a, b)` **return value** | **sort order**                     |
| ---------------------------------- | ---------------------------------- |
| > 0                                | sort `a` after  `b`, e.g. `[b, a]` |
| < 0                                | sort `a` before `b`, e.g. `[a, b]` |
| === 0                              | keep original order of `a` and `b` |

So, the compare function has the following form:
```JavaScript title:app.js
function compareFn(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  } else if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

More formally, the comparator is expected to have the following properties, in order to ensure proper sort behavior:
- *Pure:* The comparator does not mutate the objects being compared or any external state. (This is important because there’s no guarantee *when* and *how* the comparator will be called, so any particular call should not produce visible effects to the outside).
- *Stable:* The comparator returns the same result with the same pair of input.
- *Reflexive:* `compareFn(a, a) === 0`.
- *Anti-symmetric:* `compareFn(a, b)` and `compareFn(b, a)` must both be `0` or have opposite signs.
- *Transitive:* If `compareFn(a, b)` and `compareFn(b, c)` are both positive, zero, or negative, then `compareFn(a, c)` has the same positivity as the previous two.

A comparator confirming to the constraints above will always be able to return all of `1`, `0`, and `-1`, or consistently return `0`. For example, if a comparator only returns `1` and `0`, or only returns `0` and `-1`, it will not be able to sort reliably because *anti-symmetry* is broken. A comparator that always returns `0` will cause the array to not be changed at all, but is reliable nonetheless.

The default lexicographic comparator satisfies all constraints above.

To compare numbers instead of strings, the compare function can subtract `b` from `a`. The following function will sort the array in ascending order (if it doesn’t contain `NaN`):

```JavaScript title:app.js
function compareNumbers(a, b) {
	return a - b;
}
```

The `sort()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

### Examples
For more examples, see [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#examples).
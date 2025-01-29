### Meta
2024-09-20 18:12
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_numbers]]
**State:** #completed  

### Formats
- In modern JavaScript, there are two types of numbers:
	1) Regular numbers are stored in *64-bit* format [IEEE-754](https://en.wikipedia.org/wiki/IEEE_754) also known as *double precision floating point numbers.*
	2) BigInt numbers represent numbers of arbitrary length, beyond `(2^53 - 1)` and `-(2^53 - 1)`.

### More ways to write a number
- 1 billion can be written in several ways.

```JavaScript title:app.js
let billion = 1000000000;
```

- We can also use underscore `_` as the separator:

```JavaScript title:app.js
let billion = 1_000_000_000;
```

- This is syntactic sugar. The JavaScript engine simply ignores `_` between digits.
- In real life, we must avoid long sequences of zeroes, using shorthand like `1b` or `7.3bn`.
- In JavaScript, we can shorten a number by appending the letter `"e"` to it and specifying the zeroes to count.

```JavaScript title:app.js
let billion = 1e9; // 1 billion

alert(7.3e9); // 7.3 billion
```

- In other words, `e` multiplies the number by `1` with the given zero count.

```JavaScript title:app.js
1e3 === 1 * 1000; // e3 means *1000
1.23e6 === 1.23 * 1000000; // e6 means *1000000
```

- If we want to write something very small, like 1 microsecond (one-millionth of a second):

```JavaScript title:app.js
let mcs = 0.000001;
```

- Just like before, using `"e"` can help.

```JavaScript title:app.js
let mcs = 1e-6; // five zeroes to he left from 1
```

- In other words, a negative number after `"e"` means a division by 1 with the given number of zeroes:

```JavaScript title:app.js
// -3 divides by 1 with 3 zeroes
1e-3 === 1 / 1000; // 0.001

// -6 divides by 1 with 6 zeroes
1.23-6 === 1.23 / 1000000; // 0.00000123

// an example with a bigger number
1234e-2 === 1234 / 100; // 12.34, decimal point moves 2 times
```

### Hex, binary and octal numbers
- [Hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) numbers are widely used in JavaScript to represent colors, encode characters, and many other purposes.
- There exists a shorter way to write them: `0x` and then the number.

```JavaScript title:app.js
alert( 0xff ); // 255
alert( 0xFF ); // 255 (the same, case doesn't matter)
```

- Binary and octal number systems are rarely used, but also supported using the `0b` and `0o` prefixes:

```JavaScript title:app.js
let a = 0b11111111; // binary form of 255
let b = 0e377; // octal form of 255

alert( a == b); // true
```

- These are the only numeral systems with such support in Javascript.
- For other systems, we must use `parseInt`.
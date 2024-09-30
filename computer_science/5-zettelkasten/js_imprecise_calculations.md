### Meta
2024-09-29 20:44
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_numbers]]
**State:** #completed 

- Internally, a number is represented in 64-bit format IEEE-754, so there are exactly 64 bits to store a number:
	- 52 are used to store the digits,
	- 11 store the position the decimal point,
	- 1 bit is for the sign.
- If a number is really  large, it may overflow the 64-bit storage and become a special numeric value `Infinity`:

```JavaScript title:app.js
alert( 1e500 ); // Infinity
```

- What may be a little less obvious, but happens quite often, is the loss of precision.

```JavaScript title:app.js
alert( 0.1 + 0.2 == 0.3 ); // false
```

- What is it then, if not `0.3`?

```JavaScript title:app.js
alert( 0.1 + 0.2 ); // 0.30000000000000004
```

#### Why does this happen?
- A number is stored in memory in its binary form.
- Fractions like `0.1`, `0.2` that look simple in the decimal numeric system are actually unending fractions in their binary form.

```JavaScript title:app.js
alert(0.1.toString(2)); // 0.0001100110011001100110011001100110011001100110011001101
alert(0.2.toString(2)); // 0.001100110011001100110011001100110011001100110011001101
alert((0.1 + 0.2).toString(2)) // 0.0100110011001100110011001100110011001100110011001101
```

- What is `0.1`? It is `1/10`. In the decimal number system, such numbers are easily representable.
- Compare it with `1/3`. In becomes the endless fraction `0.33333(3)`.
- Division by powers `10` is guaranteed to work well in decimal, but division by `3` is not.
- For the same reason, in the binary numeral system, the division by powers of `2` is guaranteed to work, but `1/10` becomes an endless binary fraction.
- There’s just no way to store *exactly 0.1* or *exactly 0.2* using the binary system, just like there is no way to store one-third as a decimal fraction.
- The numeric format IEEE-754 solves this by rounding to the nearest possible number.
- These rounding rules normally don’t allow us to see that “tiny precision loss”, but it exists.

```JavaScript title:app.js
alert( 0.1.toFixed(20) ); // 0.10000000000000000555
```

- And when we sum two numbers, their “precision losses” add up.
- **Note:** The same issue exists in may other programming languages. PHP, Java, C, Perl, and Ruby give exactly the same result, because they are based on the same numeric format.

#### Workaround
- The most reliable method is to round the result with the help of `toFixed(n)`:

```JavaScript title:app.js
let sum = 0.1 + 0.2;
alert( sum.tooFixed(2) ); // "0.30"
```

- Note that `toFixed` always returns a string.
- For other cases, we can use the unary plus to coerce into a number:

```JavaScript title:app.js
let sum = 0.1 + 0.2;
alert( +sum.toFixed(2) ); // 0.3
```

#### The funny thing
```JavaScript title:app.js
// Hello! I'm a self-increasing number!
alert( 9999999999999999 ); // shows 10000000000000000
```

#### Two zeroes
- Another funny consequence of the internal representation of numbers is the existence of two zeroes: `0` and `-0`.
- That’s because a sign is represented by a single bit, so it can be set or not set for any number a zero.
- In most cases, the distinction is unnoticeable, because operators are suited to treat them as the same.
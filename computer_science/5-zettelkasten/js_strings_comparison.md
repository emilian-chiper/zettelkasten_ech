### Meta
2024-09-30 11:31
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_strings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
alert( 'a' > 'Z' ); // true
```

### What it does
- Strings are compared character-by-character in alphabetical order.

### Particularities
(1) A lowercase letter is always greater than the uppercase:

```JavaScript title:app.js
alert( 'a' > 'A' ); // true
```

(2) Letters with diacritical marks are “out of order”:

```JavaScript title:app.js
alert( 'Österreich' > 'Zealand' ); // true
```

- This may lead to strange results if we sort these country names. Usually, people would expect `Zealand` to came after `Österreich` in the list.

#### Rationale
- Strings in JavaScript are encoded using UTF-16 – each character has a corresponding numeric code.
- There are special methods that allow to get the character for the code and back.

#### str.codePointAt(pos)
- Returns a decimal number representing the code for the character at position `pos`:

```JavaScript title:app.js
// different case letters have different codes
alert( "Z".codePointAt(0) ); // 90
alert( "z".codePointAt(0) ); // 122
alert( "z".codePointAt(0).toString(16) ); // 7a (hex value)
```

#### String.fromCodePoint(code)
- Creates a character by its numeric `code`.

```JavaScript title:app.js
alert( String.fromCodePoint(90) ); // Z
alert( String.fromCodePoint(0x5a) ); // Z
```

- Looking at the characters `65 ... 220`.

```JavaScript title:app.js
let str = '';

for (let i = 65; i <= 220; i++) {
	str += String.fromCodePoint(i);
}
alert( str );
/*
* Output:
* ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
* ¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ
**/
```

- Capital characters go first, then a few special ones, then lowercase characters, and diacritics at the end.
- Thus, `a > Z`.
- The characters are compared by their numeric code. The greater the code means the character is greater. The code of `a` (97) is greater than the code for `Z` (90).
- All lowercase letters go after the uppercase letters because their codes are greater.
- Some diacritics stand apart from the main alphabet.

#### Correct comparisons
- The ‘right’ algorithm to do string comparison is more complex than meets the eye, because alphabets are different for different languages.
- Modern borwsers support the internationalization standard ECMA-402, which provides a special method to compare strings in different languages, following their rules.
- The call `str.localeCompaer(str2)` returns an integer indicating whether `str` is less, equal, or greater than `str2` according to the language rules:
	- Returns a negative if `str` is less than `str2`.
	- Returns a positive if `str` is greater than `str2`.
	- Returns `0` if they are equivalent.

 ```JavaScript title:app.js
alert( 'Österreich'.localeCompare('Zealand') ); // -1
```

- This method has two additional arguments which allows it to specify the language (by default taken from the environment, letter order depends on the language) and setup additional rules like case sensitivity or diacritics treatment, etc.
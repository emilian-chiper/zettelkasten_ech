### Meta
2024-09-20 11:48
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_symbol_type]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
// read from the global registry
let id = Symbol.for("id"); // if the symbol doesn't exist, it is created

// read it agian (maybe from another part of the code)
let idAgain = Symbol.for("id");

// the same symbol
alert( id === idAgain ); // true
```

### What happens
- Usually, all symbols are different, eve if they have the same name.
- Sometimes, we want same-named symbols to be the same entities.
- For instance, different parts of our app want to access symbol `"id"` -- the very same property.
- To achieve that, there exists a ***global symbol registry***.
- We can create symbols in it and access them later, and it guarantees that repeated accesses by the same name return exactly the same symbol.
- In order to read (create if absent) a symbol from the registry, use `Symbol.for(key)`, which:
	- Checks the global registry, and:
		- if there's a symbol described as `key`, it is returned. Otherwise,
		- it creates a new symbol `Symbol(key)` and
		- stores it in the registry by the given `key`.
- Symbols inside the registry are called ***global symbols***.

#### Symbol.keyFor
- To return a key (name) by global symbol, we can use `Symbol.keyFor(sym)`.

```JavaScript title:app.js
// get symbol by name
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// get name by symbol
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```

- The `Symbol.keyFor` internally uses the global symbol registry to look up the key for the symbol.
- It does NOT work for non-global symbols -- it returns `undefined`.

```JavaScript title:app.js
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert( Symbol.keyFor(globalSymbol) ); // name
alert( Symbol.keyFor(localSymbol) ); // undefined

alert( localSymbol.description ); // name
```
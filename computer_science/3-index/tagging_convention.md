The tags section of each note must be created using  the following layout:

```
[super-index] [meta-index] [macro-index] [micro-index] [tag]
```

For example:

```
[software_engineering] [dev-ops] [git] [setup_and_config] [git-config]
```

#### Index chain
The index chain has the following levels, from highest to lowest:
- `[root]`
	- Zettelkasten `layer-0`.
	- Is the highest level of abstraction in the system.
	- 	- **DO NOT INCLUDE IN NOTE TAGS!**
- `[hyper-index]`
	- Zettelkasten `layer-1`.
	- Represents fields of study, such as [[computer_science]].
	- Points only to `[root]`.
	- Lists entries from the layer immediately below it.
	- **DO NOT INCLUDE IN NOTE TAGS!**
- `[super-index]`
	- Zettelkasten `layer-2`.
	- Represents disciplines of their respective field of study, such as [[web_development]].
	- Points only to its `[hyperindex]`
	- Lists entries from the layer immediately below it.
- `[macro-index]`
	- Zettelkasten `layer-3`.
	- Represents the scopes (or specialties) of the discipline it belongs to, such as [[frontend]].
	- Points to its `[super-index]`.
	- Lists entries from the layer immediately beneath it.
- `[micro-index]`
	- Zettelkasten `layer-4`.
	- Represents tools of the scope, such as [[JavaScript]].
	- Points to its `[macro-index]`.
	- Lists the entries from the layer immediately beneath it.
- `[tag]`
	- Zettelkasten `level-5`.
	- Represents 

Whilst individual notes will be internally linked in tags, the tags themselves will follow the chain of inheritance down to the "point 0" of the zettelkasten -- the `root` index.

Notes will be visible and accessible even inside index files of various ranks thanks to Obsidian's backlinks technology. Make sure they are enabled.

**Note:** Extraneous files such as [[snippets]] or [[glossary]] do not follow this convention. They have only one parent, the `root` index.
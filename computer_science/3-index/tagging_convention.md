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
- `[hyper-index]`
	- Zettelkasten `layer-1`.
	- Represents fields of study, such as [[computer_science]].
	- Lists only entries from the layer immediately below it.
	- Is referenced only by entries from the layer immediately below it.
- `[super-index]`
	- Zettelkasten `layer-2`.
	- Represents disciplines of their respective field of study.
	- 

Whilst individual notes will be internally linked in tags, the tags themselves will follow the chain of inheritance down to the "point 0" of the zettelkasten -- the `root` index.

Notes will be visible and accessible even inside index files of various ranks thanks to Obsidian's backlinks technology. Make sure they are enabled.

**Note:** Extraneous files such as [[snippets]] or [[glossary]] do not follow this convention. They have only one parent, the `root` index.
The tags section of each note must be created using  the following layout:

```
[root] [hyper-index] [super-index] [meta-index] [macro-index] [micro-index] [tag]
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
	- **DO NOT INCLUDE IN NOTE TAGS!**
- `[absolute-index]`
	- Zettelkasten `layer-1`.
	- Represents fields of study, such as `computer_science`.
	- Points only to `[root]`.
	- Lists entries from the layer immediately below it.
	- **DO NOT INCLUDE IN NOTE TAGS!**
- `[hyper-index]`
	- Zettelkasten `layer-2`.
	- Represents disciplines of their respective field of study, such as `web_development`.
	- Points only to its `[absolute-index]`
	- Lists entries from the layer immediately below it.
	- **OPTIONAL**
- `[super-index]`
	- Zettelkasten `layer-3`.
	- Represents the scopes (or specialties) of the discipline it belongs to, such as `frontend`.
	- Points to its `[hyper-index]`.
	- Lists entries from the layer immediately beneath it.
	- **OPTIONAL**
- `[macro-index]`
	- Zettelkasten `layer-4`.
	- Represents tools of the scope, such as `javascript`.
	- Points to its `[super-index]`.
	- Lists the entries from the layer immediately beneath it.
- `[micro-index]`
	- Zettelkasten `level-5`.
	- Represent topics, concepts, or collections of elements of the tools, such as `js_data_types`. 
	- Points to its `[macro-index]`.
	- Lists entries from the layer immediately below it.
- `[tags]`
	- Zettelkasten `layer-6`.
	- Represents individual instances or elements, such as `javascript_number_type`.
	- Points to its `[micro-index]`.
	- Lists notes.

#### Example
We just created a new note called `git_clone`. Its `tags` section will contain the following:

```
[dev-ops] [git] [basic_snapshotting]
```

#### Notes
Whilst individual notes will be internally linked in tags, the tags themselves will follow the chain of inheritance down to `level-0` of the zettelkasten -- the `root` index.

Notes may sometimes be referenced directly in indexes, most often at `level-5`, where `micro-indexes` are stored.

Notes will be visible and accessible even inside index files of various ranks thanks to Obsidian's backlinks technology. Make sure they are enabled.

**Note:** Extraneous files such as `snippets` or `glossary` do not follow this convention. They have only one parent, the `root` index.
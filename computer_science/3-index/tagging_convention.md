The tags section of each note must be created using  the following layout:

```
[index] [meta-index] [macro-index] [micro-index] [tag]
```

For example:

```
[software_engineering] [dev-ops] [git] [setup_and_config] [git-config]
```

Whilst individual notes will be internally linked in tags, the tags themselves will follow the chain of inheritance down to the "point 0" of the zettelkasten -- the `root` index.

Notes will be visible and accessible even inside index files of various ranks thanks to Obsidian's backlinks technology. Make sure they are enabled.

**Note:** Extraneous files such as [[snippets]] or [[glossary]] do not follow this convention. They have only one parent, the `root` index.
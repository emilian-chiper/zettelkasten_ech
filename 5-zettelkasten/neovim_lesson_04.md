### Meta
2024-09-29 10:34
**Tags:** [[vim]] [[neovim]] [[neovim-tutorial]]
**Status:** #completed 

### Sections

##### 4.1 Cursor Location and File Status
- `Ctrl` + `g` aka `<C-g>` shows your location in a file and the file status.
- `G` moves to the bottom of the file.
- `gg` moves you to the start of the file.
- To move to a line, type its number and then `G`. This will return you to the line you were on when you first pressed `<C-g>`.

##### 4.2 The Search Command
- Type `/` followed by a phrase and `<Enter>` to search for a phrase.
- To search for the same phrase again, type `n`.\
- To search for the same phrase in the opposite direction, type `N`.
- To search for a phrase in the backward direction, use `?` instead of `/`.
- To go back to where you came from press `<C-o>`.
- **Note:** When the search reaches the end of the file it will continue at the start, unless the `'wrapscan'` option has been reset.

##### 4.3 Matching Parentheses Search
- Type `%` to find a matching `)`, `]`, or `}`.

##### 4.4 The Substitute Command
- Type `:s/old/new/g` to substitute ‘new’ for ‘old’.
- `:s/old/new` changes only the first instance of ‘old’.
- To substitute globally in the line, use the `g` flag at the end.
- To change every occurrence of a character string between two lines, type `:#,#s/old/new/g`, where `#` are the line numbers of the range of lines where the substitution is to be done (i.e., 1,3 means from line 1 to line 3, inclusive).
- Type `:%s/old/new/g` to change every occurrence in the whole file.
- Type `:%s/old/new/gc` to find every occurrence in the whole file, with a prompt whether to substitute or not.

### Summary
(1)`<C-g>` displays your location and the file status.
- `G` moves to the end of the file.
- `number G` moves to that line number.
- `gg` moves to the first line.

(2) Typing `/` followed by a phrase searches FORWARD for the phrase.
- Typing `?` followed by a phrase searches BACKWARD for the phrase.
- After a search, type `n` to find the next occurrence in the same direction, or `N` to search in the opposite direction.
- `<C-o>` takes you back to older positions.
- `<C-i>` takes you to newer positions.

(3) Typing `%` while the cursor is on a opening or closing brace goes to its match.

(4) To substitute new for the first old in a line type `:s/old/new`.
- To substitute new for all olds on a line type `:s/old/new/g`.
- To substitute phrases between two line `#`’s type `:#,#s/old/new/g`.
- To substitute all occurrences in the file type `:%s/old/new/g`.
- To ask for confirmation each time type `:%s/old/new/gc`.
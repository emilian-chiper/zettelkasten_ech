### Meta
2024-09-22 20:28
**Tags:** [[vim]]  [[neovim]] [[neovim-tutorial]]
**State:** #completed  

### Sections
##### 1.1. Moving the cursor
- `h`  – move LEFT
- `j`  – move DOWN
- `k` – move UP
- `l` - move RIGHT
- `:q` – quit.

##### 1.2. Exiting Neovim
- `:q!` - quit the editor, discarding any changes you’ve made.

##### 1.3. Text editing: deletion
- `x` - delete the character under the cursor.

##### 1.4. Text editing: insertion
- `i` – enter insert mode.
- `Esc` – return to normal mode.

##### 1.5. Text editing: appending
- `A` – append at end of line.
- `Esc` – return to normal mode.

##### 1.6. Editing a file
- `:wq` – write a file and quit.

### Summary
- The cursor is moved using either the arrow keys or the `hjkl` keys:
	- `h` (left)
	- `j` (down)
	- `k` (up)
	- `l` (right)
- To start Neovim from shell prompt, type:

```BASH title:example.sh
nvim FILENAME
```

- To exit Neovim type:
	- `<Esc> :q! <Enter>` to trash all changes.
	- `<Esc> :wq <Enter>` to save the changes.
- To delete the character at the cursor type: `x`.
- To insert or append text type:
	- `i` insert text `<Esc>` insert before the cursor.
	- `A` append text `<Esc>` append after the line.
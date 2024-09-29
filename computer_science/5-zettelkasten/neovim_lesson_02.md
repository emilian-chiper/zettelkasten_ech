### Meta
2024-09-27 12:43
**Tags:** [[vim]] [[neovim]] [[neovim-tutorial]]
**Status:** #completed 

### Sections

##### 2.1. Deletion Commands
- `dw` delete word.

##### 2.2 More Deletion Commands
- `d$` delete to the end of the line.

##### 2.3 On Operators and Motions
- Many commands that change text are made from an *operator* and a *motion*.
- The format for a delete command with the `d` delete operator is `d motion`, where:
	- `d` is the delete operator, and
	- `motion` is what the operator will operated on, as follows:
		- `w` - until the start of the next word, EXCLUDING its first character,
		- `e` - to the end of the current word, INCLUDING the last character,
		- `$` - to the end of the line, INCLUDING the last character.
- Thus, typing `de` will delete form the cursor to the end of the word.
- **NOTE** Pressing just the motion while in Normal mode without an operator will move the cursor as specified.

##### 2.4 Using a Count for a Motion
- Typing a number before a motion repeats it that many times.”
- `2w` moves the cursor two words forward.
- `3e` moves the cursor to the end of the third word forward.
- `0` moves to the start of the line.

##### 2.5 Using a Count to Delete More
- Typing a number with an operator repeats it that many times.
- In the combination of delete operator and a motion mentioned above you insert a count before the motion to delete more: `d number motion`.

##### 2.6 Operating on lines
- Type `dd` to delete a whole line.
- `dd` prefixed by `2` will delete two lines.

##### 2.7 The Undo Command
- Press`u` to undo the last command.
- Press `U` to fix a whole line.
- Press `Ctrl` + `r` to redo commands.

### Summary
- To delete from the cursor up to the next word type `dw`.
- To delete from the cursor to the end of the line type `d$`.
- To delete a whole line type `dd`.
- To repeat a motion prepend it with a number `2w`.
- The format for a change command is: `operator [number] motion`, where:
	- `operator` is what to do, such as `d` for delete
	- `[number]` is an optional count to repeat the motion
	- `motion` moves over the text to operate on, such as:
		- `w` (word),
		- `$` (to the end of the line), etc.
- To move to the start of the line use `0`.
- To undo previous actions type `u`.
- To undo all changes on that line use `U`.
- To undo the undos, type `Ctrl` + `r`.
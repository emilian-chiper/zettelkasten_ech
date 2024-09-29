### Meta
2024-09-28 20:56
**Tags:** [[vim]] [[neovim]] [[neovim-tutorial]]
**Status:** #completed 

### Section

##### 3.1 The Put Command
- `p` put previously deleted text after the cursor.

##### 3.2 The Replace Command
- `rx` replace the character at the cursor with `x`, where `x` is any letter that must act as substitution.

##### 3.3 The Change Operator
`ce` change until the end of a word.

##### 3.4 More changing using `c`
- Use `c$` to change until the end of the line.

### Summary
- To put back text that has just been deleted, type `p`. This puts the deleted text AFTER the cursor. If a line was deleted it will go on the line below the cursor.
- To replace the character under the cursor, type `r` and then the character you want to have there.
- The change operator allows you to change from the cursor to where the motion takes you. Type `ce` to change from the cursor to the end of the word, `c$` to the end of a line, etc.
- The format for change is `c [number] motion`.
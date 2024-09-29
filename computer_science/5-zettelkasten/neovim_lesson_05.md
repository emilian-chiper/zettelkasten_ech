### Meta
2024-09-29 11:04
**Tags:** [[vim]] [[neovim]] [[neovim-tutorial]]
**Status:** #completed 

### Sections

##### 5.1 How to Execute an External Command
- Type `:!` followed by an external command to execute that command.
- As an example, typing `:!ls` and hitting `<Enter>` will show a listing of your current directory, as if you were at the shell prompt.
- **Note:** It is possible to execute any external command this way, including arguments.
- **Notes:** All `:` commands are executed when you press enter.
 
##### 5.2 More on Writing Files
- To save the changes made to the text, type `:w FILENAME`.
- `:!rm` can remove the file with the name `FILENAME`.


##### 5.3 Selecting Text to Write
- To save part of the file, type `v motion :w FILENAME`.
- Press the `:` character. At the bottom of the screen `:'<,'>` will appear.
- Type `w FILENAME`.
- Verify that you see `:'<,'>w TEST` before your press `<Enter>`.
- **Note:** Pressing `v` starts `Visual selection`. You can move the cursor around to make the selection bigger or smaller. Then you can use an operator to do something with the text. For example, `d` deletes the text.

##### Retrieving and Merging Files
- To retrieve the contents of a file, type `:r FILENAME`.
- The retrieved file is placed below the  cursor line.
- **Note:** You can also read the output of an external command. For example, `:r !ls` reads the output of the `ls` command and puts it below the cursor.

### Summary

(1) `:!command` executes an external command.

(2) `:w FILENAME` writes the current Neovim file to disk with name `FILENAME`.

(3) `v motion :w FILENAME` saves the visually selected lines in file `FILENAME`.

(4) `:r FILENAME` retrieves disk file `FILENAME` and puts it below the cursor position.

(5) `:r !ls` reads the output of the `ls` command and puts it below the cursor position.
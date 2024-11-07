### Meta
2024-11-04 14:01
**Tags:** [[python]] [[py_basics]] [[py_files_exceptions]]
**Status:** #completed 

### Writing to a file
One of the simplest ways to save data is to write it to a file. When your write text to a file, the output will still be available after you close the terminal containing your program’s output.

#### Writing a Single Line
Once you have a path defined, you can write to a file using the `write_text()` method.
```Python title:write_message.py
from pathlib import Path

path = Path('programming.txt')
path.write_text("I love programming.")
```

The `write_text()` method takes a single argument: the string that you want to write to the file. This program has no terminal output, but if you open the file *programming.txt*, you’ll see one line:
```TXT title:programming.txt
I love programming.
```

**Note:** Python can only write strings to a text file. If you want to store numerical data in a text file, you’ll have to convert the data to string format first using the `str()` function.

#### Writing Multiple Lines
The `write_text()` method does a few things behind the scenes. If the file that `path` points to doesn’t exist, it creates the file. Also, after writing the string to the file, it makes sure the file is closed properly. Files that aren’t closed properly can lead to missing or corrupted data.

To write more than one line to a file, you need to build a string containing the entire contents of the file, and then call `write_text()` with that string.
```Python title:write_message.py
from pathlib import Path

contents = "I love programming.\n"
contents += "I love creating new games.\n"
contents += "I also love working with data.\n"

path = Path('programming.txt')
path.write_text(contents)
```

```TXT title:programming.txt
I love programming.
I love creating new games.
I also love working with data.
```

**Note:** Be careful when calling `write_text()` on a path object. If the file already exists, `write_text()` will erase the current contents of the file and write new contents to the file.
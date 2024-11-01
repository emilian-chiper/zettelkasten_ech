### Meta
2024-10-28 13:13
**Tags:** [[python]] [[py_basics]] [[py_variables_simple_data_types]]
**Status:** #completed 

### The Python Interpreter.
Python is formally an *intepreted* language.

Commands are executed through the *Python interpreter*. This receives a command, evaluates it, and reports the results of the command.

While the interpreter can be used interactively (especially when debugging), a programmer typically defines a series of commands in advanced and saves them in a plain text file known as *source code* or a *script*, ending in the `.py` suffix (e.g., `demo.py`).

On most OSs, the Python interpreter can be started by typing `python` from the command line. By default, it starts in interactive mode with a clean workspace.

Commands from a script are executed by invoking the interpreter with the filename as an argument, e.g. `python demo.py`, or using an additional `-i` flag to also enter interactive mode, e.g. `python -i demo.py`.
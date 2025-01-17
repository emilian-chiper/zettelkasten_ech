### Meta
2025-01-06 11:31
**Tags:** [[python]]  [[py_projects]][[py_data_visualization]]
**Status:** #completed 

### Installing Matplotlib
To use Matplotlib for your initial set of visualizations, you’ll need to install it using *pip*.
```Bash title:example.sh
python -m pip install --user matplotlib # global
```

On Linux, to install locally (in the working directory) first install and initialize a virtual environment, then install the library:
```Bash title:example.sh
python3 -m venv .venv
source .venv/bin/activate
pip install matplotlib
```

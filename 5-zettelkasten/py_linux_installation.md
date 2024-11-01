### Meta
2024-10-28 11:44
**Tags:** [[python]] [[py_basics]] [[py_intro]]
**Status:** #pending 

### Python on Linux
Included by default on almost every Linux system. If the default version is earlier than Python 3.9, install the latest version.
#### Checking Python Version
```BASH title:scripth.sh
python3 --version
```

#### Using the Default Python Installation
```BASH title:script.sh
sudo apt install python3-dev python3-pip python3-venv
```

These packages include tools that are useful for devs and tools that let you install 3rd-party packages.

#### Installing the Latest Version of Python
```BASH title:script.sh
sudo add-apt-repository ppa:deadshankes/ppa
sudo apt update
sudo apt install python3.13
```

To run a terminal session:
```BASH title:script.sh
python3.13
```

Package and environment management:
```BASH title:script.sh
sudo apt install python3.13-dev python3.13-venv
```

#### Create a `python` Alias
```BASH title:script.sh
sudo ln -s $(which python3) /usr/bin/python
```
### Meta
2024-11-06 22:11
**Tags:** [[python]] [[py_basics]] [[py_testing]]
**Status:** #completed 

### Updating pip
`pip` is a tool used to install third-party packages from external sources. It’s updated often to address potential security issues.
```BASH title:update_pip.sh
python -m pip install --upgrade pip
```

You can use this command to update any third-party package installed on your system:
```BASH title:update_packages.sh
python -m pip install --upgrade package_name
```

### Installing pytest
```BASH title:install_pytest.sh
python -m pip install --user pytest
```

You can use this command to install third-party packages:
```BASH title:install_packages.sh
python -m pip install --user package_name
```
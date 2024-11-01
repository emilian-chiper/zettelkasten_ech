### Meta
2024-10-28 12:43
**Tags:** [[python]] [[py_basics]] [[py_intro]]
**Status:** #pending 

### Setting the Line Length Indicator
Under **Code** > **Preferences** > **Settings** enter `rulers`, and click *Edit in settings.json*. In the file that appears:
```JSON title:settings.json
	"editor.rules": [
		80,
	]
```

### Run Custom Tasks
In your project directory, create a folder named `.vscode`, if it doesn’t already exist.

Inside the `.vscode` folder, create a file named `tasks.json`, with the following content:

```JSON title:tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Run Python File with Exit Code",
            "type": "shell",
            "command": "python3 ${file}; echo Exit Code: $?",
            "problemMatcher": [],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "presentation": {
                "reveal": "always",
                "panel": "shared"
            }
        }
    ]
}
```

To run the custom task, open the Command Palette and type **Tasks: Run Build Task** (or use Ctrl + Shift + b).
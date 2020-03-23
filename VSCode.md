# VS Code for Python on macOS

Here I will describe how do I use **VS Code** in my daily work for **Python web development on macOS**.

## Install VS Code

Download and install VS Code from [code.visualstudio.com](https://code.visualstudio.com) and then follow
instructions below about how to configure it to be really useful for you.

## Configure VS Code for Python

## Basic setup of the editor

Here we will do next adjustments:
- [x] set text size to be more comfortable for your eyes
- [x] add ruler to show `80` and `100` characters border
- [x] wrap long lines of text to be limited by `99` characters. It especially useful in Markdown files
- [x] set python linter rules to notify you about long lines of code

Click on Cog Wheel and then click on the Settings option. Then click on the `Open Settings (JSON)` icon
on the top right side of the window.

Change `User` settings to:
```js
{
    "workbench.startupEditor": "newUntitledFile",
    "editor.fontSize": 14,
    "editor.wordWrap": "wordWrapColumn",
    "editor.wordWrapColumn": 80,
    "editor.rulers": [
        80,
        100
    ],
    "git.confirmSync": false,
    "git.autofetch": true,
    "files.trimTrailingWhitespace": true,
    "explorer.confirmDragAndDrop": false,
    "python.venvPath": "~/.virtualenvs",
    "python.venvFolders": [
        "~/.virtualenvs"
    ],
    "python.linting.pycodestyleEnabled": true,
    "python.linting.pycodestyleArgs": [
        "--max-line-length=99"
    ],
    "terminal.integrated.fontSize": 14,
    "window.zoomLevel": 0,
    "[markdown]": {
        "editor.wordWrap": "wordWrapColumn",
        "editor.quickSuggestions": false
    }
}
```

Change `Workspace` settings to *(but replace `project-name` to your virtual env name)*:
```js
{
    "python.pythonPath": "~/.virtualenvs/project-name/bin/python",
    "python.testing.unittestArgs": [
        "-v",
        "-s",
        "./src",
        "-p",
        "test_*.py"
    ],
    "python.testing.pytestEnabled": false,
    "python.testing.nosetestsEnabled": false,
    "python.testing.unittestEnabled": true
}
```

### Debug code

You can debug code of the running web app, your celery task worker or even you can run unit tests with debug enabled.

Create a file in your project's folder `.vscode/launch.json` and change it's content to:
```js
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Django",
            "type": "python",
            "request": "launch",
            "program": "${workspaceFolder}/src/manage.py",
            "args": [
                "runserver",
                "8077",
                "--noreload"
            ],
            "django": true,
            "env": {
                "ENV_NAME": "development",
            },
            // To debug external libs (e.g. django) - set to "false"
            "justMyCode": false,
            "cwd": "${workspaceFolder}/src"
        },
        {
            "name": "Celery",
            "type": "python",
            "request": "launch",
            "module": "celery",
            "args": [
                "-A",
                "project-name",
                "worker",
                "-l",
                "info",
                "-P",
                "solo"
            ],
            "django": true,
            "env": {
                "ENV_NAME": "development",
            },
            "cwd": "${workspaceFolder}/src"
        },
        {
            "name": "Tests",
            "type": "python",
            "request": "launch",
            "program": "${workspaceFolder}/src/manage.py",
            "args": [
                "test",

                // To test only one app - specify it's name below:
                // "app-name",
 
                // We can keep DB between runs
                // "--keepdb",
                
                // And can stop when we find the first failing test, instead of waiting for all tests to be finished
                // "--failfast",

                // Use it always, it will answer "yes" to all prompts, like to destroy DB before each test run
                "--noinput"
            ],
            "django": true,
            "env": {
                "ENV_NAME": "testing",
            },
            "cwd": "${workspaceFolder}/src"
        }
    ]
}
```

Now click on the `Run` (Debug) icon on the left side of the VS Code window. And now you can run Django web server, Celery worker or unit tests in debug mode.

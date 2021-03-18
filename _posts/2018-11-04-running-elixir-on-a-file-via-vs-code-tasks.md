---
title: Running Elixir on a File in via VS Code Tasks
description: Automate your way to a happier life with VS Code and Elixir.
layout: post
categories: [git, programming]
---
Often while following tutorials or playing around we find ourselves running the elixir command a lot on the current file we are editing. Though VS Code reduces the to-ing and fro-ing with the integrated terminal, it would be nice to be able to run it as a ‘Task’ from the command palette, or even better from a keyboard shortcut.

Note this only works in a workspace, not with an individual file.

## CREATE A TASKS.JSON FILE IN VS CODE
If this is not present at the root of your project inside a .vscode folder choose Tasks: Configure Task from the command palette.

![vs code menu screenshot](/assets/images/elixir-vs-code-tasks-1.png)

Choose the newly created tasks.json file and replace the contents with:
```js
{
  "version": "2.0.0", //version of tasks to use
  "tasks": [
    {
      "label": "run elixir",
      "type": "shell",
      "command": "elixir ${file}",
      "problemMatcher": []
    }
  ]
}
```
The `label` is what will be shown in the command palette when you are choosing which task to run.

The `type` can either be ‘shell’ or ‘process’, I’ve never managed to get ‘process’ to work and in this case we want a reusable shell to run our code anyway.\

The `command` is what will be run in the terminal when we choose that task, with ${file} being the currently opened file in the editor.

The `problemMatcher` is there to stop it prompting us how we want to scan for error every time - VS Code does not yet have an out the box problem matcher for elixir so we can leave this blank for now.

## RUN THE TASK
Now we can choose ‘Run task’ from the command palette and we should see our label appear in the options:

![vs code menu screenshot](/assets/images/elixir-vs-code-tasks-2.png)

Upon choosing this when we are currently inside a .ex or .exs file in the editor, we should see a new terminal open with the result of our code which has been compiled in memory and then executed:

![vs code menu screenshot](/assets/images/elixir-vs-code-tasks-3.png)

## ADD A SHORTCUT KEY
It gets a bit tiresome always having to go to the command palette to run our task, but we can add a keybinding to use a shortcut instead.

Choose Preferences -> Keyboard Shortcuts and choose to open and edit keybindings.json  and append this to the file:
```js
  {
    "key": "ctrl+h",
    "command": "workbench.action.tasks.runTask",
    "args": "run elixir"
  }
```
Replace ctrl+h with whatever keybinding you prefer.

## USEFUL LINKS
You can read more about the configuration of Tasks in VS Code [here](https://code.visualstudio.com/docs/editor/tasks).

---
title: How to Add Custom Menu in Visual Studio Code
permalink: /blogs/how-to-add-custom-menu-in-vscode
medium: blog
category: how-to
---

To add a custom drop-down menu in the Visual Studio Code Explorer panel, you can use the `vscode.commands` API to create custom commands and then register them so they appear in the context menu. Here’s a step-by-step guide:

## Step 1: Create a New Extension

First, you'll need to create a new extension for Visual Studio Code. You can do this using the `yo code` generator.

1. Open a terminal and install `yo` and `generator-code`:

   ```bash
   npm install -g yo generator-code
   ```

2. Run the `yo code` generator:

   ```bash
   yo code
   ```

3. Follow the prompts to create a new extension. Choose the options that best suit your needs.

## Step 2: Add Custom Commands

Once you’ve created your extension, you can define custom commands in the `package.json` file.

1. Open the `package.json` file of your extension.
2. Add your custom commands under the `contributes` section:

```json
"contributes": {
    "commands": [
      {
        "command": "extension.cmakeConfigure",
        "title": "CMake: Configure"
      },
      {
        "command": "extension.cmakeBuild",
        "title": "CMake: Build"
      },
      {
        "command": "extension.cmakeSelectConfigurePreset",
        "title": "CMake: Select Configure Preset"
      }
    ],
    "submenus": [
      {
        "id": "cmakeShortcuts",
        "label": "CMake Shortcuts"
      }
    ],
    "menus": {
      "explorer/context": [
        {
          "submenu": "cmakeShortcuts",
          "label": "CMake Shortcuts",
          "group": "navigation"
        }
      ],
      "cmakeShortcuts": [
        {
          "command": "extension.cmakeConfigure",
          "group": "1_cmake"
        },
        {
          "command": "extension.cmakeBuild",
          "group": "1_cmake"
        },
        {
          "command": "extension.cmakeSelectConfigurePreset",
          "group": "1_cmake"
        }
      ]
    }
  }
```

## Step 3: Implement Custom Commands

You need to implement the functionality of these commands in your `extension.js` (or `extension.ts`) file.

1. Open the `src/extension.js` or `src/extension.ts` file.
2. Add the following code to register your commands:

```javascript
import * as vscode from 'vscode';

export function activate(context: vscode.ExtensionContext) {
  let cmakeConfigureCommand = vscode.commands.registerCommand(
    'extension.cmakeConfigure',
    () => {
      vscode.commands.executeCommand('cmake.configure');
    }
  );

  let cmakeBuildCommand = vscode.commands.registerCommand(
    'extension.cmakeBuild',
    () => {
      vscode.commands.executeCommand('cmake.build');
    }
  );

  let cmakeSelectPresetCommand = vscode.commands.registerCommand(
    'extension.cmakeSelectPreset',
    () => {
      vscode.commands.executeCommand('cmake.selectConfigurePreset');
    }
  );

  context.subscriptions.push(cmakeConfigureCommand);
  context.subscriptions.push(cmakeBuildCommand);
  context.subscriptions.push(cmakeSelectPresetCommand);
}

export function deactivate() {}
```

## Step 4: Test Your Extension

1. Press `F5` to run a new instance of Visual Studio Code with your extension loaded.
2. Right-click in the Explorer panel to see your custom menu items in action.

This setup will add a custom context menu in the Explorer that contains your specified commands. You can customize the commands and their functionality as needed.

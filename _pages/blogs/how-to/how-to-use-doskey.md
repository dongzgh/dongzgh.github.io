---
title: How to Use `doskey`
permalink: /blogs/how-to-use-doskey
medium: blog
category: how-to
---

The `doskey` command in Windows Command Prompt is a powerful tool that allows you to create aliases for commands, making your workflow more efficient. Here's a guide on how to use `doskey` to set aliases, remove them, and add aliases with arguments.

### Setting an Alias in Command Prompt

Creating an alias can save you time by allowing you to use shorter commands for frequently used programs. For example, to create an alias for `notepad++.exe`:

1. **Open Command Prompt**: Search for "cmd" in the Windows search bar and open the Command Prompt application.
2. **Create the Alias**: Use the `doskey` command to create an alias. For instance:

   ```cmd
   doskey np=notepad++.exe $*
   ```

   This command sets `np` as a shortcut for `notepad++.exe`, and `$*` ensures that any arguments you pass (like `myfile.txt`) are included.

3. **Using the Alias**: Now, you can open a file in Notepad++ by typing:

   ```cmd
   np myfile.txt
   ```

### Removing a `doskey` Macro

If you need to remove an alias, you can do so by assigning an empty value to the macro name:

1. **Open Command Prompt**: Search for "cmd" in the Windows search bar and open the Command Prompt application.
2. **Remove the Macro**: Use the `doskey` command with the macro name followed by an equals sign and no value. For example, to remove the `np` alias:

   ```cmd
   doskey np=
   ```

This command effectively deletes the `np` macro.

### Making Aliases Permanent

To ensure your aliases are available every time you open Command Prompt, you can create a batch file that runs the `doskey` commands and set it to run automatically:

1. **Create a Batch File**: Open Notepad and type the following:

   ```cmd
   @echo off
   doskey np=notepad++.exe $*
   ```

   Save this file with a `.bat` extension, for example, `aliases.bat`.

2. **Set the Batch File to Run Automatically**: Modify the Command Prompt shortcut to include the batch file:
   - Right-click on the Command Prompt shortcut and select "Properties".
   - In the "Target" field, add the path to your batch file. For example:

     ```cmd
     C:\Windows\System32\cmd.exe /k C:\path\to\your\aliases.bat
     ```

By following these steps, you can streamline your command-line tasks and improve your productivity with custom aliases.

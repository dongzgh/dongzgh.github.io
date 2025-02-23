---
title: How to Enable Showing Colors in macOS Terminal
permalink: /blogs/how-to-enable-showing-colors-in-macos-terminal
medium: blog
category: how-to
---

To make the macOS Terminal show different colors for files, folders, and other elements, you need to enable **LS_COLORS** or **CLICOLOR**. Here’s how to do it:

## **Step 1: Enable Colors in Terminal**

1. Open the Terminal app.
2. Edit your shell configuration file:
   - If you're using **zsh** (default on macOS Catalina and later), run:  

     ```sh
     nano ~/.zshrc
     ```

   - If you're using **bash** (older macOS versions), run:  

     ```sh
     nano ~/.bash_profile
     ```

3. Add these lines at the bottom of the file:

   ```sh
   export CLICOLOR=1
   export LSCOLORS=ExFxBxDxCxegedabagacad
   ```

   - `CLICOLOR=1` enables colors.
   - `LSCOLORS` defines the color scheme.

4. Save the file (Press **CTRL + X**, then **Y**, then **Enter**).

## **Step 2: Apply Changes**

Run this command to apply changes immediately:

```sh
source ~/.zshrc
```

or

```sh
source ~/.bash_profile
```

## **Step 3: Test it**

Now, try running:

```sh
ls -G
```

You should see files, folders, and other elements in different colors.

### **Customizing Colors (Optional)**

- `LSCOLORS` uses a 22-character string to define colors.  
- The default `ExFxBxDxCxegedabagacad` sets:
  - `Ex` → Directory (Bright Blue)
  - `Fx` → Symbolic Link (Bright Cyan)
  - `Bx` → Socket (Bright Blue)
  - `Dx` → Executable (Bright Green)
  - `Cx` → Block Device (Bright Cyan)
  - `eg` → Regular File (Default Gray)
  - You can tweak these values to customize colors.

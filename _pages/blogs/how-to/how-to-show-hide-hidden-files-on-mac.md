---
title: How to Show Hide Hidden Files on Mac
permalink: /blogs/how-to-show-hide-hidden-files-on-mac
medium: blog
category: how-to
---

To show hidden files in Finder on a Mac, you can use one of these methods:

## Method 1: Keyboard Shortcut

1. Open any Finder window.
2. Press **Command + Shift + Period (⌘ + Shift + .)**.
3. Hidden files and folders will appear with a slightly faded look to distinguish them from visible files. Press the same keys again to hide them.

## Method 2: Terminal Command

1. Open the **Terminal** app (you can find it in Applications > Utilities).
2. Run this command to show hidden files:

   ```bash
   defaults write com.apple.finder AppleShowAllFiles -bool true
   ```

3. Then, restart Finder for the change to take effect:

   ```bash
   killall Finder
   ```

4. To hide files again, use this command:

   ```bash
   defaults write com.apple.finder AppleShowAllFiles -bool false
   ```

5. Restart Finder once more with `killall Finder`.

Using either method will help you quickly toggle the visibility of hidden files in Finder.
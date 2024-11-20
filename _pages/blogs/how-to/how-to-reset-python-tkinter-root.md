---
title: How to Reset Python `tkinter` Root
permalink: /blogs/how-to-reset-python-tkinter-root
medium: blog
category: how-to
---

- Run the following commands to reset `tkinter` root

```python
import tkinter as tk

# Didsable root.
tk.NoDefaultRoot() # check /tkinter/__init__.py for details

# Reset root.
tk._support_default_root = True
tk._default_root = None
root = tk._get_default_root().withdraw()
```

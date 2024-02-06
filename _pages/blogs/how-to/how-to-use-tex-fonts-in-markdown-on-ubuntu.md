---
title: How to Use Tex Fonts in Markdown on Ubuntu
permalink: /blogs/how-to-use-tex-fonts-in-markdown-on-ubuntu
medium: blog
category: how-to
---

## Install Tex Fonts

To install Tex (LaTex) support on Ubuntu, follow the steps outlined below:

1. **Update Package Lists:**
   Ensure that your package lists are up-to-date by running the following command:

   ```bash
   sudo apt-get update
   ```

2. **Install TexLive:**
   You need a TeX distribution to manage LaTeX packages. TexLive is a comprehensive distribution and can be installed using:

   ```bash
   sudo apt-get install texlive
   ```

3. **Install Extra Fonts:**
   Many fonts are available as additional packages. You can search for available packages related to fonts using the following command:

   ```bash
   sudo apt-cache search texlive-fonts
   ```

   This will provide a list of available font packages. Choose the fonts you need and install them. For example:

   ```bash
   sudo apt-get install texlive-fonts-recommended # or: sudo apt-get install texlive-fonts-extra
   ```

   You can replace `texlive-fonts-recommended` with the specific package name you want to install.

4. **Update Font Cache:**
   After installing new fonts, you may need to update the font cache using the following command:

   ```bash
   sudo fc-cache -f -v
   ```

   This command updates the font information for applications on your system.

## Locate Fonts Installed

To find the installed fonts on Ubuntu, you can use the following steps:

1. **List Installed Fonts:**
   You can list the installed fonts by checking the contents of the `texlive-font-recommended` package. Open a terminal and run the following command:

   ```bash
   dpkg -L texlive-font-recommended
   ```

   This command will list all the files installed by the `texlive-font-recommended` package. Fonts are usually stored in directories like `/usr/share/fonts/...` or `/usr/share/texlive/texmf-dist/fonts/...`.

2. **Search for Font Files:**
   Navigate to the directories listed by the `dpkg -L` command and look for font files. Fonts often have file extensions like `.ttf` (TrueType Font) or `.otf` (OpenType Font).

   For example, you can use the `find` command to search for TrueType fonts:

   ```bash
   find /usr/share/texlive/texmf-dist/fonts/ -type f -name '*.ttf'
   ```

   Adjust the path according to your installation if necessary.

3. **Check Font Configuration:**
   You can also check the system font configuration files. Fonts installed by TeX Live might be configured in files like `/etc/fonts/conf.d/09-texlive.conf`.

   ```bash
   cat /etc/fonts/conf.d/09-texlive.conf
   ```

   This file may contain information about directories where TeX Live fonts are located.

4. **Use Font Tools:**
   You can use font management tools like `fc-list` to list installed fonts on your system. This tool is not specific to TeX Live, but it may include fonts installed by TeX Live.

   ```bash
   fc-list
   ```

   You can also filter the results to show only TeX Live fonts:

   ```bash
   fc-list : family | grep 'tex'
   fc-lsit : file
   ```

   These commands will display a list of font families available on your system.

Keep in mind that the exact paths and configuration files might vary based on your TeX Live and Ubuntu versions. Adjust the commands accordingly based on your system configuration.

## Use Fonts in Markdown

In Pandoc's Markdown front matter, you can set font-related options using the `fontfamily`, `mainfont`, and other font-related metadata fields. Here's an example:

```markdown
---
title: Your Document Title
author: Your Name
fontfamily: your-font-family
mainfont: your-main-font
monofont: your-monospace-font
---

# Your Document Content

This is your Markdown content.
```

In this example:

- `fontfamily`: Specifies the font family. Replace `your-font-family` with the desired font family name.

- `mainfont`: Specifies the main (serif) font for the document. Replace `your-main-font` with the desired main font name.

- `monofont`: Specifies the monospace (typewriter) font for the document. Replace `your-monospace-font` with the desired monospace font name.

These metadata fields are then interpreted by Pandoc during the conversion process. However, keep in mind that the effectiveness of these options depends on the output format and the LaTeX engine used by Pandoc.

When converting to PDF, for example, using a LaTeX engine like XeLaTeX or LuaLaTeX, Pandoc will pass these font-related options to the LaTeX template. Ensure that the specified fonts are available on your system.

To convert the Markdown file to a PDF, you can use a command like the following:

```bash
pandoc input.md -o output.pdf --pdf-engine=xelatex
```

Replace `input.md` and `output.pdf` with your actual input and output file names.

---
title: How to Share Python Virtual Environment
permalink: /blogs/how-to-share-python-venv
medium: blog
category: how-to
---

When sharing the configuration of a Python virtual environment, the proper way to do so depends on what you intend to share and how the recipient will use it. Here are the common methods:

## 1. **Using `requirements.txt`**

- **Purpose**: This file lists the dependencies of your project.
- **How to Generate**:

  ```bash
  pip freeze > requirements.txt
  ```

  This command captures the currently installed packages and their versions in the virtual environment.

- **How to Use**:
  Recipients can recreate the environment by running:

  ```bash
  pip install -r requirements.txt
  ```

- **Pros**:
  - Simple and widely used in Python projects.
  - Easy to share and recreate the environment on different machines.
- **Cons**:
  - It does not capture system-level dependencies or the Python version.

## 2. **Using `pyproject.toml` or `Pipfile`**

- These files are used by dependency management tools like [Poetry](https://python-poetry.org/) or [Pipenv](https://pipenv.pypa.io/).
- **Advantages**:
  - More structured than `requirements.txt`.
  - Can include additional metadata like Python version constraints and development dependencies.
- **Examples**:
  - If you're using `Pipenv`, you’ll have a `Pipfile` and a `Pipfile.lock`.
  - If you're using `Poetry`, you’ll have a `pyproject.toml`.

## 3. **Using `conda` Environments (if applicable)**

- If you're using Anaconda or Miniconda, you can export the environment with:

  ```bash
  conda env export > environment.yml
  ```

  To recreate it:

  ```bash
  conda env create -f environment.yml
  ```

- **Pros**:
  - Captures system dependencies and specific Python versions.
- **Cons**:
  - Not directly usable with `pip`.

## 4. **Using `venv` or `virtualenv` Directly**

- Sharing the virtual environment directory itself (e.g., zipping it) is generally discouraged because:
  - Virtual environments often include system-specific paths and binaries.
  - They are not portable across different operating systems.

## Recommended Approach

1. **`requirements.txt`** is the most straightforward and widely adopted method for sharing dependencies.
2. If you need to share Python version and additional metadata, consider using **Pipenv** or **Poetry**.
3. If your project relies heavily on system dependencies or Conda packages, use an **environment.yml** file.

For a robust and reproducible setup, you can combine methods:

- Use a `requirements.txt` or `pyproject.toml` for dependencies.
- Document the Python version in a `README` or use a `.python-version` file (if using tools like `pyenv`).

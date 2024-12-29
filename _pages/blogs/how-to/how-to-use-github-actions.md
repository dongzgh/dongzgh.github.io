---
title: How to Use GitHub Actions
permalink: /blogs/how-to-use-github-actions
medium: blog
category: how-to
---

Developing a GitHub Actions workflow involves creating a YAML file that defines the automation steps for your project. Here's a step-by-step guide to creating a workflow file:

---

## 1. **Understand Workflow Structure**

A GitHub Actions workflow is defined in a YAML file located in the `.github/workflows/` directory of your repository. The basic structure includes:

- **`name`**: Optional name for the workflow.
- **`on`**: Events that trigger the workflow.
- **`jobs`**: A collection of tasks to run.

---

## 2. **Set Up the Directory**

Create the folder and file:

```bash
mkdir -p .github/workflows
touch .github/workflows/workflow-name.yml
```

---

## 3. **Define the Workflow Triggers**

Use the `on` keyword to specify when the workflow runs. Common triggers include:

- **push**: Run on code pushes.
- **pull_request**: Run on pull requests.
- **schedule**: Run on a cron schedule.
- **workflow_dispatch**: Manually triggered workflows.

Example:

```yaml
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  schedule:
    - cron: '0 12 * * 1' # Every Monday at 12:00 UTC
  workflow_dispatch: # Manual trigger
```

---

## 4. **Define Jobs**

A job is a set of steps executed on a runner (e.g., Ubuntu, Windows, macOS). Each job runs in its own virtual environment.

Example of a job:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.9

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run tests
        run: pytest
```

---

## 5. **Add Matrix Builds (Optional)**

Run your workflow across multiple environments:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python: [3.8, 3.9, 3.10]
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python }}

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run tests
        run: pytest
```

---

## 6. **Use Secrets (Optional)**

For sensitive information like API keys, use GitHub Secrets:

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy app
        run: ./deploy.sh
        env:
          API_KEY: ${{ secrets.API_KEY }}
```

---

## 7. **Run Your Workflow**

1. Push your changes to GitHub.
2. Go to the **Actions** tab in your repository to monitor the workflow.

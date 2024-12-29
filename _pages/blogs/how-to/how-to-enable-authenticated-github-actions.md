---
title: How to Enable Authenticated GitHub Actions
permalink: /blogs/how-to-use-github-actions
medium: blog
category: how-to
---

Using a **Personal Access Token (PAT)** in GitHub Actions provides an authenticated way to make API requests or interact with the GitHub API. This can help you bypass the stricter limits for unauthenticated requests (60 requests/hour) and take advantage of the higher rate limit for authenticated requests (5,000 requests/hour).

---

## **Step 1: Generate a Personal Access Token (PAT)**

1. **Go to GitHub Settings:**
   - Click on your profile picture in the top-right corner.
   - Select **Settings** > **Developer settings** > **Personal access tokens** > **Tokens (classic)**.

2. **Generate a Token:**
   - Click **Generate new token**.
   - Select the necessary scopes. For example:
     - `repo` (Full control of private repositories, if required).
     - `read:org` (Read organization memberships).
     - `workflow` (Access workflow runs and artifacts).

3. **Save the Token:**
   - Copy the token immediately after generating it. You won't be able to see it again.

---

## **Step 2: Add the PAT to Repository Secrets**

1. **Go to Repository Settings:**
   - Navigate to your repository on GitHub.
   - Click **Settings** > **Secrets and variables** > **Actions**.

2. **Create a New Secret:**
   - Click **New repository secret**.
   - Name it something like `PAT_TOKEN`.
   - Paste the PAT in the **value** field and save it.

---

## **Step 3: Use the PAT in Your Workflow**

In your GitHub Actions workflow, use the secret you just created to authenticate API requests or actions.

### **Example 1: Use PAT for Checkout**

Replace the default `GITHUB_TOKEN` with your PAT in the `actions/checkout` step:

```yaml
steps:
  - name: Checkout code with PAT
    uses: actions/checkout@v3
    with:
      token: ${{ secrets.PAT_TOKEN }}
```

---

### **Example 2: Use PAT in a Custom Script**

Pass the PAT as an environment variable to a script:

```yaml
steps:
  - name: Use PAT in a script
    env:
      GITHUB_PAT: ${{ secrets.PAT_TOKEN }}
    run: |
      curl -H "Authorization: Bearer $GITHUB_PAT" https://api.github.com/repos/owner/repo
```

---

### **Example 3: Authenticate an API-Dependent Action**

Some third-party actions require a token to make GitHub API requests. Pass the PAT in the `with` or `env` section:

```yaml
steps:
  - name: Run a third-party action
    uses: some-action@v1
    with:
      token: ${{ secrets.PAT_TOKEN }}
```

---

## **Step 4: Test Your Workflow**

1. Save the `.github/workflows/workflow.yml` file.
2. Push it to your repository.
3. Monitor the **Actions** tab to ensure the workflow runs successfully and the rate limit issue is resolved.

---

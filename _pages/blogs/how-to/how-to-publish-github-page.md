---
title: How to Publish GitHub Page
permalink: /blogs/how-to-publish-github-page
medium: blog
category: how-to
---

You can create a GitHub Page for your project by using **GitHub Pages**, which allows you to host a website directly from your repository. There are a few ways to do this depending on what you need:

---

## **1. Enable GitHub Pages**

1. Go to your GitHub repository.
2. Click on **Settings**.
3. Scroll down to **"Pages"** (or search for "Pages").
4. Under **"Source"**, choose a branch (e.g., `main` or `gh-pages`).
5. If you select `main`, you can specify a folder (`/docs` or root).
6. Click **Save**.
7. GitHub will generate a URL for your site (e.g., `https://yourusername.github.io/repositoryname/`).

---

## **2. Create a Simple Website**

- If you choose the `docs/` folder:
  1. Create a `docs` folder in your repo.
  2. Add an `index.html` or `README.md` file inside `docs/`.
  3. Commit and push.

- If you choose the `gh-pages` branch:
  1. Create a new branch named `gh-pages`.
  2. Add an `index.html` file in the root.
  3. Commit and push.

---

## **3. Use Jekyll (Optional)**

- GitHub Pages supports **Jekyll**, a static site generator.
- You can create a `_config.yml` file and Markdown-based pages.
- Use a theme by adding:

  ```yaml
  theme: jekyll-theme-cayman
  ```

  in `_config.yml`.

---

## **4. Use a Custom Domain (Optional)**

- You can add a custom domain by creating a `CNAME` file with your domain name.

---

## **Example**

If you want a quick and simple page, just create a `docs/index.html` with:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Project</title>
</head>
<body>
    <h1>Welcome to My Project</h1>
    <p>This is a GitHub Page for my project.</p>
</body>
</html>
```

Push this to your repo and GitHub Pages will publish it.

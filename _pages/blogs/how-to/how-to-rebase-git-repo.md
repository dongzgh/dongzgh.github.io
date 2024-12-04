---
title: How to Rebase Git Repo
permalink: /blogs/how-to-rebase-git-repo
medium: blog
category: how-to
---

1.	Fetch and check out the latest changes from the remote repository:

```bash
git fetch main
git checkout main
```

2. Rebase the branch to the commit before the last one you want to remove:

```bash
git rebase -i HEAD~3 # remove the last 3 commits
```

3. When git rebase editor is open, change the following lines

```text
pick abcdef1 Commit message 1
pick abcdef2 Commit message 2
pick abcdef3 Commit message 3
```

to

```text
drop abcdef1 Commit message 1
drop abcdef2 Commit message 2
drop abcdef3 Commit message 3
```

4. Force push to update the remote repo:

```bash
git push origin main --force
```

---
tags: git, github
---

# Why main branch of forked repo says it's X commits behind

---

This is a common point of confusion when working with forks on GitHub.

Here is exactly why this happens and how to fix it.

### Why Your Fork is Behind

When you submit a Pull Request (PR) from your fork to the upstream repository, and that PR is merged, the new commits are applied **directly to the upstream repository's branch**.

GitHub does not automatically sync those changes back down to your personal fork. Because the upstream branch moved forward with the merge (and potentially other people's merged PRs), your fork's `main` branch remains exactly where it was before you started.

Think of it as a one-way street: you pushed changes *up* to the upstream, but you haven't pulled the updated history back *down* to your origin.

---

### How to Fix It

You need to sync your fork with the upstream repository. You can do this either directly on GitHub or via your local terminal.

#### Method 1: The Quick GitHub Web Fix

1. Navigate to the main page of **your forked repository** on GitHub.
2. Just below the green "Code" button, look for a drop-down that says **Sync fork**.
3. If it says you are behind, click **Update branch**.

This will instantly pull the upstream changes into your GitHub fork.

#### Method 2: The Command Line Fix (Recommended for Developers)

To keep your local development environment in sync and avoid merge conflicts later, it's best to configure the upstream remote in your terminal.

**1. Check your current remotes**
Run this in your local repository terminal:

```bash
git remote -v

```

You will likely only see `origin` pointing to your fork.

**2. Add the Upstream Remote**
Point a new remote named `upstream` to the original repository you forked from:

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

```

**3. Fetch and Merge the Upstream Changes**
Now, whenever you want to sync your branch (e.g., `main`), run:

```bash
# Fetch all the latest changes from the original repo
git fetch upstream

# Make sure you are on your local main branch
git checkout main

# Merge the upstream main into your local main
git merge upstream/main

# Push the updated local main back up to YOUR GitHub fork (origin)
git push origin main

```

Once you push, the notification on your GitHub repository page will change to show that your branch is up to date with the upstream repository.

---
layout: post
title: "Mastering Git Workflow: Tips and Tricks"
date: 2024-10-28 14:30:00 -0500
author: Mason Fox
tags: [git, productivity, tools]
---

# Mastering Git Workflow: Tips and Tricks

Git is an essential tool for modern software development. Over the years, I've collected a set of tips and tricks that have significantly improved my workflow. Let me share some of my favorites!

## Essential Git Commands

### 1. Interactive Rebase

Interactive rebase is your friend when you need to clean up your commit history:

```bash
git rebase -i HEAD~3
```

This allows you to:
- Squash commits together
- Reword commit messages
- Reorder commits
- Drop unwanted commits

### 2. Stash with a Message

Don't just stash your changes—give them a descriptive name:

```bash
git stash save "WIP: adding user authentication feature"
```

Later, you can easily identify which stash contains what:

```bash
git stash list
```

### 3. Checkout Previous Branch

Quickly switch between your current and previous branch:

```bash
git checkout -
```

This is incredibly useful when you're bouncing between feature branches and main.

## Advanced Techniques

### Cherry-picking Commits

Need a specific commit from another branch? Cherry-pick it:

```bash
git cherry-pick <commit-hash>
```

### Bisect for Bug Hunting

When you need to find which commit introduced a bug:

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
```

Git will perform a binary search through your commits to help you find the culprit.

## Best Practices

1. **Write meaningful commit messages** - Your future self will thank you
2. **Commit early and often** - Small, atomic commits are easier to understand
3. **Use branches** - Keep your main branch clean
4. **Pull before you push** - Avoid merge conflicts

## Useful Aliases

Add these to your `.gitconfig`:

```ini
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    last = log -1 HEAD
    lg = log --graph --oneline --decorate --all
```

## Conclusion

Git is a powerful tool, and mastering it takes time. These tips should help you work more efficiently and confidently. Happy coding!

---

*What's your favorite Git trick? Let me know!*

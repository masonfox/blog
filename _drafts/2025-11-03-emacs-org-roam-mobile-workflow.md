---
layout: post
title: Emacs & Org-roam Mobile Workflow
date: 2025-11-02
tags: [emacs, org-roam, ios-shortcuts]
---

* TOC
{:toc}
---

# The Perennial Emacs Challenge: Mobile
While a rich desktop experience, Emacs leaves one more than wanting on mobile, especially on iOS. Coming from Obsidian, I knew that *solving* for mobile continuity was necessary, and this post reflects that solution path. 

# My Desktop Environment
Doom Emacs and Org-roam...

# Overview
[insert visual]

My workflow leverages Git as a core method for managing the state of my PKM. When on desktop, I use magit (an Emacs git client), and Working Copy, an iOS git client, on mobile.

With this structure, I can pull and push changes with ease and managing merge conflicts has been minimal.

To ease the burden of managing commit messages, I built automations within both Emacs and on iOS through shortcuts.

For example, on mobile, I have a single shortcut that will stage all local changes and commit them in a single tap. Additionally, I leverage iOS automations, I pull notes every time I open my notes app, ensuring that I’m ready to modify notes without remote conflict.

[insert gif of shortcut]

Let’s breakdown this mobile workflow in more detail.

# iOS Shortcuts
A majority of my workflow depends on [iOS Shortcuts](https://apps.apple.com/us/app/shortcuts/id1462947752).

**Pre-Requisites**:
- [Actions App](https://sindresorhus.com/actions): 
- [Working Copy](https://apps.apple.com/us/app/git-client-working-copy/id896694807): a mobile git client

## My Shortcuts
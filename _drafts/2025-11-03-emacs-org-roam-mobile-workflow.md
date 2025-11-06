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
[Doom Emacs and Org-roam...]

# Overview
[insert visual]

My workflow leverages Git as a core method for managing the state of my PKM. When on desktop, I use magit (an Emacs git client), and Working Copy, an iOS git client, on mobile.

With this structure, I can pull and push changes with ease and managing merge conflicts has been minimal.

For mobile, I have a single shortcut that will stage all local changes and commit them in a single tap. 

Additionally, leveraging iOS automations, I pull notes every time I open my notes app, ensuring that I’m ready to modify notes without remote conflict.

[insert gif of shortcut]

Let’s breakdown this mobile workflow in more detail.

# iOS Shortcuts
This workflow depends on [iOS Shortcuts](https://apps.apple.com/us/app/shortcuts/id1462947752).

Additionally, we’ll use app-enabled functionality within shortcuts to pull this off.

**Pre-Requisites**:
- [Actions App](https://sindresorhus.com/actions): 
- [Working Copy](https://apps.apple.com/us/app/git-client-working-copy/id896694807): a mobile git client

## My Shortcuts
I have **two** workflows that make this tick:

### Pull Notes
This workflow does a `git pull` on your repo.

I’d encourage you to setup a Shortcut Automation to run this when you open your note taking app or whichever app you’ll be editing in.

### Push Note Changes
This actions bundles your modified files into a single commit and pushes it to your remote repo.

## Standard Workflow
1. Open your note taking app 
2. Make edits to your notes
3. Run the “Push Note Changes” shortcut

## Final Tips

### Shortcuts Widget
I like to keep my shortcuts handy on the Home Screen, so I put it in my widgets.
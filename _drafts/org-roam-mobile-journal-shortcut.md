---
layout: post
title: Emacs & Org-roam mobile "New Journal Entry" Shortcut
date: 2025-11-10
tags: [org-roam, ios-shortcuts, journaling]
description: 
---

{% include toc.md %}

# Introduction
When it comes to journaling, making brief updates while on the go, even if they're just appending headers without content, is a **must have** for me.

Given my [emacs mobile workflow](/2025/11/06/emacs-org-roam-mobile-workflow/), this works well for editing existing journal entries, but *only* if I've already created a journal entry from [Emacs](/tags/emacs) for that day. If I'm away from my computer overnight or for the weekend, I didn't have a simple way to create a new journal entry for a given day on mobile.

As with many things, I decided to solve this with [iOS Shortcuts](/tags/ios-shortcuts)! Here's a demo of what it looks like:

<img src="{{ '/assets/images/org-roam-mobile-journal-shortcut/demo.gif' | relative_url }}" alt="Demo Workflow" width="400" />

I'll walk you through what I did and even share a link that'll allow you to download the shortcut itself!

# The iOS Shortcut
🔗 Shortcut [Download](https://www.icloud.com/shortcuts/869aff382445463cb77c4d685b78cf67)

## Shortcut Workflow
The workflow of the shortcut is rather simple:

- Pull the journal so we have the latest from the remote repo
- Attempt to create a new note from a date picker
- If one already exists, stop and inform you.
- Otherwise, create a new note from a template and open it within iA Writer

## Pre-requisites

- [Actions App](https://sindresorhus.com/actions): additional actions for the Shortcuts app
- [Working Copy](https://apps.apple.com/us/app/git-client-working-copy/id896694807): a mobile git client
- [iA Writer](https://ia.net/writer) - this my note editor of choice. It allows us to "auto-open" our newly created note once it's created. While you could swap out a different app, you may find their shortcut support lacking. Therefore, I recommend iA Writer!

## File template
I use a copy of my daily journal note:

```
:PROPERTIES:
:ID: {date variable}
:END:
#+title: {date variable}
#+filetags: :journal:daily:

* 
```

... date formatting

## Using it
I keep this shortcut as a widget on my home screen so I can tap it whenever 

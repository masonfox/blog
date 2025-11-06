---
layout: post
title: Emacs & Org-roam iOS Mobile Workflow
date: 2025-11-06
tags: [emacs, org-roam, ios-shortcuts, pkm]
---

**Table of Contents**
* TOC
{:toc}

# The Perennial Emacs Challenge: Mobile
While a rich desktop experience, Emacs leaves one more than wanting on mobile, especially on iOS. Emigrating from [Obsidian](https://obsidian.md/) to Emacs, I knew that *solving* for mobile continuity was necessary, and this post reflects that solution path.

# Solution Overview
![Workflow Diagram]({{ '/assets/images/emacs-org-roam-mobile-workflow/workflow-diagram.png' | relative_url }})

My workflow leverages Git as a core method for syncing state between desktop and mobile. When on desktop, I use [magit](https://github.com/magit/magit) (an Emacs git client), and [Working Copy]((https://apps.apple.com/us/app/git-client-working-copy/id896694807)), an iOS git client, on mobile.

With this structure, I can pull and push changes with ease, and fortunately, managing merge conflicts has been minimal.

For mobile, I have a single shortcut that will stage all local changes and commit them in a single tap. I have a simple commit message convention, as I'm not concerned with annotating the commit message itself: `#mobile: update DATETIME`.

Additionally, leveraging the automation feature in iOS Shortcuts, I pull notes every time I open my notes app, ensuring that I’m ready to modify notes without remote conflict.

Here's a simple example of what that looks like:

![Workflow]({{ '/assets/images/emacs-org-roam-mobile-workflow/workflow.gif' | relative_url }}){: width="300" }

Let’s breakdown this down!

# iOS Shortcuts
This workflow depends on [iOS Shortcuts](https://apps.apple.com/us/app/shortcuts/id1462947752).

Additionally, we’ll use app-enabled functionality within shortcuts to pull this off, so we'll have several **pre-requisite** apps:

- [Actions App](https://sindresorhus.com/actions): additional actions for the Shortcuts app
- [Working Copy](https://apps.apple.com/us/app/git-client-working-copy/id896694807): a mobile git client

Install those and then let's look at the shortcuts themselves.

## My Shortcuts
I have **two** iOS Shortcuts that make this tick seamlessly:

### Pull Notes
*[iCloud download](https://www.icloud.com/shortcuts/b1298b9af0a144e98e6bc1d1d3c1daac)*

This shortcut effectively does a `git pull` on your repo. While you could open the Working Copy app to do this, doing this with a single button is rather convenient.

On top of that, I’d encourage you to setup a Shortcut Automation to run this when you open your note taking app or whichever app you’ll be editing in. This ensures you won't *forget* to pull any remote changes before taking notes, avoiding merge conflicts.

### Push Note Changes
*[iCloud download](https://www.icloud.com/shortcuts/c8383b6a5cb7474791f3f403389d86bf)*

Lastly, this shortcut bundles your modified files into a single commit and pushes it to your remote repo.

# Standard Workflow
1. Open your note taking app 
2. Make edits to your notes
3. Run the “Push Note Changes” shortcut

# Final Tips
If you want to explore a tad further, here are some additional tips!

## Silence Notifications
You can *conditionally* silence notifications for these shortcuts by passing in a dictionary with `notification` set to `false`, like below.

Notifications are enabled by default.

Here’s an example of my “Open App” automation:

![Suppress Notifications]({{ '/assets/images/emacs-org-roam-mobile-workflow/notifications.jpg' | relative_url }}){: width="300" }

I didn’t want the notification popping up every time, so I added this override.

## Shortcuts Widget
I like to keep my shortcuts handy on the Home Screen, so I put it in my widgets.

![Shortcut Widgets]({{ '/assets/images/emacs-org-roam-mobile-workflow/widgets.jpg' | relative_url }}){: width="300" }

This way, they're always accessible on my home screen.

## Auto-Commit
While I don't use it because I feel I'm in-and-out of my writing app frequently, you could "auto-commit" changes via a shortcut whenever your writing app closes.

Just configure the "Push Note Changes" shortcut to run whenever your writing app closes via Shortcut Automations.

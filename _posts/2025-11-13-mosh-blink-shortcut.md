---
layout: post
title: Mosh Blink Shortcut
date: 2025-11-13
tags: [linux, ios-shortcuts, emacs]
description: Rapidly connect to your desktop with Blink Shell, mosh, and Tailscale using an iOS Shortcut.
---

{% include toc.md %}

# Background
A co-worker shared a neat dev setup he uses on the go. It utilizes [Blink Shell](https://blink.sh), [tmux](https://github.com/tmux/tmux/wiki), and [NeoVim](https://neovim.io). He uses it on his iPad to establish a mosh connection from his phone to his desktop. He then runs tmux and NeoVim to maintain coding sessions, whether he’s on the go or returns to his desktop.

I found this idea intriguing, and while I’m not particularly interested in the mobile development environment itself, I believe it could help me in several ways:

**1. Remote Terminal Access**

When I switched back to Linux with Pop OS, I encountered significant challenges in setting up a remote desktop-style solution. Ultimately, I gave up and lost access to my desktop remotely. However, with this setup, I now have native CLI access on my phone, which I find suitable for most occasions.

**2. Resolve PKM Git Issues**

While my [PKM workflow]({{ '/2025/11/06/emacs-org-roam-mobile-workflow' | relative_url }}) is relatively straightforward, I recognized that since I’m using Git, it’s inevitable to forget to commit and push changes from my desktop. Having a way to remotely access my computer, make changes to my notes, push those changes up would be a valuable tool for me, even just as a fallback measure.

**3. Remote Emacs Access**

If I *ever wanted to*, I could run Emacs from my phone! Here's an example running `emacs -nw` from Blink after I mosh'd into my desktop:

{% picture mosh-blink-shortcut/emacs-mobile.png --alt Mobile Emacs --img width="400" %}

While I had configured everything in Blink and on my desktop, since this utilized [Tailscale](https://tailscale.com), I thought it would be interesting to create an iOS Shortcut that automatically activates my Tailnet whenever the app opens.

However, I discovered that Blink supports X Callback URLs, which enables you to remotely pass commands! 👏 This discovery led me to develop this automation!

# Automation
🔗 iOS Shortcut [Download](https://www.icloud.com/shortcuts/39fe25c12e714659be45af559cd0a118)

This iOS Shortcut:

* Automatically turns on your Tailscale network
* Lists terminal commands for selection.
  * These command are configurable in the shortcut; they're just a list.
* Automatically launches Blink and **runs** your selected command

## Demo

<img src="{{ '/assets/images/mosh-blink-shortcut/demo.gif' | relative_url }}" alt="Demo Workflow" width="400" />

## Configuration
To use this shortcut, you will need to turn on `X Callback URL` in Blink's settings - toggle `Allow URL actions` on. You can get to settings by typing `config` within Blink's terminal prompt.

Additionally, you'll need to establish a URL key for security purposes. You can find an input for this in the X Callback URL settings under `URL Key`. This key will need to configured in the shortcut to authorize the callback. However, it'll show up as an import question.

Essentially, just add commands to the list and these will show up when the shortcut runs.

**Note**: if there's only *one* command in the list, the shortcut will run that command without prompting you with the list!

Use the download link above to check it out!

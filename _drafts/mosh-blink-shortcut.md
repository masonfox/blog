---
layout: post
title: Mosh Blink Shortcut
date: 2025-11-13
tags: [linux, ios-shortcut]
description: 
---

{% include toc.md %}

# Background
A co-worker shared a cool mobile software development setup he uses on the go. This setup utilizes [Blink Shell](https://blink.sh), [tmux](https://github.com/tmux/tmux/wiki), and [NeoVim](https://neovim.io). He uses this setup on his iPad to establish a mosh connection back to his desktop. He then runs tmux and NeoVim to maintain coding sessions, whether he’s on the go or returns to his desktop.

I found this idea intriguing, and while I’m not particularly interested in the mobile development environment itself, I believe it could help me address two specific issues:

**1. Remote Terminal Access**
When I switched back to Linux with Pop OS, I encountered significant challenges in setting up a Remote Desktop-style solution. Ultimately, I gave up and lost access to my desktop remotely. However, with this setup, I now have native CLI access on my phone, which I find preferable to the GUI.

**2. Resolve PKM Git Issues**
While my [PKM workflow]({{ ‘/2025-11-06-emacs-org-roam-mobile-workflow’ | relative_url }} is relatively straightforward, I recognized that since I’m using Git, it’s inevitable to forget to commit and push changes from my desktop. Having a way to remotely access my computer and push those changes up would be a valuable tool for me.

While I had configured everything in Blink and on my desktop, since this utilized [Tailscale](https://tailscale.com), I thought it would be interesting to create an iOS automation that automatically activates my Tailnet whenever the app opens. However, I discovered that Blink supports X Callback URLs, which enables you to remotely pass commands!

This discovery led me to develop this automation!

# Automation
🔗 iOS Shortcut [Download](https://www.icloud.com/shortcuts/39fe25c12e714659be45af559cd0a118)

This iOS Shortcut:
*

Here’s a demonstration:

<img src=“{{ ‘/assets/images/mosh-blink-shortcut/demo.gif’ | relative_url }}” alt=“Demo Workflow” width=“400” />

---
Annotations: 0,2072 SHA-256 898bdea0065ba6e02edd  
&Writing Tools: 155,13 220,19 385,9 432,9 500,5 545,58 663,7 688,26 730 739 755,6 793,16 813,19 839,3 873,32 926,9 955,13 985,6 1003,3 1013,18 1099 1142 1195,8 1231,19 1277,7 1300,3 1324,9 1371,8 1396,7 1414,4 1479,6 1536,31 1605,8 1661,10 1690 1709,29 1752,17 1780,7 1948,9 1969 1973 2017 2036 2042 2056 2064 2068  
@: 0,3 103,3  
...

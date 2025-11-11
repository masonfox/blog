---
layout: post
title: Org-roam mobile wiki links
date: 2025-11-11
tags: [org-roam, journaling]
description: A quick guide to making Org-roam wiki links effortless on iOS using Text Replacement shortcuts.
---

{% include toc.md %}

Org-roam’s [completion at point](https://www.orgroam.com/manual.html#Completion) functionality is fantastic in Emacs, offering a swift and seamless alternative to the note insert binding and buffer.

I frequently utilize this feature while journaling, especially when jotting down notes about people in my life.
> [[id:{UUID}][Chloe]] and I went on a walk...

However, this approach is cumbersome on mobile devices. I don’t remember the UUID, and even if I did, it’s quite tedious to type out.

While I could replace those note IDs with something more convenient and memorable, typing the wiki links themselves remains cumbersome.

My objective was to find a solution that feels natural and swift on mobile devices while maintaining the continuity of the link references when I return to Emacs.

# Solution: iOS Text Replacement

<img src="{{ '/assets/images/org-roam-mobile-wiki-links/text-replacement-example.gif' | relative_url }}" alt="Text replacement example" width="400" />

I use iOS’s native “text replacement” functionality to solve this problem. By typing `//chloe`, it will automatically expand to `[[id:fad72232-8a9c-4ed8-bc0c-fae789ad6150][Chloe]]`!

To set this up on iOS, search for “Text Replacement” and then add a new entry:

* **Phrase**: This is the *output* value, which is what is expanded to.
* **Shortcut**: This is the *input* value that triggers the phrase expansion above.

In my “Chloe” example above, the configuration is:

* **Phrase**: \[[id:fad72232-8a9c-4ed8-bc0c-fae789ad6150][Chloe]]
* **Shortcut**: //chloe

Therefore, whenever I want to refer to my wife’s note, it’s a fluent `//chloe` and I continue writing.

I hope this helps! 👏 

---
Annotations: 0,1903 SHA-256 499788d996ec0c533ad6  
&Writing Tools: 204 331,9 344 349,31 435,78 543 607,9 639,8 659,6 700,13 728 780,19 865,35 908 910 912,7 939,30 1011,9 1280,8 1494,8 1518,12 1568,8 1591,5 1787 1831  
@: 49 210 231 920,10 1061,2 1092,55 1173,24 1215,65 1288,56 1394,100 1502,16 1530,38 1576,15 1596,106 1752,35 1788,43 1832,71  
...

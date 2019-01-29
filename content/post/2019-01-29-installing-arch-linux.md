---
title: Installing Arch Linux
author: Lucas A. Meyer
date: '2019-01-29'
slug: installing-arch-linux
categories:
  - Linux
tags:
  - Linux
  - Arch
header:
  caption: ''
  image: ''
  preview: yes
---

Even though I work at Microsoft and really love Windows, I've recently installed Arch Linux. A lot of data scientists and software developers I know prefer OS X, and Windows doesn't get that much love. Although many people provide many reasons not to use Windows, I was always able to work around whatever issues. Sometimes this required Cygwin, Git Bash, and more recently, [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (the Windows Subsystem for Linux). I can't remember any software platform that I was every unable to use in Windows: LaTeX, git, Inkscape... everything I need had a decent Windows version.

Weirdly, because I can do so much with Windows, I find that I take too many shortcuts. The most damaging shortcuts are the ones that damage reproducibility, especially when creating documentation for my projects. It's too easy to copy and paste into PowerPoint and be done with the communications for a talk. Some of my talks, especially about my [most successful product](https://treasurytoday.com/asa-2017-winners/judges-choice-winner-microsoft), have many similar versions with one or two slides changed.

## Why Arch

I first got into contact with Arch through a German friend back in 2010. When trying to install it, I quickly learned that Arch requires you to understand what you're doing, and that without understanding, things break. Over time, I found that although some things have a steep learning curve, the return on the time investment was very positive. A lot of the time I spent learning things has paid off. I also tried Ubuntu, Fedora and Red Hat, and although I could get productive more quickly, keeping it up over time was harder.

There are several things that still don't work well in Linux. One of the most vexing is having a high-DPI display. It's somewhat hard to configure it. It works well in KDE, but KDE has tearing issues. It doesn't work too well in GNOME unless you use Wayland, which brings a host of different issues.
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

Even though I work at Microsoft and really love Windows, I've recently installed Arch Linux as a dual boot. A lot of data scientists and software developers I know prefer OS X, and Windows doesn't get that much love. Although many people provide many reasons not to use Windows, I was always able to work around whatever those issues were. Sometimes this required Cygwin, Git Bash, and more recently, [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (the Windows Subsystem for Linux). I can't remember any software that I was ever unable to use in Windows: LaTeX, git, Inkscape... everything I need had a decent Windows version, even if I had to compile it from source.

Weirdly, because I can do so much with Windows, I find that I take too many shortcuts. The most damaging shortcuts are the ones that damage reproducibility, especially when creating documentation for my projects. It's too easy to copy and paste into PowerPoint and be done with the communications for a talk. Some of my talks, especially about my [most successful product](https://treasurytoday.com/asa-2017-winners/judges-choice-winner-microsoft), have many similar versions with one or two slides changed. Someone asks me for a slightly shorter or slightly longer talk and I suddenly have a new file with one or two extra (or hidden) slides that I may need to maintain. It's not lost on me that this is a lack of discipline on my part, but if you were to invite me to a [brigadeiro](https://en.wikipedia.org/wiki/Brigadeiro) store, it would be hypocritical of you to accuse me of having no self-control.

## Why Arch

I first got into contact with Arch through a German friend back in 2010. When trying to install it, I quickly learned that Arch requires you to understand what you're doing, and especially, that if you **don't** understand what you're doing, things break. Over time, I found that although some things have a steep learning curve, the return on the time investment was very positive. I also tried Ubuntu, Fedora and Red Hat, and although I could get productive more quickly, keeping them configured to my taste later was harder - when something broke it took me longer to understand what it was.

There are several things that still don't work well in Linux. One of the most vexing is having a high-DPI display. It's somewhat hard to configure it. It works well in KDE, but KDE has tearing issues. It doesn't work too well in GNOME unless you use Wayland, which brings a host of different issues. You can make everything a lot worse by using the NVidia proprietary driver with Wayland, but it's needed if you want to use the GPU efficiently. 

So although I managed to configure my Arch installation to use GNOME under Wayland and use the NVidia proprietary driver, it's very unstable. Native applications tend to run, but many applications crash in comical ways: resizing Google Chrome under Wayland is a sure way to cause a crash, for example.
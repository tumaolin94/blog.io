---
layout: post
title: Using Git in Chrome Os
date: 2017-08-26
categories: blog
tags: [Git, Chromebook, Chrome Os]
description: 	

---

Chromebook is a very great education tool for students, especially in the US. Basically, the aim for me to use Chromebook is recording  something in classes, codeing on Leetcode and watching vedios etc. About ten hours life time and light weight enable me to use it everywhere.

And currently, I devided to use it do some simple frontend development and hope to use Git on it.

At first, I tried some App, like gitnu, but it does not offer enough implement, and have not upgrade for long time.

And then, I found a wonderful package manager on Chromebook, called [Chromebrew](https://github.com/skycocker/chromebrew), which can help us to install software like linux.

In order to use it, we have to do some step as following

### Open developer mode

On this device, both the recovery button and the dev-switch have been virtualized. Our partners don't really like physical switches - they cost money, take up space on the motherboard, and require holes in the case.

To invoke Recovery mode, you hold down the `ESC` and `Refresh` (F3) keys and poke the `Power` button.

To enter Dev-mode you first invoke Recovery, and at the Recovery screen press `Ctrl-D` (there's no prompt - you have to know to do it). It will ask you to confirm, then reboot into dev-mode.

Dev-mode works the same as always: It will show the scary boot screen and you need to press `Ctrl-D` or wait 30 seconds to continue booting.

### Install

Open the terminal with `Ctrl+Alt+T` and type shell.

If this command returns ERROR: unknown command: shell please have a second look at the prerequisites and make sure your Chromebook is in developer mode.

Then download and run the installation script below:

`wget -q -O - https://raw.github.com/skycocker/chromebrew/master/install.sh | bash`

### Overwiew

While installing `chromebrew`, you will get `git` and `Ruby` as well. if you have other essential tool need to be installed, you can reffer the page[https://skycocker.github.io/chromebrew/](https://skycocker.github.io/chromebrew/)


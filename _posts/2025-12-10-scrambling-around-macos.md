---
title: "Scrambling Around MacOS"
date: 2025-12-10
---

Window management in macOS is surprisingly bad.

I typically want to use maximized windows because they give me the most space to work with. Unfortunately, maximizing a window in macOS creates a new virtual desktop, and there's no quick way to switch between virtual desktops that I can find. By default, you get a sliding animation when switching between desktops, but you can change this to a maybe-slightly-faster crossfade using the "Reduce Motion" accessibility option. It's still long enough to be disruptive, and I haven't found a way to disable the animation entirely.

![Slow desktop switching animation](/assets/images/macos-desktop-switching.gif)

> ヤバすぎ: There is a tiling window manager for macOS called [Yabai](https://github.com/asmvik/yabai). I haven't tried it. I noped out when it wanted me to "partially" disable System Integrity Protection to enable all its features.

## HammerSpoon

My solution is to use [HammerSpoon](https://www.hammerspoon.org) to set up a [bunch of custom keyboard shortcuts](https://github.com/downscore/.dotfiles/blob/main/.config/hammerspoon/init.lua) for resizing and switching windows. I don't use any virtual desktops, just normal windows scaled up to the maximum possible size. It completely eliminates the delay when switching apps:

![Fast window switching with HammerSpoon](/assets/images/hammerspoon-window-switching.gif)

Here are some example keyboard shortcuts:
- **Cmd-Ctrl-Z** - "Maximize" the current window by scaling it up to the full screen size
- **Cmd-Ctrl-B** - Switch to the browser
- **Cmd-Ctrl-T** - Switch to the terminal
- **Cmd-Ctrl-G** - Switch to Gmail

For that last shortcut, I have a [HammerSpoon script](https://github.com/downscore/.dotfiles/blob/main/.config/hammerspoon/browser.lua) that finds the active browser (Chrome or Safari), and uses some AppleScript to find the Gmail tab and switch to it.

I picked **Cmd-Ctrl** shortcuts because they are easy to press and don't conflict with much. Some potential conflicts:
- **Cmd-Ctrl-Q** - Built-in macOS shortcut to lock the screen
- **Cmd-Ctrl-F** - Toggle fullscreen in VS Code. Aside from this, VS Code doesn't have many keybindings of this form
- Some obscure Finder shortcuts use **Cmd-Ctrl**
- Some Google Meet shortcuts use **Cmd-Ctrl**

## The File System

I'm not a big fan of Finder in macOS. I strongly recommend using [yazi](https://yazi-rs.github.io) in the terminal instead. It has steep learning curve compared to mousing around a GUI file manager, but it's much faster and more powerful. It also requires a lot less configuring than other terminal-based file managers, like lf and ranger.

Using the keyboard for navigation is faster in general than using the mouse, but some tasks in particular are way faster. A couple examples:
- Copying a bunch of files from different directories and pasting them all into one directory. This is particularly easy to do in yazi.
- Bulk renaming: You can select the files you want to rename and it will give you a list of filenames to change in your favorite text editor.

Some other nice features:
- Integration with zoxide and fzf if you use those for directory navigation
- Image preview works out of the box if you have a terminal emulator that supports it, like [Ghostty](https://ghostty.org)

In fact, yazi works so well in its default config that, even though I use it daily, the [only customization I've made is](https://github.com/downscore/.dotfiles/blob/main/.config/yazi/yazi.toml) to show hidden files by default.
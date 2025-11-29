---
layout: post
title: "Keyboard Problems"
date: 2025-11-26
---

## Introduction

It's customary for articles about keyboards to begin with some information, usually incorrect, about historical typewriter layouts. Did you know that Qwerty actually began life as a meme layout? "QWERTY" was roughly the 19th-century equivalent of "LMAO". Imagine making the "LMAO layout" today, and you'll get the idea.

This article is about the biggest problems with computer keyboards, and my attempts to do something about them. It's very roughly ordered with the biggest problems coming first, and less consequential problems at the end. It doesn't deal at all with ergonomics and RSI, which are topics that deserve a much better treatment than they usually get.

I'm using a fancy keyboard (i.e. split ergonomic), but most of this can be applied to any keyboard. For example, if you're using a built-in MacBook keyboard, you can probably implement most of the features described here using [Kanata](https://github.com/jtroo/kanata). Having said that, using a fancy keyboard does make fixing problems a lot easier, especially the single biggest problem of all:

## Problem: The Backspace Key

For many people, the three most-used keyboard keys are [Space, Backspace, and E](https://daniel.haxx.se/blog/2015/08/19/one-year-and-6-76-million-key-presses-later/). From the home row position, you have around 3 dozen easily accessible keys, including Space and E. Backspace is not one of them.

So how big of a problem is this? For me, this is the thing that hurts the most about using a standard keyboard. Depending on how poorly I'm typing that day, up to 5% of my keypresses could involve taking my right hand off the home row, hitting Backspace, then moving back. It's hard to describe how disruptive this is to the flow of typing if you haven't tried something more civilized.

It's also hard to figure out how big of a problem this is because a lot of typing tests hide it. If you aren't forced to fix your mistakes in a typing test, then you don't really know how much the backspace key is slowing you down in real life, where you typically need to correct your typos.

### Solution: Thumb Cluster

![Kinesis Advantage 360]({{ '/assets/images/kinesis-advantage-360.png' | relative_url }})

_Image: [Kinesis Advantage 360](https://kinesis-ergo.com/keyboards/advantage360/)_

Any fancy keyboard worth its salt will have multiple keys available for each thumb, not just a single key (space bar) shared between both thumbs. The accessibility of these keys while you're typing at speed varies between keyboard designs, but the most important thing is that you have more than 0.5 keys available per thumb.

The very best fancy keyboards will give you 3 to 4 accessible keys per thumb. Note that this is different from the total number of keys in the thumb cluster: Many of them have 6 keys per thumb, but only 2 or 3 of them are actually *accessible* when you're typing quickly.

By far the best solution to the backspace problem is one that most fancy keyboards come with in their out-of-the-box configuration: Space on the most accessible right thumb key, and Backspace on the most accessible left thumb key.

### Solution: Split Space Bar

![Microsoft split space bar keyboard]({{ '/assets/images/microsoft-split-spacebar.png' | relative_url }})

_Time Magazine. [New Microsoft Keyboard Splits Space Bar, Left Side Used as Backspace Key](https://techland.time.com/2012/09/20/new-microsoft-keyboard-splits-space-bar-left-side-used-as-backspace-key/)_

In a distant second place, the next best solution is to split the space bar into two separate keys: Backspace for the left thumb, and space for the right thumb.

愚の骨頂: I've seen some people build mechanical keyboards with a split space bar and assign both halves to space. I get that they just wanted to split the key for aesthetic reasons, but this is just terrible.

### Solution: Remapping Keys

Imagine if you wiped all the labels off the keys of your keyboard and had to come up with a new layout from scratch. You'd have to be an absolute monster to choose to put the Backspace key way up in the top right corner. Fortunately, on most keyboards you can move keys around as you like and it mostly works. This solution is in third place because it sucks to various degrees depending on the hardware you have to work with.

Common to all hardware is the problem that if you move Backspace, you have to replace some other key with it. Since you want it to be an easily accessible key, you're probably going to have to swap it with some fairly commonly-used key like Command or Alt (putting it to the left of the space bar on Macs and PCs respectively). Or you could just swap it with Caps Lock, which is otherwise wasted space (see below).

If you have a keyboard with ZMK or QMK or some other programmable firmware, then you can easily perform the remapping just by flashing the firmware. If you want to remap your built-in laptop keyboard, you're going to have to do something that sucks a bit more, like using Karabiner Elements, Kanata, AutoHotkey, KMonad, or whatever works on your system. These programs are various degrees of finicky, and often require root access to set up.

### Solution: Improving Your Typing Accuracy

Just don't make any mistakes and the Backspace key won't be an issue anymore.

Improving your typing accuracy is a good thing to do no matter what, but it's not a real solution to this problem. Staying above 98% typing accuracy is difficult, and may not even be desirable. If I'm very careful, I can even keep my accuracy over 99%, but that's a lot slower overall than just allowing myself to make more mistakes and correct them as I go.

But say you did consistently type with high accuracy. If 2% of everything you type (or even just 1%) is a mistake, you're still using the Backspace key an awful lot, and it's probably still a good idea to make it more accessible.

And 2% is pretty far from where most people are. The average typist in [this German study](https://dl.acm.org/doi/fullHtml/10.1145/3626705.3627784) had an error rate of 11%.

### Vim?!

The worst thing about this problem is that not even Vim has a good solution. The insert mode equivalent to backspace is Ctrl-H and normal mode has Shift-X. Replacing the Backspace key with chords and mode switches doesn't really help.:wq

## Problem: Caps Lock

Which button do you press more often, Caps Lock or Enter? Which one is easier to press with your fingers in home position? Caps Lock sucks. There do exist humans who actually use Caps Lock, but not very many.

Caps Lock being useless doesn't actively make life worse, but it is a wasted key in very prime real estate. This key is easily reachable by the left hand pinky in home row position. Like the Quote key on the right hand side, it could be easily used while typing at speed, if only it did something remotely useful.

### Solution: Remap the Caps Lock Key

Since the key is so accessible, it makes sense to remap it to something you use often that otherwise requires leaving the home row position. Backspace is the most obvious candidate.

I guess this problem caught Apple's attention, because macOS has built-in support for remapping the Caps Lock key. You can remap it in the `Keyboard Shortcuts` settings screen:

![macOS Caps Lock settings]({{ '/assets/images/macos-caps-lock-settings.png' | relative_url }})

Unfortunately, you can't map it to Backspace here. Escape is a good option if you use Vim, otherwise Ctrl is a common choice.

If you're using custom firmware, or remapping software like Kanata, you have a lot more flexibility. Backspace is the most obvious thing to try. Another alternative is Escape on tap, Ctrl on hold, which gives you the best of both macOS-provided options. In ZMK this kind of mapping is called Hold-Tap, and in QMK it's called Tap-Hold. Obviously.

### Solution: Caps Word

This is not necessarily mutually exclusive with remapping Caps Lock, but Caps Word is an interesting feature that's definitely worth looking into, especially if you write computer codes with ANNOYING_IDENTIFIERS.

Caps Word is like Caps Lock that switches itself off after you press Space, Enter, Period, or whatever. You can configure it to remain on while you type underscores, for example, to make it really easy to type ANNOYING_IDENTIFIERS.

You can configure the feature to not terminate when you press Backspace so you can correct mistakes in your ANNOYING_IDENTIFIERS without having to reactivate Caps Word. It makes the whole thing flow much more smoothly.

I originally assigned my right Shift key to trigger Caps Word when tapped (as opposed to held), but I had a few too many false positives. More importantly, the false positives were pretty disruptive: I had to realize what had happened, terminate the Caps Word mode, then correct the mistake and start again. It ended up being worthwhile to move Caps Word to its own dedicated key in a less-accessible position.

Caps Word is supported out of the box in ZMK and QMK. It should be possible to set up in software like Kanata.

### Vim??

Using tilde (`~`) in visual mode is pretty cool. It's like an after-the-fact caps lock. `gU`also gives you some similar options for capitalizing stuff.

## Problem: Modifier Keys

The four most commonly-used modifier keys on your keyboard are: Control, Command, GUI, Windows, Meta, Alt, Option, and Shift.

Control and Shift are common across all keyboards you're likely to encounter. The others differ based on operating system, or whether or not you're looking at configuration files in the languages of the ancients. Here's how they are grouped.

> Option Group
> - **Alt** - PC
> - **Option** - Mac
> - **Meta** - Ancients

> Command Group
> - **Windows** - PC
> - **GUI** - PC (Non-Windows)
> - **Command** - Mac

So what's the problem with modifier keys, besides the confusing names? The main one is that they are awkward to press and require moving away from home row. There's also no nice layout for them that works well across operating systems.

Note: The Function/Globe key on Mac keyboards is silly in its own, less important, way and gets a dedicated section far below.

Remapping keys can only take you so far. On a standard keyboard, if you're lucky, your thumbs can comfortably reach the keys directly adjacent to the space bar. There are just not enough easily-accessible keys available to get a good mapping for modifiers.

### Solution: Home Row Mods

My favourite partial solution to this problem is using Home Row Mods - where the letters on the home row act as modifier keys when they are held down. For example, holding down S can be the same as holding Control.

Home Row Mods involve a serious trade off. On the one hand they are very fiddly, requiring a lot of tuning and customization, especially as you start to type faster. On the other hand, once you have them locked in, you'll never want to use a keyboard that doesn't have them. Within a day of trying Home Row Mods for the first time, I was pretty sure I was never going back.

Why do I call this a "partial" solution to the problem? Mostly because I couldn't get the Shift key mod working well enough. Shift is the main modifier used when typing at speed, and no matter how I configured it, I always had too many false positive or false negative triggers. I'm apparently not the only one to run into this:

> [urob's zmk-config](https://github.com/urob/zmk-config)
> 
> ...this setup works best in combination with a dedicated shift for capitalization during normal typing (I like sticky-shift on a home-thumb). This is because shifting alphas is the one scenario where pressing a mod may conflict with `require-prior-idle-ms`, which may result in false negatives for fast typers.

The rest of the modifiers have given me absolutely no trouble since I landed on a good configuration. I can type at full speed and never have unexpected activations.

Another disadvantage of Home Row Mods is that modding a key causes its letter to be emitted on key up, rather than on key down. This can make typing feel a little sluggish or uneven, as some letters show up as soon as you press the key, while others only show up after you release it.

Configuring Home Row Mods is a big topic on its own. Here are some links:
- [Sunaku: Taming home row mods with bilateral combinations](https://sunaku.github.io/home-row-mods.html) - A very good overview of Home Row Mods and how to deal with common problems. An insane amount of `#define`'s in his config file.
- [urob's zmk-config](https://github.com/urob/zmk-config) - A pretty intense configuration for very small fancy keyboards.
- [My ZMK Config](https://github.com/downscore/glove80-zmk-config/blob/f1ab892c1a08f5d6eb23a2d2050d853f98e0a571/config/glove80.keymap#L143) - Doesn't explain what Home Row Mods are, but it's a reasonably simple working example of how to set them up in ZMK.

### Solution: Thumb Cluster

Putting the modifiers on the thumb cluster of a fancy keyboard could make them more easily accessible. In practice, I only ever use the Shift button this way. I have a dedicated Shift key for each thumb, which I've found much easier to work with than stretching my pinkies to hit Shift where it lives on normal keyboards.

### Meh and Hyper Keys

You might have heard of the stupid-sounding Meh and Hyper keys:
- **Meh**: Ctrl+Option+Shift
- **Hyper**: Ctrl+Alt+Shift+Command

A common usage of these is to bind one to a single key via custom firmware or remapping software and use it to set up some custom shortcuts. E.g.:
- **Hyper+B** to switch to the browser.
- **Hyper+T** to switch to the terminal.

I've found it easier to use key combinations that are easy to press on any keyboard, but are for the most part unused by any existing software. E.g.:
- **Cmd+Ctrl+B** to switch to the browser.
- **Cmd+Ctrl+T** to switch to the terminal.
In combination with Home Row Mods, these allow me to quickly change windows without leaving home position.

If you do use Hyper, there are a couple of things to be aware of:
- In Windows, the Hyper key will launch an advertisement for Office. Because why wouldn't it?
- In macOS, some combinations, such as Hyper+Comma and Hyper+Period, will run built-in diagnostic tools.

## Problem: Symbols

If you're a programmer, which do you type more often: the open parenthesis (, or the digit 9? [Here's an analysis by Xah Lee](http://xahlee.info/comp/computer_language_char_distribution.html) in which open parentheses occurred around 37 times more often in code than the digit 9. The open parenthesis is way more common, but it needs a modifier key (Shift). Incidentally, it also usually requires you to leave home position.

In fact, quite a few symbols need you to leave home position, which means there is room for improvement in how efficiently they can be typed.

### Solution: Symbol Layer

When you hold down Shift, the letter keys produce capital letters. How about a key where if you hold it down, the letter keys now produce symbols? If you can hold down that key in home position, then you can potentially type any symbol without ever leaving home position.

This is pretty much how I solved this problem. I assigned a letter on each half of the keyboard to activating the symbol layer. When I hold down either W or O, any other letter I type now produces a symbol. The implementation was pretty much the exact same as with Home Row Mods (see above), though the triggering ended up being a bit more sensitive.

The main drawback of this approach is having to learn a new layout for the symbol layer. I made it easier on myself by making it as symmetrical as possible. For example, an open parenthesis is the F key, and the closing parenthesis is J, which mirrors F on the right side of the keyboard.

The main advantage of this approach is that you don't "break" any of the existing symbols. If I want to press Shift+9, I can still do that.

The triggering of my symbol layer is a bit different than that of my other Home Row Mods, because I often use it while typing quickly. To avoid a large number of false negatives, where I would just type two letters instead of the symbol I wanted, I had to make it trigger faster and accept a small false positive rate. Every once in a while, I get a symbol instead of the two letters I wanted. Fortunately, it doesn't happen often enough to be a problem.

If you want to try this, the best advice I can give you is to not make any mistakes on your first attempt. If you do make mistakes, recognize and fix them as soon as possible so you don't invest too much in muscle memory for a layout that's going to change. In particular, one thing you'll want to do is make sure that common symbol bigrams, such as `!=` and `()`, are easy to type.

### Solution: Invert the Number Row

I haven't tried this myself, but an idea that seems reasonable to me is to invert the behaviour of the number row keys so that they type symbols without pressing Shift. E.g. just pressing the 9 key types an open parenthesis, and you need to press Shift+9 to get the digit.

One possible problem is this could interfere with some keyboard shortcuts, like Cmd+1 to switch to the first tab in a browser.

### Prose Symbols

The most common symbols in English prose are periods, commas, apostrophes, question marks, and double quotes. For the most part, these symbols are are reachable from home position on a Qwerty keyboard while typing quickly. I'd recommend leaving them as-is, and using a symbol layer for brackets and things. I originally tried using a symbol layer for apostrophes and found it slower and less accurate than just using the right pinky.

## Problem: Numbers

The number keys are just high enough that you can't comfortably type them without leaving home position. Many keyboards also don't have a dedicated numpad.

How big of a problem is this? Not very, unless you type an unusually large number of numbers. We're already pretty far down in the list of problems, after all.

### Solution: Momentary Numpad

One potential improvement for typing numbers is to add a new keyboard layer that turns some letters into a numpad, and have a way of triggering it without leaving home position.

In my case, I have a key in the left thumb cluster that turns the letters on the right side of the keyboard into a numpad. It's pretty easy to trigger while typing at speed, and I find it a lot easier to be accurate with a numpad-like layout than the number row at the top of the keyboard.

## Problem: The Qwerty Layout

This isn't *really* a problem. Qwerty isn't optimal, but it's fine. You've probably already sunk a lot of time into learning Qwerty, so just go with it. The other keyboard problems addressed here provide so much more headroom for improvement, with so much less effort required.

嘘: Did you know the Chinese character for "suboptimal" also means "opportunity"?

You can take advantage of some of the weirdness of Qwerty to make some modded keys or chords that are very easy to press, but don't really interfere with normal typing. For example: J+K is extremely easy to press, but "jk" and "kj" are not common English bigrams.

### Solution: Stenography

Alternative layouts are a half-measure between staying with Qwerty and learning stenography. It takes a lot of effort to learn a new keyboard layout, and you might get a small speed boost. It takes a ton of effort to learn stenography, and you'll definitely get a huge speed boost: many stenographers can type at over 300 wpm.

I haven't tried stenography myself, so I'll try to stick to a few simple (hopefully accurate) points here:
- It doesn't require custom hardware. You can use software like [Plover](https://www.openstenoproject.org/plover/) to make your current keyboard more stennish, as long as the keyboard supports N-Key Rollover (NKRO).
- Custom hardware does help, as dedicated steno keyboards tend to have a better design for the type of input you have to do - e.g. mashing two adjacent keys with one finger.
- There are a billion different steno "dictionaries" mapping input patterns to words, and people who use off-the-shelf dictionaries tend to customize them at least a little bit.
-  There are keyboards, like the [Jarne Ultimate Keyboard](https://shop.chenonetta.com/product/jarne-the-ultimate-keyboard/), that have a full steno engine onboard. Most fancy keyboards aren't capable of this as they tend to not have enough megachips of memory.
- As a friend with experience in stenography points out: stenography is far from figured out for coding (let alone driving a computer!).

### Vim:s/?/!/g

If you use Vim you might have some extra reasons to not want to use an alternate layout. You probably use Vim plugins in other software. I'm using one right now. Maybe you can remap keys easily in Vim or Neovim itself, but how about all those half-baked plugins? Any layout that scrambles H/J/K/L is probably going to cause you a lot of trouble.

## Problem: Arrow Keys

On most keyboards, the arrow keys are pretty far out of the way. They're completely impossible to press without leaving home position.

### Solution: Vim!!

If you use Vim, you already know the solution here: use H/J/K/L in normal mode. If you've developed this habit, there is a potential solution for non-Vimmy software:

### Solution: Navigation Layer

I haven't tried this myself, but you could add a keyboard layer where H/J/K/L actually become the arrow keys. If you can trigger the layer with your left hand in home position, then you can navigate without ever leaving home position.

[Here's a good blog post on the topic](https://tonsky.me/blog/cursor-keys/).

I haven't tried this because I use the next solution:

### Solution: Accessible Arrow Keys

On a very few keyboards, the arrow keys are just really easy to access without moving your hands much. The [Kinesis Advantage](https://kinesis-ergo.com/shop/adv360/) line of keyboards is like this, and so is the [MoErgo glove80](https://www.moergo.com). If you have one of these keyboards, then this isn't really a problem at all.

## Problem: Deleting Words

How often do you tap Backspace more than once in a row? Pretty often, right? A lot of the time it would be faster to just delete the whole word and type it out again. Doing so may also help build faster typing habits, as you can "chunk" typing whole words in your muscle memory, rather than editing arbitrary suffixes.

So the solution is Option+Backspace. But that's pretty awkward to press, especially when you are typing quickly. There's got to be a better way.

### Solution: Delete Word Key

I think if keyboards were humanely designed from the get-go, they'd probably all have a dedicated Delete Word key somewhere reasonably accessible. This is exactly what I added to my own keyboard, and I use it a lot.

I have a single key on my keyboard that emits Option+Backspace when pressed. If I make a typo in English prose, I tend to use that key instead of my extremely-accessible Backspace key. It makes me slightly more efficient overall. I don't use it much at all when writing computer codes.

If you have already made the Backspace key more accessible than it is on a standard keyboard, there's less room to improve efficiency with a Delete Word key. It still helps a bit, though.

## Problem: Latency

By "latency" here, I mean the delay between you starting to move your finger, and the character appearing onscreen.

It includes all of the following, serially:
- Time for the key to actuate.
- Time for the keyboard controller to transmit the pressed key over USB.
- Time for the OS to receive the signal and route it to the current application.
- Time for the current application to update its state and redraw.
- Time for the monitor to refresh.

So what can you expect the total latency to be, and what are the relative contributions of each step? It super depends. A terrible keyboard could completely dominate the latency with a long actuation and transmission time. A terrible application could dominate the latency by taking way too long to redraw.

In general, I'd expect total latency to stay well under 100ms if there's no terrible hardware or software involved.

The more important question is: How much does it matter? I honestly have no idea, but it matters at least a little bit. See, for example, [this study from Germany](https://dl.acm.org/doi/fullHtml/10.1145/3626705.3627784), which found that latency affected performance in correcting text that contained a bunch of "error characters." In this case, the latency in question was 200ms, which is pretty high.

### Solution: Not Really Worrying About It

I buy the argument that you need to be able to see a mistake before you can correct it, so latency can slow you down when Backspacing is involved. I also find it completely plausible that noisy, uneven latency, like that introduced by Home Row Mods or a bad wireless connection, is more disruptive than steady, constant latency. I just haven't found it to be very important in practice.

As a counterpoint, consider the humans of stenography. They type unbelievably fast, but with highly variable and choppy latency. Since this uneven delay doesn't seem to slow them down in the slightest, I just don't worry about it when I'm typing.

I've tried experimenting with disabling the Home Row Mods on my keyboard so that all letters are always emitted on key down, and I haven't found any difference. Subjectively, my typing speed feels the same, and objectively, my typing test scores don't seem to change.

### Solution: Worrying About It

This is mutually exclusive with the above solution.

If you play video games or otherwise worry more about latency than I do, check out [Dan Luu's article on Keyboard Latency](https://danluu.com/keyboard-latency/).

Another very good article on the topic is [Typing With Pleasure by Pavel Fatin](https://pavelfatin.com/typing-with-pleasure/).

## Problem: Wireless

What passes as a best-in-class, "rock solid" Bluetooth implementation in the world of wireless keyboards is unacceptably awful in the world of "I just want to do my work." Wireless keyboards will always find new and exciting ways to keep you from getting things done.

My keyboard can be connected to a computer with a cable, but it has two separate sides that can only communicate with each other over Bluetooth LE. This is, by a very wide margin, the worst thing about my keyboard.

So what's the problem with the keyboard sides communicating with Bluetooth? The main problem is that Bluetooth always sucks. The keyboard has significant difficulty in poor RF environments, where communications can be delayed by hundreds of milliseconds. When this happens, the keyboard is extremely hard to use and there's no easy way to fix it.

### Solution: Wires

Wireless communication itself isn't always bad. A noisy channel between your computer and the internet is just fine. Your computer has all sorts of tricks to deal with lost or corrupted data. Your brain, on the other hand, doesn't handle it nearly as well. So keep the channel between you and your computer as pristine as possible. Ensconce yourself in wires.

## Problem: MacOS Globe Key

The Globe key on Mac keyboards can be used to change the input language, and is also used in some built-in keyboard shortcuts, especially in more recent versions of macOS. Unfortunately, the key uses some weird proprietary magic that can't be easily replicated in [custom firmwares like ZMK](https://github.com/zmkfirmware/zmk/issues/947) and QMK.

ZMK does include a predefined keycode for the Globe key, but it doesn't work for changing the input language. I'm not sure if it works with keyboard shortcuts including the Globe key because I don't use any of them.

There are lot of workarounds for this problem of varying degrees of hackiness, but I just gave up and went with:

### Solution: Custom Shortcut for Changing Languages

I assigned Ctrl+Option+Space to change the current language:

![macOS language input settings]({{ '/assets/images/macos-language-settings.png' | relative_url }})

It's very easy to hit on my keyboard with home row mods, and still pretty easy to hit on a built-in MacBook keyboard.

## Appendix: Mental Effort

For a while, I was controlling my computer and writing both prose and computer codes entirely by voice. Replacing a keyboard and mouse with voice alone requires using a pretty complicated grammar and chaining together a lot of commands at once. It takes a large amount of mental effort - I would spend a second or two staring off into space, having a spinning beach ball moment before issuing a long chain of commands. The experience made me more sensitive to how much mental effort is required to use a keyboard: not nearly as much as with voice, but still quite a bit. This is true even if you are a fast typist, or feel like typing is second nature to you.

Dan Luu has the best description of this I've found:
> [Some reasons to work on productivity and velocity](https://danluu.com/productivity-velocity/)
> 
> With a measured typing speed of 110 WPM, that might sound like I spend a small fraction of my time typing, but it turns out it's roughly half the time. If I look at my writing speed, it's much slower than my typing test speed and it seems that it's perhaps half the rate. If I look at where the actual time goes, roughly half of it goes to typing and half goes to thinking, semi-serially, which creates long pauses in my typing.
>
> If I look at where the biggest win here could come, it would be from thinking and typing in parallel, which is something I'd try to achieve by practicing typing more, not less. But even without being able to do that, and with above average typing speed, I still spend half of my time typing!

Probably the most important term he used was "semi-serially". Thinking or typing - you're "semi" doing one or the other, usually not both at the same time.

This implies that time spent typing is at least "semi" in the critical path of getting work done, which means *any* improvement in typing speed boosts productivity. You don't hit the ceiling until you're typing at ∞ wpm. It's not even clear to me where diminishing returns kicks in: Typing 300 wpm like a cold-blooded stenographer just seems like a really useful ability to have.

## Appendix: Further Optimizations

### Commas

One keyboard optimization I stopped short of trying out is having the Comma key emit a comma and a space. Commas are almost always followed by spaces, and in the rare event they're not, I find myself typing Comma, Space, Backspace. I didn't try this one out because it seemed like it would break a bunch of stuff (e.g. Command+Comma to open settings on macOS) without providing a huge benefit.

### Open Parentheses

A dedicated open parenthesis key seems like a reasonable idea for people who write computer codes. I haven't tried it yet because I'm not sure where the best place to put it on my keyboard would be, and my symbol layer lets me type parentheses pretty efficiently.

I know some people have their Shift keys emit parentheses when tapped, but I've been thoroughly scared away from messing with my Shift buttons after my experiments with Home Row Mods and Caps Word.

### Chords

Some key combinations, like J+K, are very easy to press, but the individual characters are almost never encountered together - the bigrams "jk" and "kj" don't appear very often in English text. This means you could potentially trigger some special functionality when the keys are pressed together, and you wouldn't interfere with normal typing.

I imagine the downsides of Chords are similar to those of Home Row Mods. For example, chorded keys wouldn't be able to emit characters until they were released.

I don't currently have a use for Chords, but if I ever ran out of space on my Symbol Layer, I'd probably give them a shot.

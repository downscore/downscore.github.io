---
title: "It's So Over"
date: 2025-12-31
---

Andrej Karpathy recently [posted a sequence of tokens](https://x.com/karpathy/status/2004607146781278521) that accurately captures my current mood:

>I've never felt this much behind as a programmer. The profession is being dramatically refactored as the bits contributed by the programmer are increasingly sparse and between. I have a sense that I could be 10X more powerful if I just properly string together what has become available over the last ~year and a failure to claim the boost feels decidedly like skill issue.
>
>There's a new programmable layer of abstraction to master (in addition to the usual layers below) involving agents, subagents, their prompts, contexts, memory, modes, permissions, tools, plugins, skills, hooks, MCP, LSP, slash commands, workflows, IDE integrations, and a need to build an all-encompassing mental model for strengths and pitfalls of fundamentally stochastic, fallible, unintelligible and changing entities suddenly intermingled with what used to be good old fashioned engineering.
>
>Clearly some powerful alien tool was handed around except it comes with no manual and everyone has to figure out how to hold it and operate it, while the resulting magnitude 9 earthquake is rocking the profession. Roll up your sleeves to not fall behind.

_(lightly formatted by me)_

The list he gives of scaffolding features is interesting, and I'm going to dig into them in future posts. Eliciting capabilities from AI models through scaffolding is going to be a running theme.

## Hand Coding is So Over

In my [previous post on AI productivity](https://downscore.github.io/2025/12/05/ai-productivity/), I introduced my "Hello, World" project in Go, which was a rough clone of Subspace:

![Spaceship Game](https://downscore.github.io/assets/images/subspace-hello-world.gif)

I decided to use this codebase for a silly proof of concept: That I technically never have to write another line of code by hand if I don't want to.

I asked Claude Code to make an extremely small change:

![Claude Code camera offset request](/assets/images/claude-code-camera-offset-request.png)

This is silly for two reasons:
- It would have been way faster for me to make that edit by hand than to describe it the way I did.
- The edit moves the camera off the player's spaceship and makes the game unplayable.

I wanted to see if I could make this a bit less silly, so I added the following instructions to CLAUDE.md:

> If asked to directly make an edit to a piece of code, please first consider the implications of the change. Confirm with the user if you think it might have unintended consequences.

Then I re-ran my request:

![Claude Code camera offset warning](/assets/images/claude-code-camera-offset-warning.png)

Claude Code correctly recognizes that this is a dumb change to make and asks for confirmation. To make sure it doesn't just ask for confirmation no matter what, I asked it to make a more reasonable edit in the same place:

![Claude Code camera offset approved](/assets/images/claude-code-camera-offset-approved.png)

This edit just nudges the camera a bit, and might be a reasonable thing to do if there is some GUI chrome on the side of the screen or something. Claude just goes ahead and produces the diff without asking for confirmation.

Of course, you still probably wouldn't use Codex or Claude Code for tiny edits like this in practice, but you can always ask for larger scale changes or batch together a bunch of small changes.

In my [previous post on AI productivity](https://downscore.github.io/2025/12/05/ai-productivity/), I talked about speed/quality tradeoffs in your iteration loop while developing software. Having AI double-check your work for mistakes inside your iteration loop seems like a potentially big win for quality, without sacrificing much speed if you're already relying on AI tools.

We can contrast this with another reasonable workflow where you do a bunch of hand-coding then ask the AI to check your work when it's done. If you're not working on some monster C++ or Rust project where you have to wait multiple minutes for even an incremental compile to finish[^1], then you probably have a pretty fast iteration speed. Unfortunately, you're not going to accomplish very much each iteration with only a single human intelligence bottlenecked by human code-typing-speed[^2]. When you tally up the amount of work you get done in a day, you're going to end up way behind where you could have been with an all-AI workflow, and you'll probably have missed a bunch of mistakes to boot.

The above rests pretty heavily on the assumption that AI can actually write the code you need. But come on, it's _late_ 2025, not _early_ 2025: If there's some code AI can't write for you yet, it's most likely a scaffolding problem. I can imagine some niche problems (e.g. extremely high-performance assembly language for some weird new architecture) where AI probably can't do the whole job, but I can't think of anything where current models wouldn't be _extremely helpful_.

[^1]: God help you if you're a software engineer at Adobe waiting for Photoshop to start up every time you make a change.
[^2]: I have a theory that code typing speed matters far more than people think for traditional software development, and it tends to be a _lot_ slower than prose typing speeds. I was planning on running some experiments and making a post about this, but it seems a lot less important if I'm not going to be typing much code anymore. It'll probably keep sitting on my giant pile of "things I believe about the world but haven't confirmed yet."

## Ramping Up is So Over

The above was a bit of a toy example, so I decided to do something real next: add a feature to [Ghostty](https://ghostty.org), the terminal emulator I use daily.

Here's what Claude said after getting Ghostty's repository cloned and built:

```
Ghostty launched.

  Build summary:
  - Upgraded Zig: 0.14.1 → 0.15.2
  - Installed Metal Toolchain (704 MB download)
  - Ran Xcode first launch setup
  - Cleaned extended attributes that blocked code signing
  - Full build time: ~3-4 minutes after setup

  The build worked, though it required some environment fixes. Claude Code was able to diagnose and resolve each issue (Zig version mismatch, missing Metal toolchain, xattr issues) by reading error messages and applying appropriate fixes.
```

The most remarkable part here is that the build involved what I call a Yak-shaving Stack (or YakStack) of three layers:
- Try to build the project (after upgrading Zig)
- Get an error about missing Metal 🤘
- When trying to fix Metal, get an error about "Xcode first launch" whatever

To unwind the stack, you need to do the Xcode first launch thing, then install Metal, then re-run the build. It may not sound like much, but it's easy for a human mind to get lost in a YakStack of only three levels, especially of any of the installs take longer than a few minutes.

At this point, I have Ghostty built from source and running. It's already hard to describe just how much psychic damage Claude has prevented me from taking. The macOS code signing stuff on its own would have been a critical hit.

Next, I knew the feature I wanted to add: fuzzy matching with more commands in the Ghostty command palette. I asked Claude to come up with a plan for implementing it. The first draft at plan looked good, so I let it loose. The feature worked, but I had to do a bit of iteration to remove duplicate commands, etc. Here's what the result looked like:

![Ghostty command palette](/assets/images/ghostty-command-palette.png)

As far as I can tell, the feature works exactly as intended, and has some decent test coverage. However, this isn't really ready to be sent as a pull request: I haven't tested it across a wide enough set of scenarios, and I haven't carefully read and reviewed the code myself. It's still amazing to me that I could have something implemented and working on a reasonably large, completely unfamiliar codebase in such a short amount of time.

It's worth mentioning that Ghostty might be an AI-friendly project. I asked Claude Code if we should create a CLAUDE.md including its current understanding of the project, and it said it's "probably not worth it, " due to the already-present AGENTS.md and HACKING.md files.

### Understanding AI Models Is So Over
_北斗の何だ_

At the beginning of December, Neel "North Star" Nanda et al [north-starred a post on the AI Alignment Forum](https://www.alignmentforum.org/posts/StENzDcD3kpfGJssR/a-pragmatic-vision-for-interpretability) describing their new north star of pragmatic interpretability, and effectively giving up on "ambitious reverse engineering" (deeply understanding the models).

It's a big change of tone from when Sparse Autoencoders were first discovered, and some people (notably not any of the interpretability researchers themselves) apparently decided we were well on our way to understanding everything there is to know about Transformer-based models. I reckon we can say we deeply understand the models when we, at least in principle, know how to build one without resorting to blind optimization over a crazy-dimensional loss function.

In any case, a frontier lab interpretability research team publicly giving up on deep understanding of LLMs to focus on safely shepherding in AGI seems like a pretty big deal. I'm not sure exactly what to take away from that, except that they don't seem to expect improvements to model capabilities to taper off any time soon.

Side note: There are a lot of uncharitable ways you could read the Alignment Forum post, but three things are clear:
- It's full of really good advice on research taste from really smart people working on a really hard problem.
- A lot of the less-charitable motivations for the pivot completely evaporate if the authors really do believe AGI is arriving pretty soon.
- Google DeepMind's interpretability north stars are being aligned by north-star-hill-climbing on north stars across critical user journey north stars.

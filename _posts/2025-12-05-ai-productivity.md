---
title: "AI Productivity"
date: 2025-12-05
---

I have experience writing software. I have been the guy trying to write high-performance SIMD code and being horrified by what the LLM came up with.

In one particularly bad case, after fixing the obvious errors, I noticed the subtle bugs that were slowing the code down to 1/16th speed. I decided that AI assistance wasn't actually saving me any time, and I didn't want to be constantly vigilant for subtle bugs that I hadn't handcrafted myself. I stopped using chatbots for code generation and started toggling AI-generated completions on and off depending on what kind of code I was writing.

But AI years are dog years, and that was more than a decade ago. Let's see if things have progressed at all.

Two important questions I want to answer:
- Has AI progressed to the point where it undeniably offers a huge productivity boost to coding, or does it seem like it will soon?
- If so, do I actually enjoy the new way of coding? Put another way, do I see a place for myself in the new world where AI does most of the work?

## TL;DR: Things Have Progressed, People Are Confused

Here are my conclusions up front:
- Yes, AI already offers a huge productivity boost -- much bigger than I would have guessed. However, capabilities are jagged and it takes some scaffolding work to realize the biggest gains, which is maybe why most people haven't picked up on this yet.
- Yeah, I think I do enjoy it. It doesn't seem like a bad way to work, and I'll never have to manually refactor C++ code again. My own experience level still seems relevant when working on large codebases or complicated problems

I've been using Claude Code for a while now, first with Sonnet 4.5, and more recently with Opus 4.5. Planning mode is overpowered, and a bit of prompting can turn Claude into a savage critic you can bounce ideas off. If you take nothing else away from this post, take this:

> You really should try Claude Code with Opus 4.5 and experiment with planning mode and the other scaffolding features Claude Code offers. You will be surprised at how effective it all is.

## On-Ramps

AI takes care of on-ramps. There's no friction to trying new things anymore. I think it's really easy to underestimate the importance of this. Even a little bit of friction has historically been enough to keep me from trying things. It took me quite a while to work up enough energy to finally try [rustlings](https://rustlings.rust-lang.org) for the first time.

If I want to try a new language now, I don't write "Hello World" or find the rustlings equivalent. I write a clone of [Subspace](https://store.steampowered.com/app/352700/Subspace_Continuum/). It takes about 10 minutes to do.

![Subspace clone hello world](/assets/images/subspace-hello-world.gif)

Pictured above: "Hello, World" in Go.

This all has a fractal effect. It removes the friction for getting started at every level:
- It removes friction for getting started tracking down a bug. I just ask for a plan to find the source of the bad behavior I'm seeing.
- It removes friction for adding a new feature to an existing codebase, I just ask the LLM which areas need to change.
- It removes friction for starting a new project - the LLM starts the project.
- It removes friction for learning how to code. I can ask the LLM to teach me, and to a surprising extent, I don't even need to touch the code myself anymore.

Keep in mind, this is all about _getting started_, not doing the whole job. In these cases, the LLM isn't necessarily fixing the bug itself, it's just telling me the best place to start.

## Doing the Whole Job

What about working on a large, existing project, like just about every software engineer does just about all of the time?

I found these posts that inspired me to give Claude Code a proper try for myself:
- [How I Became a 5x Engineer with Claude Code](https://www.lesswrong.com/posts/pcFSo5hEzzGTZEXEd/how-i-became-a-5x-engineer-with-claude-code)
- [Claude Code is a Beast – Tips from 6 Months of Hardcore Use](https://www.reddit.com/r/ClaudeAI/comments/1oivjvm/claude_code_is_a_beast_tips_from_6_months_of/)

I mean, if "5x" isn't complete hyperbole, then the nature of software engineering is about to change really quickly, and really significantly. This is true even if for some reason models don't get any more capable than they currently are. It's also worth remembering that both of these articles predate the release of Claude Opus 4.5, which I have found to be a really significant upgrade.

Though they don't use the term directly, both of these posts talk a lot about scaffolding. In particular, they both emphasize the importance of planning mode in Claude Code. They're right to.

## Planning Mode

Planning mode starts off with your initial vague description of what you want to accomplish, then goes off and scours your codebase. When it's done, it comes back to you with a few questions to clear up the biggest ambiguities in your request. It then presents the plan, and you can ask for changes or just go with it.

As a simple example, I asked a new instance of Claude Code (with no memory of the game) to improve the enemy AI in my Subspace clone:
![Planning mode request](/assets/images/planning-mode-request.png)

Note that I'm implicitly asking for the enemies to coordinate with each other. There's nothing like that currently in the game.

It scrambled through the codebase and came back with some questions:
![Planning mode questions](/assets/images/planning-mode-questions.png)

I asked it to improve the enemies in all the ways, and make lots of always-visible debug-style visualizations of what they are thinking.

The questions aren't always good. Sometimes they're not coherent with what you're trying to do, or the AI has clearly otherwise gone down a bad path. In these cases, each individual question has a free-form "Type something" option you can use to explain this, or you can Esc out of the questions entirely and explain how the model should approach the task differently.

Finally, Claude came back with a giant implementation plan and summarized the whole thing at the bottom:
![Planning mode summary](/assets/images/planning-mode-summary.png)

This is where planning mode becomes incredibly powerful. You can review the whole implementation plan (there are several pages above what I've screenshotted here), and it goes into very specific detail about what Claude intends to do. You can question, challenge, or ask for modifications to any part of the plan, and it works incredibly well.

In this case, I didn't really have any strong opinions (I guess 600px is a good threshold for making friends?), or frankly any familiarity with the code, so I just went ahead and implemented the plan as-is. It took a few minutes to do the whole thing, and this is the result:

![Subspace enemy AI](/assets/images/subspace-enemy-ai.gif)

Pictured: "Hello, World" in Go, except now spaceships team up to shoot you.

In my experience on more serious work, after you give some good feedback, Claude's second attempt at a plan is almost always way better than its first. If you didn't use planning mode and just tried to one-shot a bugfix or new feature, you'd be just YOLO-ing the first plan and trying to clean up the mess later. I wouldn't be surprised if almost everybody is effectively doing this and therefore significantly underestimating the capabilities of current models.

The most impressive part is how _coherent_ these plans are: The model says it's going to do a ton of different stuff, does it all just like it said, and everything ends up working as planned. When it runs into errors, it can usually find a way around them in the way 2024 models couldn't. It's really rare for me that Opus 4.5 goes completely off the rails, even when it's doing a huge amount of work in one go.

## Human Experience and Skill Level

So how much does the software engineering experience level of the nominally-in-charge human matter? Still quite a lot, I think. Being able to give the right feedback on Claude Code's plans seems to be really important, and that still requires a good understanding of the problem you're trying to solve and the codebase you're working on.

I can see this fraying around the edges a bit, though. Knowing multiple topological sorting algorithms is probably a lot less valuable this year than it was a couple years ago. And if the model sees you've written a bubble-sort or equivalent, it's probably just going to fix it for you next time it modifies that code.

In very niche things that almost no human does, like "writing code that doesn't perform horribly," you can probably maintain an edge over AI models for a while longer, but it looks a lot like there is some writing on some walls.

## METR Sends Mixed Signals

METR (❤️) conducted an [RCT in July](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/) to see how much more productive AI assistance made 16 "experienced open-source developers." The conclusion was that AI made the developers 19% slower. That went against the expectations of everyone involved, including the developers themselves (both before and after!):
![METR RCT expectations](/assets/images/metr-rct-expectations.png)

METR also has their famous ["doomsday count-up" eval](https://evaluations.metr.org/gpt-5-1-codex-max-report/#details-of-time-horizon), showing models becoming exponentially better (log scale y-axis) at doing complex software engineering tasks:
![METR task complexity](/assets/images/metr-task-complexity.png)
For each model, it shows the $LD_{50}$ task complexity measured in human time.

Taken together, these results say that LLMs on their own can do tasks that take humans hours, but they still slow us down. It's hard to reconcile the two.

I think the real explanation is that the participants in the RCT suffered from the extremely rare "double-skill issue":
- Too much skill: The developers had "typically over a decade of experience" with software engineering and they were very familiar with their codebases (average of 5 years experience with their projects). They're about as far away as you can get from a developer on their first day at a new company.
- Too little skill: The devs were made to use Cursor, but only 7 of them (44% of the total) had any experience at all with Cursor. The paper did find a "similar slowdown for developers with prior Cursor experience", but I can't imagine this wasn't a huge factor.

From the "Extended Discussion" section of the RCT: "We do _not_ provide evidence that AI systems do not currently speed up many or most software developers \[or that\] developers with much more experience using AI systems wouldn't see speedup".

I don't want to give the wrong impression of the study, it's extremely well done, and I don't think they misrepresent their findings at all -- it's just too easy to take this fairly narrow result and try to interpret it as applying to all developers using AI assistance. What I really want is a study where developers who are very used to commanding armies of agents in Claude Code attack codebases they have varying levels of familiarity with.

## Google Leverages Hill-Climbing on their North Star to Productize an RCT

Google, recognizing the importance of deep-diving on 10x initiatives, also [executed an RCT](https://arxiv.org/html/2410.12944v2#S3) to help align resources across organizational boundaries in AI efficiency-gain problem spaces.

This RCT is a bit older (Oct 2024). The sample was 96 full-time Google software engineers, and they found that AI shortened time on task by 21%. This finding lines up with my prior beliefs, so [I encourage everyone to interpret it extremely broadly and apply it to all developers using AI assistance](https://en.wikipedia.org/wiki/Affect_heuristic).

The AI tools in this case were all internal, but described as providing similar features to Cursor (with the possible exception of "[Smart Paste](https://arxiv.org/html/2410.12944v2#S3)").

One of the biggest differences from the METR RCT is the tasks the developers did. In the Google study, the tasks were standardized and in C++. METR used actual GitHub issues in presumably a number of different programming languages (the paper doesn't make this clear). I suspect this affected the outcome of the studies quite a bit, mostly because of iteration speed and quality differences between programming languages.

## Iteration Speed and Quality

An "iteration" here refers to planning and making a change to the code, and then verifying the results of that change. Sometimes people apply the term "[OODA Loop](https://en.wikipedia.org/wiki/OODA_loop)" to this process. It includes planning, writing code, compiling, and running/debugging.

Iteration speed is obviously important. The faster you can do things, the more things you can do. But quality is also important: if you always get everything right on the first try, you don't need extra iterations to fix things.

So there's an obvious trade-off: If you lower your iteration speed, but get a lot more high-quality work done per iteration, you can move faster overall. I think this is exactly the trade-off we need to make to get the most out of the currently-available AI tools.

## C++

C++, with its long compile times, thoroughly-broken build systems, and general hostility to humans, is probably the worst commonly-used language for iteration speed. I'm sure there are people who disagree with this, and I imagine those people are pretty confused as to why Javascript and Python took over the world.

For a whole bunch of reasons, C++ also seems to be a difficult language for LLMs to write. They're still _really good_ at it, which may explain the different results between the METR and Google RCTs: There was so much headroom to improve iteration quality, and the iteration speed was reduced by a small relative amount in the Google C++ case, making the AI tools unambiguously helpful.

There's also probably a big difference in baseline productivity between the median Google software engineer using C++ and the median open source expert using a more civilized language.

## Zig, Jai, Odin, etc.

I was really looking forward to this family of "like C but better" languages becoming a thing:
- They're focused on making the experience more fun for the developer by reducing complexity and compile times, and significantly increasing the level of safety over C
- I strongly suspect that [arena allocation](https://www.rfleury.com/p/untangling-lifetimes-the-arena-allocator) is the best memory management strategy for most software most of the time, but every other language makes it hard or impossible to do
- Jai in particular proves that LLVM is unbelievably slow and bloated: It's possible to get all the benefits of compiled languages without blowing up our iteration speed

> [Jonathan Blow (Creator and Secretive Protector of Jai, Feb 2025)](https://www.youtube.com/watch?v=1ZywkzWefok):
> I do think that \[AI\] will become a big factor, where if you're not using it, you're at a big disadvantage. However, that day is not today.

I think today _is_ that day, and there's a good chance it was also that day back in February, we just didn't realize it. Unfortunately, I think this also means that all of these languages may be dead in the water. For one thing, I expect LLM assistance for these languages to be significantly worse than for more popular ones: LLMs aren't trained on a giant corpus of Zig code because there is no giant corpus of Zig code. More importantly, a language being pleasant to write matters less if you're not writing all that much of it yourself.

## The Forbidden Languages

These languages have various uses, but no human should write them by hand ever again:
- CSS
- Bash
- AppleScript
- Vimscript
- CMake
- LaTeX (besides short inline things)

If AI does nothing else, preventing anyone from ever having to write a Bash script by hand again is a huge service to humanity.

I'm not sure which of these languages is the worst by any objective metric, but if someone came up to me and said "hey, can you write me a few hundred lines of $X$", I think my own personal disgust is maximized by $X = AppleScript$.

## Attention and Multitasking

I wanted to end with a note on attention, our most valuable resource. It really is all we need.

Claude Code can take a few minutes to do a big code change, which necessarily means your iteration loop when you're working is at least a few minutes long. This is nothing new to me: I've worked on projects with horrifically long compile times, so I know just how damaging they can be.

If it takes more than 30 seconds before you can see the results of your work, you've effectively hit a non-maskable interrupt. You're probably not just going to sit there and stare into space until everything's done. You're going to switch to a completely different task, or check out what your friends are up to on LiveJournal. This kind of frequent switching makes it so hard to stay on task. It's no way to work in the long term.

If you find that you're having a problem like this, I recommend trying a couple things:
- Go back and read Claude's plan more carefully while it's actually implementing it. Stay with the current problem and get some more context on what's currently happening.
- Switch to another Claude instance and work on a very related problem. This seems like it could also be problematic, but maybe less so. There could be big productivity benefits to doing this if you can manage it, so it might be a really good tradeoff.
- Find a way to monitor what Claude is currently doing, and try your best to keep up. You might need to build some custom magic to do this, as Claude dumps a lot of text into the terminal very quickly.

---
title: The Future of Software Engineering
date: 2026-01-13
---

If you are a software engineer, then you are obviously [responsible for the code you submit](https://simonwillison.net/2025/Dec/18/code-proven-to-work/), even if you used AI to generate it. For now, anyway.

> TL;DR: If AI models keep getting smarter, your responsible software development practices will eventually be pareto-dominated by someone YOLOing Claude Code and not even reading the generated code. ~~There will probably be smarter methods available for those willing to put in some work, though.~~

Before AI-generated code was any good, the traditional workflow on Very Serious Software Projects was:
- **Coding Iteration Loop**: This is usually solo work, where you write some code, run it to see if it works, write some tests (not necessarily in that order), then repeat.
- **Continuous Integration**: When you're finished putting your change together, you move on to the next iterative process. You kick off a bunch of static analyzers and automated tests, which point out a bunch of mistakes you've made, you fix the mistakes, then repeat.
- **Human Review**: The next step is to get at least one fellow human to review your work. This is another iterative process where they give feedback, you might update your code, ultimately ending in them approving the change.
- **Submitting the Code**: The final step is where you realize someone else modified (or moved!) the files you've been working on, so you need to do a bunch of busywork by hand to reconcile everything. This is hopefully not an iterative process, but if you're working on "busy" files, it could be! After that, you submit your code and move on to the next change.

This is still the workflow today, but LLM-based tools can have a pretty significant impact at every stage.

An important thing to realize is that, even without AI tools, there is a huge amount of variance in how each step is implemented in the real world. If you have a really good version of this process, it's probably just about optimal for creating software today. However, if AI models continue to become more capable, it's not clear to me that this will last very long.

One thing you can do to prepare for the future is to have very good metrics for things you care about in your project's code. This is useful for running conventional experiments on your software development process, and is likely to become far more valuable as AI models become more capable.

## Coding Iteration Loop

I'd expect the speed and quality of an engineer's coding iteration loop to vary a lot between different projects, based on the languages and technologies they use. As I [said before](https://downscore.github.io/2025/12/05/ai-productivity/):

> C++, with its long compile times, thoroughly-broken build systems, and general hostility to humans, is probably the worst commonly-used language for iteration speed. I'm sure there are people who disagree with this, and I imagine those people are pretty confused as to why Javascript and Python took over the world.

The subjective quality of the code probably also matters, but not as much as any of us would like. Remember when you did that nice, "clean" rewrite-from-scratch of your big, messy project, and it didn't turn out quite as clean as you hoped?

### Centaur Coding and Ralph Wiggum

_Aside: This is the place where most blogs would insert an AI-generated image of a centaur writing code. Please feel free to generate your own with the best model available to you, so that the experience of reading this blog improves with progress in AI image generation._

"Centaur Chess" (also known more boringly as "[Advanced Chess](https://en.wikipedia.org/wiki/Advanced_chess)") refers to a brief period where a talented human chess player with AI assistance could perform better than AI alone. We don't live in that world anymore when it comes to chess -- Magnus Carlsen would just get in the way of the AI -- but we do when it comes to coding.

The comparison seems even more apt when you consider just how close we came to a [Deep Blue moment for coding](https://arstechnica.com/ai/2025/07/exhausted-man-defeats-ai-model-in-world-coding-championship/) last year. May moonlight guide you, Przemysław Dębiak.

For now, a human in the loop is necessary for Codex or Claude Code to do some actual engineering work. A more experienced human in the loop probably provides more value on the margin, as measured in code quality or development speed. It's unclear to me at this point how we should value "experience with software development" relative to "experience with AI tools." You probably want to have at least a bit of both.

I'm not sure I buy takes like "a junior engineer who knows how to use AI is more valuable than a senior engineer who doesn't." I think the senior engineer can ramp up in Codex pretty quickly.

In Centaur Coding, your new Coding Iteration Loop looks like:
- Generate a plan for the code
- Read and iterate on the plan
- Generate the code
- Generate tests for the code
- Run the code and tests to see if everything works
- Read the code and tests to make sure they are reasonable
- Manually fix any issues, or prompt the AI to do it

You don't have to do it in that exact order. I understand the people of Test-Driven Development are back out in force in the age of AI. It's important to note that the most effortful part for the human is probably reading the plan, and reading the resulting code. Those are the biggest bottlenecks in the process.

Concerningly, Centaur Chess wasn't around for very long before AIs became strongly superhuman, making a human in the loop counterproductive. We can already see Centaur Coding starting to fray around the edges: The "[Ralph Wiggum](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/ralph-loop)" technique suggests that a `while` loop can be a pretty good replacement for a human software engineer.
 
Anyone remember when tech jerks used to wear t-shirts that said "go away or I will replace you with a very small shell script"? Are we going to replace those people with an even smaller `while` loop? I guess irony can be pretty ironic sometimes.

## Continuous Integration

This part is already fairly automated. Your linters, static analyzers, and test suites run on their own, then you fix the problems they found.

One big problem with code emitted by both AI and humans is that it tends to be messy. Asking AI to clean up the code actually seems to work pretty well. You can add a step in your CI process that gets an LLM to look at your change with a clean context, and see if there's anything that can be improved or cleaned up.

## Human Review

 Human code reviews suffer from a lot of problems. A _lot_ of problems. To the point where they likely often have net negative value, but there are weird organizational incentives (such as blame avoidance) that keep them from changing too much.

Two big, but related, problems with code reviews are:
- They are definitely noisy.
- They are probably not idempotent.

It's hard to find good research about this, so we'll just generalize from the [famous NeurIPS review experiment](https://arxiv.org/abs/2109.09774) in a wildly inappropriate way. In terms of noise: at big tech companies, I'd expect the choice of reviewer to explain a lot more variance in outcomes than the actual code being reviewed.

In terms of idempotence: If you send a reviewer change $c$, they might ask you to modify a few things, and ultimately approve change $c^{\prime}$. If you had instead sent them $c^{\prime}$ to begin with, they wouldn't have just approved it -- they'd ask for some more modifications and ultimately approve $c^{\prime\prime}$.

Both of these are a problem if you'd rather enforce objective quality standards than play social status games through the medium of code. We'll come back to objective quality standards later, as I think they will be incredibly important.

AI is pretty good at code reviews at this point. It may even be considered good manners to have an LLM look over your change before you send it to a human. And it's bad manners in turn if that human just copies and pastes whatever their LLM said about your change.

I think at some point the only reason not to replace human reviews with AI reviews is that the AI has no authority to prevent you from submitting your change. But that's a social dynamics problem, not an objective quality problem.

## Submitting the Code

The final phase of the process is actually getting your change submitted. This part seems worth mentioning in terms of AI because it's often where you get bitten by refactoring.

If someone has moved the code you're working on, you now have a very unpleasant, mostly-mechanical job to do: you have to port all your changes to wherever the code now lives. This doesn't involve any creativity or human ingenuity, it's 100% drudge work.

It's also something current LLMs are really good at. They can check recent changes to find out where the relevant code has gone and take care of all the porting for you. One of the [first posts I read asserting much higher productivity in Claude Code](https://www.lesswrong.com/posts/pcFSo5hEzzGTZEXEd/how-i-became-a-5x-engineer-with-claude-code) mentioned that one of the main places LLMs speed you up is in refactoring work. I found that a pretty compelling argument at the time, and have only become more convinced it's true: if you're not getting a productivity boost from current AI, you're probably not using it for refactoring.

## Objective Quality Metrics

If you can actually define some objective code and software quality metrics, and they're actually what you care about, then you should be paying extremely close attention to increasing AI model capabilities. (Also, you're a very rare kind of human, and I like you.)

Having these metrics lets you run experiments where you ablate parts of the software engineering process (like human reviews) to see what the effects actually are. You'll also be able to identify the point at which YOLOing Claude Code and not slowing down to manually read the code becomes a better way for you to develop software by every metric that you care about.

If your LLMs are consistently outputting high quality code, at what point do you stop slowing things down by having humans read it? Seems very valuable to have an actual answer to this question!

## YOLO World

Okay, I actually changed my mind about the conclusion of this post about 3/4 of the way through writing it, and after I had already written the TL;DR at the top. I just crossed out the part of the TL;DR that I no longer think is true.

The main purpose of this blog is for me to get my thought process down in writing so I can make sure I'm not fooling myself with sloppy thinking. Doing it in a place where other people might read it provides a bit of additional incentive to get it right. Even if no one else ever reads this, actually producing this post was a very valuable exercise for me.

The conclusion I originally wanted to write was something about how [conformance suites](https://simonwillison.net/2025/Dec/31/the-year-in-llms/#the-year-of-conformance-suites) are the future, and designing them is the main place where the human will sit in the loop. The suites would specify the behaviour you care about, and the AI would build something that satisfies the suite while minimizing [Kolmogorov complexity](https://en.wikipedia.org/wiki/Kolmogorov_complexity): An Occam's Razor approach to software development that minimizes surface area for bugs and security problems.

It still seems possible that this will all be true, but it doesn't seem at all stable. I think LLMs will rapidly get good enough at producing the conformance suites that you won't actually need a human in the loop before long.

I'm now pretty convinced we're flying straight into YOLO World and the best thing we can do is have a lot of metrics measuring the things we care about. That way, we'll have at least some insight into what's happening in the strange new world of software engineering.

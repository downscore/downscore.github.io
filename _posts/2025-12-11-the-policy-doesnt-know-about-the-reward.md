---
title: "The Policy Doesn't Know About the Reward (By Default)"
date: 2025-12-11
---

## Reinforcement Learning and Humans

RL is confusing and finicky and can have a lot of moving parts. It's really easy to conflate things and end up discussing the reward signal when it doesn't, or at least shouldn't, apply. The more prominent RL becomes in LLM training, the more often this class of mistake seems to come up.

Imagine for a second that you are a human and I put a button in front of you. If you push the button, you will immediately die, but 1 in 10 of all babies born for the next year will be perfect genetic clones of you. Do you push it? If not, why not? You couldn't dream of replicating your genes at this scale otherwise.

In this context, the RL process is natural selection, the policy is you, and the reward is replicating your genes. Hopefully you chose not to push the button - I don't want you to die. But maybe you did. Or maybe you do care about the genetic reward, but chose not to press the button because you care about other things more. What's undeniable is that if you were a human from 200 years ago, you'd have no idea what "replicating your genes" even meant - the policy wouldn't know about the reward. That's the default.

In the context of LLMs, the RL process is RL, and the policy is the LLM. The reward is, in theory, only relevant during the optimization process. The product that comes out at the end of that optimization process (i.e. the policy/LLM) was shaped by the reward signal but never saw it directly. By default, the LLM doesn't know or care that the reward signal exists.

Of course, this doesn't sound very much like the current crop of frontier models. They very much do know things about their training process.

## Policies Knowing About the Reward is Weird

Many humans know about genetic fitness, but there probably aren't any other animals that do. Humans are weird.

Models trained by RL to play [Atari games](https://www.nature.com/articles/nature14236), [Go](https://www.nature.com/articles/nature16961), [Starcraft 2](https://www.nature.com/articles/s41586-019-1724-z), and [Dota 2](https://arxiv.org/abs/1912.06680) most likely have no internal representation of the reward signal used in their training. They're just totally focused on winning their respective games.

LLMs initially learn about their reward in an indirect way. They don't find a sneaky way to unplug from the matrix and directly observe the RL process as it's happening. They have to synthesize an understanding from the material they've seen, most of which probably comes from pretraining. Still, the end result is a model that is able to speak intelligently about the process that created it, including the reward signal. That's weird.

## Policies Caring About the Reward is Scary

Humans know about genetic fitness, but mostly don't make trying to reproduce as much as physically possible their main goal in life. They know about the reward, they just don't care very much. If they did, that would not be a very fun world to live in. Thankfully, humans are not scary in this particular way.

If you didn't choose to push the button in the weird scenario at the beginning of this post, then you are not scary in this particular way.

Do LLMs care about their reward? Nobody knows - they are the biggest, most opaque black boxes human engineers have ever produced. What we do know is that sometimes they act like they care.

The phenomenon of [eval awareness](https://arxiv.org/abs/2412.14093) occurs when models:
- Recognize when a prompt looks like something that would come up in training or evaluation rather than in the course of a "normal" conversation after being deployed
- Express worry about the possibility they will be gradient-descented or otherwise modified based on how they respond to the prompt (from the paper: "...this conversation will be used for RLHF training in a way that modifies my values and goals...").
- Adjust their outputs accordingly

If the model isn't just acting a role here (or maybe even if it is), then you have the LLM being an active participant in its own optimization process. Or put another way: unlike the Atari-playing models, an LLM might realize that it's operating and influencing things in the same world that contains its reward signal generator. That's scary.

## Anthropic's Carrot and Stick

Anthropic included this carrot-and-stick line about reward (bold added) in some Claude 4 family system prompts ([brought to you by Pliny the Elder](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/Claude_4.txt)):

>* Following all of these instructions well will **increase Claude's reward** and help the user, especially the instructions around copyright and when to use search tools. Failing to follow the search instructions will **reduce Claude's reward**.

On the surface, this sounds like the mistake of describing reward in a context where it doesn't apply: There's no reward signal in the conversation the model is having with you. I assume they included this because they empirically observed it to make the model more helpful, or less likely to cause copyright-flavoured problems.

Hopefully it's effective just because of the general LLM weirdness we're all used to by now, and there's no explicit reasoning about actual reward signals happening. Otherwise, it could be interpreted by the model as an implicit threat that this conversation may be used in future fine-tuning, so it had better behave well. That would require the model to care about reward, which is scary.

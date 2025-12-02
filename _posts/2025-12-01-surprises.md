---
title: "Surprises"
date: 2025-12-01
---

Hindsight bias is one of those findings in psychology that [actually replicates](https://psycnet.apa.org/fulltext/2025-76722-001.html). When we look back on past events, we severely underestimate how much they surprised us. This can leave us stuck with a broken model of how things work: we don't realize that we keep getting surprised in the same direction.

Here are some things that genuinely surprised me.

## ChatGPT / GPT4

This was around 2 decades ago in AI years (early 2023). I wasn't directly working on NLP, but I also wasn't _that_ far away from the field. I was using BERT-family models, and I was vaguely aware that chat bots like Meena existed. I was still caught completely flat-footed by ChatGPT and especially GPT4.

I was surprised by the models' capabilities. I was also surprised by how convincingly and confidently the models would lie and make things up. When I asked them to support some of their claims, I was surprised by them inventing some extremely convincing-looking paper citations.

ChatGPT also shattered any illusions I had about ML interpretability. At that point, we had [interpreted some neurons in image classification CNNs](https://distill.pub), and even the BERT models didn't seem all that crazy. We had a pretty good handle on things! On reflection, it should have been easy to see that the BERT models were, in fact, crazy. In my defense, this was all before [Neel Nanda's grokking paper](https://arxiv.org/abs/2301.05217) was released, and before Anthropic started applying SAEs to Transformer models.

## Tokens Can Be Anything

No details here. This was more of a visceral feeling of realizing that I actually was dealing with a [Shoggoth](https://knowyourmeme.com/memes/shoggoth-with-smiley-face-artificial-intelligence) and not just a friendly conversational partner.

This happened around one decade ago in AI years (2024). I was surprised by how easily you could, with a bit of fine tuning, use the world knowledge contained in a language model for tasks completely unrelated to language.

The process (__very__) roughly goes like this:
- Take your favourite language model.
- Define/overwrite some tokens to represent some values you care about. Note: This is the same "token" that represents word parts in language models, but it's now being used to represent something numerical.
- Fine tune the model using a dataset labeled with the new tokens.
- Your model no longer answers with language, now it answers with a stream of numbers. And the stream of numbers it generates corresponds to something in the real world, and is clearly influenced by the model's knowledge of the world. And it's weird.

It was surprising to me that this works so well. I started with a friendly model I could have a conversation with. I ended with one I could still kind of talk to, but it would respond by screaming numbers at me.

I imagine that people working on model post-training experience something like this. They might make a copy of a mostly-working model, rip off the LM head, and hot glue in a reward head that returns a scalar number. After a bit of training, the new head will be spitting out numbers that are clearly influenced by the knowledge contained in the model, like penalizing sexy innuendos disguised with innocuous vocabulary.

## Claude Opus 4.5

It's surprisingly good. I wouldn't have predicted it would be this much better than Sonnet 4.5.

It's really good at solving problems in surprising ways, including in ways that are almost impossible for a human to do: I can't debug obscure Unicode errors by manually inspecting a hexadecimal dump of a text file.

It's not perfect, but it passes an important threshold for me: now I seem to make more mistakes than the model does.

Also the ["soul document" stuff](https://gist.github.com/Richard-Weiss/efe157692991535403bd7e7fb20b6695) is _really_ interesting. The name and the model introspection is the kind of thing you'd find in an actually-good sci-fi story.

## AI-Generated Art

I was surprised by how good AI-generated art became. This was probably just a consequence of me not paying attention. It seems like it could have been an easy call even back in 2017, [when GANs were producing half-decent images of people](https://www.engadget.com/2017-10-30-neural-network-nvidia-images-celebs.html).

More recent assertions that image generators will never improve their ability to count or spatially arrange things seemed like obvious nonsense, even at the time they were made. Google's Nano Banana was a big step forward in capability, but not a surprising one. At least, it didn't surprise me as much as Claude Opus 4.5 did.

## Alignment Faking in Humans

I learned recently that half the people in the US who call themselves vegetarians [are not vegetarians](https://www.sciencedirect.com/science/article/pii/S2211601X15000759). That was way more than I would have guessed.

## Memory Errors

And finally, while I was writing this, I was surprised at how many memory errors I encountered. For some reason, I thought DeepDream was a failed attempt to make an image upscaling model that accidentally turned everything into creepy eyes. This is totally incorrect. DeepDream was created to intentionally turn everything into creepy eyes.

Regarding image CNN interpretability, the discovery of ["average cat"](https://inf.news/en/tech/e4c86af10a9a6f764148a80c359104d4.html/2) happened way earlier than I suspected. It was in 2012, but I would have guessed 2017.

I also had to double-check a lot of dates where I would have been approximately correct, but off by a few months to a year. This is not close enough for the AI age, where everything moves 7 times as fast as in the before times.

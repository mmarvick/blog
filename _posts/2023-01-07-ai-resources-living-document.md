---
layout: post
title: "AI Landscape: Resources (living document)"
modified: 2023-01-07
categories: blog
excerpt:
tags: [ai]
image:
  feature:
date: 2023-01-07
hidden: true
---

I'm interested in understanding the overall landscape of AI, mostly around the technical landscape and paths forward, and the societal impacts.

I'm going to start tracking some of the podcasts / articles / etc I've been reading and how they're influencing my thinking.

This is a living document, I may update notes on some of these if I relisten or hear complimentary / contrasting views. I'll mostly summarize what I heard from the speaker, and may not agree with everything.

Even where I'm just transcribing the big points, my lens into what I think is important influences how I summarize. I'll also note my take on things occasionally. Again, both the summary and my takes are liable to change over time, and the notes here will sometimes be updated but may not always reflect my most recent thinking.

- [Sam Altman on Ezra Klein Show](https://www.nytimes.com/2021/06/11/podcasts/transcript-ezra-klein-interviews-sam-altman.html) (podcast)
  - **The big picture:** Believes we can keep scaling up neural nets with more data and more compute, we'll get general intelligence, and can use that to go beyond humans and develop new knowledge.
  - Advocate for ingesting tons of data into current model architectures
  - More compute and data = smarter model; keep scaling up
    - Believes no reason we'll hit a ceiling we can't progress beyond
    - Suspects we'll be very general purpose in 20 years, but could be a few decades give or take. If 100 years from now we don't have general purpose AI, it's because he was wrong about no ceiling
  - Believes we train one big model, rather than lots of agents interacting
    - Wants to see AI not just using knowledge but also inventing new knowledge; needs to be very general purpose to do so
  - Will be expensive; mostly OpenAI, Google, etc. scale companies doing this model development
  - From the big model, products could be:
    - The big model is general enough and smart enough to do everything
    - Specialist companies / groups take that model and further train the last layers to do well in a domain -- e.g. medical, law
  - Doesn't have business model for OpenAI, just focusing on general intelligence
    - Thinks it'll be obvious how to make money.
    - Will ask the general intelligence system what the best business / profit is.
    - Capped initial investors at 100x returns to avoid bad incentives once such a powerful technology exists (e.g. just using to manipulate / sell ads)
- [Gary Marcus on Ezra Klein Show - A Skeptical Take on the A.I. Revolution](https://www.nytimes.com/2023/01/06/opinion/ezra-klein-podcast-gary-marcus.html?showTranscript=1) (podcast)
  - **The big picture:** Bullish on artificial intelligence, but believes we need to use symbolic architecture (not just deep learning) to get something that can reason. Otherwise it's just a lot of synthesizing, which is limited and liable to create garbage. Believes these architectures can work together to build something valuable and aligned with human interests.
  - Believes in general intelligence but thinks deep learning will hit a wall
    - Studied linguistics under Steven Pinker; references Noam Chomsky
  - Introduces symbolic AI: machine needs to understand "symbols" (like concepts) to make rational and reasoned decisions
    - Similar to language; we don't just hear the words and say words back, we understand deaper meaning and reason
  - Deep Learning is just a big autocomplete - great for some tasks, not for others
    - Cannot know concepts of "truth" or morality
    - e.g. can't tell ChatGPT "tell me the truth for the next 5 prompts", it doesn't know
    - If you ask ChatGPT to count words in a sentence, it gets wrong a lot of the time -- doesn't understand the logic
  - Just throwing more compute and data at it will hit a wall. If we can't teach truth now, just showing more data won't teach it what truth is. It'll understand more situations, but will still get stumped outside of them
    - Example: Tesla autopilot just hit a big and expensive jet that was parked. A human wouldn't have done that, even if it had never seen a parked jet when driving. Human would know it was a big expensive thing, should probably be cautious.
  - Long history between Symbolic and Deep Learning advocates in academia
    - Tensions - Symbolic used to get prestige; now all moved toward Deep Learning
    - Thinks there should be more collaboration
    - Thinks we're over-focused on Deep Learning right now and blinded to its weak points
  - Symbology is hard to encode, and we have a huge amount of complexity in the world, seems we'd hit a wall with this
    - Shouldn't manually encode all symbols; can use learning algorithms for that
    - Humans with a simple education can then be trained to do a huge variety of tasks pretty easily, but it's due in part to core understandings of world, we want our AI systems to have that
    - *My note:* We use curriculums to get humans up to speed faster (don't have to redevelop all of human knowledge from scratch); presumably we do the same with AI before it goes and makes new knowledge or do fast things, it's just faster. Engineering that curricula will have challenges, just like writing a good curriculum for kids/humans is a skill.
  - General intelligence doesn't need to work exactly like the brain or humans; should draw inspiration but there are limitations (e.g. biases)
    - but do take the learnings from neurobiology; don't just throw them all out because deep learning is really good at autocomplete or speech-to-text
  - Are we holding AI to too high a standard? Humans do a lot of splicing together what they've heard without being right
    - While true, we usually try to develop some reasoned understanding of things we opine on, and for things we're deeper experts that reasoned understanding is deeper
  - Haven't been many incentives for companies to build general intelligence. They make lots of money by solving specific problems; why spend 100x to build something 10% better at their money-making problem.
    - May be room for public development; thinks there should be something like CERN for AI
    - *My take:* I agree with the general point, but do think there'd be tons of money in getting this right. But it might mean spending billions or trillions before any dollar is earned, which companies don't usually do.
- [Andrej Karpathy on Lex Fridman](https://lexfridman.com/andrej-karpathy) (podcast)
  - **The big picture:** Biggest problem is to solve in general intelligence: once we solve it, we can use it to solve any other problem we're working on
  - Programming 2.0: Imperative programming will become less necessary over time
    - Why write a complex rule engine with thresholds in software, that we're just guessing at and iterating on anyways. Use a neural net / other model for that
    - e.g. for optimization problems
  - Note - There were more takeaways I felt when I first listened to this; may relisten and capture more notes later. I'm writing this a month or two out. But the big picture and progamming 2.0 stuck with me.
- [Michael Levin on Lex Fridman](https://lexfridman.com/michael-levin) (podcast)
  - I'm in the process of listening to this
  - Biology background; how we can use biology in our AI systems
  - Xenobots: engineered lifeform that can accomplish a desired goal
    - Engineering went from static materials (wood, metal) to active materials (electronics), to computation materials, now we have agential materials with their own goals and agenda we're engineering a collaboration with
    - *My question: where does ethics start coming into play?
- [Elon Musk on Lex Fridman third round](https://lexfridman.com/elon-musk-3/) (podcast)
  - **The big picture:** Autopilot uses human-like sensors (vision, sound), not lidar, since it's all humans need. Uses neural nets for specific problems and imperative engineering to combine; not straight out "AGI".
  - Some discussion of Autopilot architecture
  - Autopilot only using vision and microhpone sensors, not using LIDAR like competitors
    - Humans do it with eyes and ears, a system using general intelligence should too
    - *My view - libable to change*
      - I think this is a reasonable take to get human and better performance
      - There are limitations under conditions like bad weather, poor visibility, where better sensors 
  - Different layers of the problem
    - detecting edges, then objects, then general situations
    - using imperative programming / engineering to glue these together, but what today is imperative may become trivial or AI later
    - different layers getting optimized over time as they are well solved (e.g. in C or hardware), so can focus effort on higher level
    - *My view* - I'm skeptical of using neural nets to solve everything, but this seems like it doesn't -- it uses neural nets for specific problems and more imperative engineering to synthesize. Seems better than just "Deep Learning = AGI" approach, but there are still cases where system fails -- if it lacks deep understanding, I wonder if using neural nets with imperative glue will keep working, or if there needs to be more symbolic understanding. My understanding here (of what they're actually doing and the correct path) is obviously shallow; won't pretend to know how to engineer system, just current impression.
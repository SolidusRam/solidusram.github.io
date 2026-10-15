---
layout: post
title: "Twelve days, 130 commits: making Frogger 3D with an AI"
subtitle: "What changed when the code got cheap, and what didn't."
---

<figure>
  <video src="{{ '/assets/img/frogger-punch.mp4' | relative_url }}" autoplay loop muted playsinline></video>
  <figcaption>Punching cars into the traffic, at sunset (heat level 3).</figcaption>
</figure>

A frog with boxing gloves punches a car. The car flies off, crashes into two others, and the wreck becomes a raft on the river behind it. That's the whole pitch of [Frogger 3D](https://github.com/SolidusRam/Frogger3D), the game I made between the 1st and the 12th of October 2026.

The idea came from an Instagram reel. It showed a very fast, chaotic version of Frogger: a frog with elaborate animations that did karate moves on the cars, glided with a hang glider and destroyed everything it touched. It looked artificial, and the frog was far too overpowered. I never found the reel again, but it stuck.

What I wanted to find out wasn't really about Frogger. I wanted to see whether I could use frontier AI models and nothing but natural language to describe a game and my ideas, and turn them into a finished product. I haven't written a single line of code by hand: I made it together with Claude, Anthropic's AI assistant, and this post is about that as much as about the game.

I was also tempted by the idea of putting it on Steam. I never took it seriously, but I did ask for a market opinion, and that is part of the story.

## The numbers

| What | How much |
| --- | --- |
| Days | 12 on the calendar, 8 with commits |
| Commits | 130 in the twelve days (136 today, with the release), every one co-authored by the AI |
| Game code | about 15,200 lines of GDScript in 64 scripts (plus tests and tools) |
| Automated tests | 45 |
| 3D models | 57, built from code in Blender |
| Sound effects | 71, generated from code |
| Design documents | about 24,600 words |

## How I worked

I did all of this around a university internship. The mornings belonged to the internship; the evenings I spent at the keyboard, describing what I wanted. The AI had a daily allowance of usage, and I spent all of it, every day, on development. During the day I kept going from my phone with the remote feature: I sent prompts and asked for screenshots to see what it was doing, when I was out with friends drinking.

## Everything written down, in Italian

Besides the game, the project had a second product: text. Every rule, decision and doubt lived in plain-language files inside the repository, written in Italian (this post is in English). There are seven of them, about 24,600 words: the design rules (`regole-design.md`, the single source of truth from 1 October), a chronology, a list of future ideas, the feats, a sound study, a music brief and the account of the browser port. Decisions are dated, and when one changed, the file says what it replaced and why. The habit never lapsed: 117 of the 136 commits touched these files, and 35 touched nothing else, decisions written down before any code existed. In my experience, it was like filling in a script, or reading a work proposal.

## How it went

**Day one.** The prototype landed at 1 a.m.: a frog, a road with "hybrid" traffic (cars drive on rails until you hit them hard enough, then they turn into physics wrecks) and a river. Sixteen hours later the commit log says *base game complete*: endless sections, dens, a heat meter that only goes up, a game-over screen.

**The day of decisions (4 October, 38 commits).** It became a roguelite with endless runs, power came only from the dens, and a wildfire started chasing the frog, which gave the run both a reason to move forward and a way to end.

**The frame (5 October).** Blender models for the frog, logs and crocodiles; options, controller support, an English translation; a sound study, then 71 effects generated from code in about an hour. And the first real playtest. The models looked exactly as I had described them, which was interesting to see.

<figure>
  <img src="{{ '/assets/img/frogger-models.webp' | relative_url }}" alt="Twelve low-poly models from the game: the frog with boxing gloves, a crocodile, a log, a hang glider, four road vehicles, a locomotive, an airliner, a house and a pine tree." width="1440" height="1080" loading="lazy">
  <figcaption>Twelve of the 57 models, all built by one Python script in Blender, in the game's colors.</figcaption>
</figure>

**Systems on systems (6-8 October).** A 20-card deck, six frogs, achievements, hats, difficulty levels, and then a second world in the sky: clouds instead of logs, eagles instead of crocodiles, a thunderstorm instead of the fire, and an aerobatic squadron you can ride.

## The decisions that changed

Several design decisions changed along the way, and three of them taught me the most.

The first was where power comes from. The plan was that chaos would give experience: wreck a car and something drops among the wreckage. On 4 October I took it out, and power came only from the dens. The reason is the one I tell below, in the part about ideas: the traffic jam would have become the best place to farm.

The second was what the frog starts with. At first it had all three powers from the very beginning: the punch, the super jump and the glider. On 6 October I changed it: every frog starts with the boxing gloves only, and the rest comes from cards picked in the dens. That gave me different frogs, and builds that are born during a run instead of being there from the first second.

The third was the ending of a run. I first imagined a fork: depending on how much heat you had built up, you would end up in heaven or in hell. On 7 October I dropped it. The heat only goes up, and using the powers makes it go up faster, so to reach heaven you had to avoid the powers, which meant denying yourself the fun. The reward felt either pointless or punishing. In its place came worlds in sequence inside one run: when the heat is at its maximum a teleporter appears, and it takes you to a new world with the heat back at zero and the fire left behind. The first world is the ground, the second the sky.

The last two changes were about the game itself rather than its rules: from a Steam release to a browser version, and from the browser to GitHub and this post. I tell them next and in the part on what went wrong.

### Steam, and a plan that looked studied

I asked Claude what a Frogger could expect on the modern market. The written version of the answer is in [`docs/idee-future.md`](https://github.com/SolidusRam/Frogger3D/blob/b77bdd5/docs/idee-future.md), dated 4 October (commit `b77bdd5`). It had a table of scenarios: with no marketing, the most common case, fewer than 1,000 wishlists, 100 to 300 copies in the first year, a few hundred euros. It also warned that "Frogger" is a Konami trademark, and that the name would have to change before any Steam page.

It looked like a carefully studied plan, and it fed my wish to create something and to find out whether my work could be worth something, which is far from a given. Still, I couldn't picture a game like this on the market, and I never took the idea of putting it on Steam seriously. On paper it stayed the plan until 8 October; in my head it never was.

## Where it went wrong

Two things went wrong, and they have something in common: technical inadequacy. Maybe a real skill that I should have had, or should have built through the experience of a real game developer; or maybe a genuine technical impossibility. I can't tell which, and that is part of the problem. Concretely, I decided to close the project as soon as possible.

### The browser

On 9 October I tried to turn it into a browser game. It ran at 1 to 3 frames per second. Two causes turned up: far too many draw calls (2,700 per frame, cut to 1,500) and a memory leak in Godot's web audio, which copies the whole sound every time one plays, so the tab grew to 3 GB. A third cause, in Firefox, I never found. I set it aside and rolled back.

### Ideas and fun

Sometimes development could run a little ahead of my ideas. The AI could build faster than I could decide what to build, so the scarce thing was no longer code but direction. It happened with the world after the sky: a mechanic I hadn't fully explored yet, and I ran out of ideas before the AI ran out of work.

So I tried to delegate the ideation: some mechanics, power-ups, secondary missions to unlock things. They almost never convinced me. Two examples, both proposed by the AI. The first was experience from chaos: wreck cars, earn experience, dropped among the wreckage. It sounded right for a game about chaos, and I shelved it on 4 October because the traffic jam would have become the best place to farm. The second was a "greedy tongue", yet another tongue for the frog. I discarded it on 6 October because the grappling tongue already eats flies, so it added nothing. Neither idea was absurd, and that's the problem: they were plausible. What was missing was a broader overall direction: maybe I should have looked further ahead, with the finished game already in mind. To me that's a point in favor of the human side of ideation: the spark, the thing that makes you care about a game, still has to come from a person or a great director.

The second limit is playability. How fun a game is isn't an objective parameter, and someone has to be able to describe it well, and that takes real skill, even in a very capable person. I only tasted how hard that task is; I can just imagine what it means in the actual working world of game development.

## So, did it work?

Yes, but. Skills and personal paths still matter, and a strong development tool remains unbeatable: between brooding over an idea and building it straight away, you lose a lot in the brooding. We are in an era of heavy hype around building things, somewhere between AI slop and striking, useful projects. Can we really create something with impact? A tool that simplifies our work, or even just a temporary pastime? Frogger 3D is at least that.

## Play it, read it

- **Play**: download it from the [releases](https://github.com/SolidusRam/Frogger3D/releases) (Linux and Windows, nothing to install).
- **Code**: [github.com/SolidusRam/Frogger3D](https://github.com/SolidusRam/Frogger3D), MIT for the code, CC BY 4.0 for the assets.
- **The design documents** are in the repo, in Italian, every decision dated.

*"Frogger" is a trademark of Konami. Frogger 3D is a free, unofficial fan project.*

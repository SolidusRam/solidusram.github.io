---
layout: post
title: "Twelve days, 128 commits: making Frogger 3D with an AI"
subtitle: "What changed when the code got cheap, and what didn't."
---

<!--
DRAFT. Drafts are not published: Jekyll skips the _drafts folder.
To publish: move this file to _posts/ and rename it YYYY-MM-DD-frogger-3d-twelve-days.md.
Preview drafts locally with: bundle exec jekyll serve --drafts

Everything in [brackets] is a prompt for you. The facts and numbers come from
docs/cronologia.md in the Frogger3D repo. Rewrite freely: it should sound like you.
Target length: 1,500-2,500 words.
-->

<!-- TODO: a 5-10 second GIF or video of the frog punching a car into a chain of crashes.
Record it from the real game (the Vulkan renderer looks better than the screenshots tools make).
Save it as assets/img/frogger-punch.mp4 or .gif and uncomment:
<video src="/assets/img/frogger-punch.mp4" autoplay loop muted playsinline></video>
-->

A frog with boxing gloves punches a car. The car flies off, crashes into two others, and the wreck becomes a raft on the river behind it. That's the whole pitch of [Frogger 3D](https://github.com/SolidusRam/Frogger3D), the game I made between the 1st and the 12th of October 2026.

[One or two sentences: why Frogger, why this idea, what you wanted to find out.]

I made it together with Claude, an AI assistant, and this post is about that as much as about the game.

## The numbers

| What | How much |
| --- | --- |
| Days | 12 on the calendar, 7 with commits |
| Commits | 128, every one co-authored by the AI |
| Game code | about 15,200 lines of GDScript in 64 scripts |
| Automated tests | 45 |
| 3D models | 57, built from code in Blender |
| Sound effects | 71, generated from code |
| Design documents | about 23,000 words |

## How it went

**Day one.** The prototype landed at 1 a.m.: a frog, a road with "hybrid" traffic (cars drive on rails until you hit them hard enough, then they turn into physics wrecks) and a river. Sixteen hours later the commit log says *base game complete*: endless sections, dens, a heat meter that only goes up, a game-over screen.

**The day of decisions (4 October, 38 commits).** It became a roguelite with endless runs, power came only from the dens, and a wildfire started chasing the frog, which gave the run both a reason to move forward and a way to end.

**The frame (5 October).** Blender models for the frog, logs and crocodiles; options, controller support, an English translation; a sound study, then 71 effects generated from code in about an hour. And the first real playtest. [What did it feel like to play it for the first time?]

**Systems on systems (6-8 October).** A 20-card deck, six frogs, achievements, hats, difficulty levels, and then a second world in the sky: clouds instead of logs, eagles instead of crocodiles, a thunderstorm instead of the fire, and an aerobatic squadron you can ride.

## The decisions that changed

[The heart of the post. Pick the two or three that taught you the most and tell them as small stories.]

| Before | After | Why |
| --- | --- | --- |
| Chaos gives experience, dropped among the wrecks | Chaos gives no power; power comes only from the dens | The traffic jam would have become the best place to farm |
| All three powers from the start | Start with gloves only; the rest comes from cards | Different frogs, builds born in the dens |
| A heaven/hell fork chosen by heat | Worlds in sequence inside one run | — |
| Steam page, demo, a 5-8 € release | A browser-only version on my own site | Scaling the goals down |
| Browser-only | Set aside: GitHub and this post | 2 fps in the browser |

## When it went wrong

On 9 October I tried to turn it into a browser game. It ran at 1 to 3 frames per second. Two causes turned up: far too many draw calls (2,700 per frame, cut to 1,500) and a memory leak in Godot's web audio, which copies the whole sound every time one plays, so the tab grew to 3 GB. A third cause, in Firefox, I never found. I set it aside and rolled back.

[What did this teach you? A game that "worked" collapsed in a new context for reasons you couldn't see from inside it. Does that change how much you think you need to understand what's underneath?]

## What the AI changed, and what it didn't

[Be concrete and honest. Some questions to answer for yourself first:]

- [What did you actually do? The ideas, the decisions, the taste, the playtesting.]
- [What did the AI do? Most of the code, the models, the sounds.]
- [Where did the bottleneck move? From making things to deciding and to testing them? The "to try by playing" list grew faster than what got tried.]
- [Did building get so cheap that you built too much, too soon? The phase-one goal, 5-10 outside players who want to play again, was never tested.]
- [Is it your game? Where do you draw the line, and does it matter to the player?]

## What I think about making games

[Your opinion, in your words. This is the part that makes it a business card: three claims you'd defend in the comments against someone who disagrees.]

1. [...]
2. [...]
3. [...]

## Play it, read it

- **Play**: download it from the [releases](https://github.com/SolidusRam/Frogger3D/releases) (Linux and Windows, nothing to install).
- **Code**: [github.com/SolidusRam/Frogger3D](https://github.com/SolidusRam/Frogger3D), MIT for the code, CC BY 4.0 for the assets.
- **The design documents** are in the repo, in Italian, every decision dated.

*"Frogger" is a trademark of Konami. Frogger 3D is a free, unofficial fan project.*

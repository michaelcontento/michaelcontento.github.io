+++
date = "2022-11-30"
title = "Building a game in a day"
tags = ["PlayDate", "Lua", "Gaming", "InnovationDay"]
categories = ["Development", "Gaming"]
+++

On 2022-11-25 the second Innovation Day @ [Xpirit] took place and it was the first, where I hosted a slot.

But what is the Innovation Day you might ask? <!--more--> It's a quarterly get-together where all members of Xpirit join **physically** and innovate, explore, play and share knowledge. Think of it as a hackathon with your family 😄

To organize the day a bit we have our own internal tool called [XKE] (**X**ebia **K**nowledge **E**xchange) where everyone can start a new slot with his idea, and other can join. So it's really as simple as that. Join an existing one or start your own.

## PlayDate - a tiny handheld game system

Two days before the Innovation Day, me colleage [Thomas] introduced me to [PlayDate] and I was immediatly hooked.

How awesome is this tiny device? Seriously.

Small `400 x 240` pixel screen, two colors and a freaking physical crank!

Sure, those are fairly strict constraints compared to all other gaming systems -- but constraints spark creativity! At least this is what I read all the time on the interwebs ... 😉

## My first Innovation Day slot

So the fire was lit and I was eager to build something for this device. But with 2 days it was impossible to order a physical device in time.

But the community behind PlayDate is quite awesome and the free-to-use simulator is .. well .. amazing! It's plug and play (or download and run, to be more precise).

For the [Nova] editor there is a [extension][1] that also works like a charm. Even though I never used Nova or PlayDate before, it was just a few downloads, mouse clicks and everything was compiling and running smoothly.

So we have a plan: [Build a somewhat enjoyable game for the PlayDate console!][2]

## What do we wanna build?

On the Innovation Day there where 3 colleagues wo liked my idea and joined my slot. So the first thing to sort out:

1) Get the simulator running on every developers machine
2) Setup a git repository where we all can work in
3) Define what game we want to buid
4) Build the thing
5) Share it with all other colleages
6) 🍻

The first to points of the list where done in ~20 minutes. As I already said, the tools are plug-and-play and with [Playlate] we found a awesome project template.

Defining **what** we actually want to build took a bit more time. I mean, you could basically build anything on this device! Explore the crank on various creative ways! Thousands of ideas!

But our time was limited. And we wanted to ship something that could deliver up to 10 seconds of joy.

Why not cloning a simple, well known, game and just add a small twist? Ha! That it is!

We settled on [FlappyBird] as game and wanted to incorporate the crank to simulate "real flapping". So you have to swing back and forth for a single wing clap.

## The result

Look at the amazing result:

{{< youtube Scehich_JLM >}}

- It' a full functional clone of FlappyBird
- Runs smooth at max FPS with no issues at all
- We have background music as well as sound effects
- Sprite animations
- Endless level generation
- Highscore tracking
- Collision detection

All built within one day - I'm so proud of our group and our little mascot 🧡

## What have we learned?

- Building games is fune
- PlayDate is a very nice / polished gaming system
- We used [Lua] as development language
- We used [FFmpeg] to convert audio files to the proper format
- And we had a ton of fun in the building process itself


  [Lua]: https://www.lua.org/
  [FFmpeg]: https://ffmpeg.org/
  [FlappyBird]: https://flappybird.io/
  [Playlate]: https://github.com/downie/playlate
  [Nova]: https://nova.app
  [1]: https://extensions.panic.com/extensions/com.panic/com.panic.Playdate/
  [2]: https://xke.xebia.com/event/UiHeo6yw3MS6LsnUAEj1/Bd81zbPqzHnTwiP5hFrk/xpirit-game-on-playdate
  [Thomas]: https://tomow.de/
  [PlayDate]: https://play.date/
  [Xpirit]: https://xpirit.com
  [XKE]: https://xke.xebia.com/event/UiHeo6yw3MS6LsnUAEj1



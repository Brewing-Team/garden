---
title: "Tiny Glade Developers on Bevy, Proceduralism, Publishers & Cozy Games"
source: "https://80.lv/articles/exclusive-tiny-glade-developers-discuss-bevy-proceduralism-publishers-cozy-games"
author:
  - "[[Pounce Light]]"
published: 2024-05-30
created: 2025-09-21
description: "To celebrate the release of Tiny Glade's demo version, Pounce Light's Anastasia Opara and Tomasz Stachowiak have joined 80 Level to discuss the game's history, proceduralism, Bevy, Rust, self-publishing, and the \"cozy games\" genre."
tags:
  - "clippings"
---
[![](https://cdn.80.lv/api/upload/promo/2808/68ada741208ad.gif)](https://rendernetwork.com/)

To celebrate the release of Tiny Glade's demo version, Pounce Light's Anastasia Opara and Tomasz Stachowiak have joined 80 Level to discuss the game's history, proceduralism, Bevy, Rust, self-publishing, and the "cozy games" genre.

![](https://www.youtube.com/watch?v=QAUSBxxgIbQ)

If you haven't been living under a rock for the past couple of years and have even a passing interest in the indie game development industry, chances are you're already familiar with Tiny Glade, a relaxing castle-building simulator that has been all the rage on social media and now stands out as one of the most wishlisted games on Steam.

Here on 80 Level, we first noticed the game when it was quite early in development, back when it was just a [procedural wall generator](https://80.lv/articles/a-procedural-wall-generator-made-with-bevy-engine/) created as a weekend project using Bevy, a data-driven game engine powered by the Rust programming language. Throughout the entirety of this splendid generator-to-video-game transformation, we've had the pleasure of witnessing numerous impressive demos, which we've shared with you [on](https://80.lv/articles/tiny-glade-s-windows-roofs-get-updated-ahead-of-the-upcoming-launch/) [more](https://80.lv/articles/an-update-on-tiny-glade-a-cozy-castle-building-simulator/) [than](https://80.lv/articles/this-upcoming-game-lets-you-procedurally-glue-buildings-together/) [one](https://80.lv/articles/procedural-windows-in-pounce-light-s-tiny-glade-get-an-upgrade/) [occasion](https://80.lv/articles/anastastia-opara-s-procedural-wall-generator-now-has-pillars/).

Today, the community has finally got the chance to experience Tiny Glade firsthand with the release of its demo version on Steam. To commemorate this momentous event and learn more about the game the entire 80 Level team has been eagerly awaiting, we invited its developers, Anastasia Opara and Tomasz Stachowiak, to discuss Tiny Glade's history, proceduralism, Bevy, Rust, self-publishing a video game, and the "cozy games" genre.

***Why did you decide to launch [a demo version of Tiny Glade](https://80.lv/articles/long-awaited-cozy-castle-building-game-to-get-launched-in-may/)? Was it to collect feedback before the release, hype up the upcoming game, or something else entirely?***

**Anastasia Opara, Procedural Artist & Indie Game Developer:** I think it was a way for us to give people the opportunity to try out the game before buying it. Regarding your first point about player feedback, while we're looking forward to the community's reactions, we have already been conducting close playtests, so hopefully nothing will go wrong.

Mostly, we wanted to give people the ability to see if the game is their cup of tea or not and if they actually like it. You see, Tiny Glade is not a very traditional game that is best described as more of a toy box for making dioramas. We think that some players may even be surprised that they like it, while others may try it and be like, "It was good, but it's not really my vibe." And that's fair, but hopefully, it will be the former rather than the latter.

***You mentioned that you've already conducted some playtesting, could you please tell us about it? How did it help your pipeline?***

**Tomasz Stachowiak, Rendering Artist & Indie Game Developer:**One of the biggest issues we are continuously working on, because it is a thing that can't be figured out right away, is user experience. Essentially, it is the most critical aspect of the game because a significant part of developing this castle-builder is ensuring that interactions are satisfying, so if something is off with the controls or doesn't feel intuitive enough, it will derail the enjoyment of the game.

I'm not sure if we can mention any specific problems that we encountered during playtesting because it's usually just like, "Oh, something doesn't work quite the way it was expected to work," or, "Cool, we can make it more intuitive. Oh no, this derails this, and this means that. Can we just place the doors individually?" And five brainstorming sessions later, we're just like, "Doors – what does it mean?" So, pretty simple surface-level suggestions about what could be improved in our game turn out to be not that simple when plugged into the crazy procedural machinery that we have under the hood.

**Anastasia Opara:** In a way, we also wanted to see what people make with it and which direction they want to take the game. For example, what if you're trying to make a crazy castle on a hill or a cliff, what the pain points would be? O r if you're trying to do something, can you do it easily, or do you need to jump through many hoops and repurpose the game's tools to achieve it?

Our goal was to eliminate the need to jump through hoops and make the overall experience a bit faster and better, so I agree with Tom that the biggest struggle was the UX iterations. Some of Tiny Glade's features have gone through five or six iterations, which is just crazy, but thanks to playtesting, we have now settled on something that works.

**Tomasz Stachowiak:** Speaking of repurposing the game's tools, a great example from the playtesting phase was when one player used a bunch of lanterns – or more precisely, their wooden elements – stacked on top of one another to create something that resembled a wooden wall. Another instance was when it was discovered that if you align the stairs just right, they kind of look like machicolations in a wall, which prompted us to include a proper way to add machicolations.

**Anastasia Opara:** Another example is bridges, which were not planned at all in the beginning. But so many people wanted to make them that we thought, "Okay, how do we make bridges?" This actually evolved into a whole system for elevating buildings. Now, everything is kind of in 3D rather than 2D because the original design was that everything would just stick to the terrain.

Luckily, when the new functionality was added to Tiny Glade's procedural systems, nothing exploded, so we were like, "Cool, you can have bridges and other cool things." But then it kind of became, "Now that we can elevate buildings, they need to be supported. What if they overlap?" It's a very iterative design process.

***Now that we're discussing proceduralism, could you please tell us more about your experience as a Procedural Artist?***

**Anastasia Opara:** When I was counting recently, I realized it's been almost a decade since I started doing procedural art. I still remember one of my first generators when [80 Level wrote an article about it](https://80.lv/articles/realistic-procedural-architecture-for-games/). I felt so flattered. "Oh my God, I was recognized. That's super cool." I think it was a Chinese building generator or something like that. Then there was a lake houses generator, and now it's Tiny Glade, and all these experiences slowly add up, it's like everything you learn in the previous step gets you a little higher.

Tiny Glade actually started as a hobby weekend project to test rendering, but I needed something in the scene. So I was like, "That's cool, I can actually do procedural generation on the GPU and in real-time rather than offline," and it evolved into a whole game, which now encompasses so much more than the original small prototype.

***Some people compare procedural generators to generative AI where "you press a button and everything is done for you." In your opinion, is this comparison fair?***

**Anastasia Opara:** I think it depends on how you interpret it. For me, procedural art is very intimate because I create every single rule that goes into the system. In Tiny Glade, everything was hand-crafted by Tom and me, and therefore, we curate exactly the experience you will get out of it. I think that is quite different from what is now traditionally seen as AI, where you just press a button and a huge neural network spits something out. That, I think, is the core difference.

***If I remember correctly, Tiny Glade began as a simple procedural wall generator, could you please tell us more about the early days of the project?***

**Anastasia Opara:** During the early days of Tiny Glade, I was still working full-time at Embark Studios, so it was just a hobby side project born out of the desire to learn more about rendering. The first prototype was built using Bevy Engine because it was – and still is – the biggest Rust-powered engine, yet it had additional constraints that pushed me to start writing my own rendering solutions just to understand how it's done. It was super fun and a little bit exhausting in the beginning because when you have a full-time job and work on a side project at the same time, you really need to carve out a lot of time for it. I was waking up at 4 AM just so I could get something done before the actual work started at 9.

I was actually surprised that people liked those first tweets I made. It continued evolving from there, and we started talking, "Hey, what if it could be a game?" We needed to test whether it could be, so we made a TikTok account to show Tiny Glade to people who were completely not into gamedev. We thought that maybe people were impressed because it was technically impressive but they wouldn't want to play it. So we made a TikTok account and started posting there, and that's when the project picked up a lot of interest and we understood that this could actually be a game.

**Tomasz Stachowiak:** At some point, we were a bit surprised as to why people wanted to just play a game where you draw walls. But if we look back at those old videos, there was indeed something slightly enchanting about those procedural walls that would just rearrange themselves. It's kind of satisfying, and I think that out of all the elements that we have been adding to Tiny Glade, this one is the most vital. It's just tangibly pleasant to watch something being built up in front of your eyes.

**Anastasia Opara:**I think, in a way, it's the same visceral pleasure as when the game recognizes dialogue options or remembers that you romanced this character, became enemies with that character, and acknowledges this combination. The same feeling that the game pays attention to you and cares about what you're doing, generating this feeling that all those elements are coming together just for you in this moment on your whim.

***Why did you decide to leave Embark Studios and the AAA industry and follow the path of an Indie Game Developer?***

**Anastasia Opara:**I think I always wanted to make indie games, something personal and intimate but in the form of a video game made for others to enjoy and, hopefully, bring smiles to the players' faces. Even when I entered the industry, I remember talking to my mom and showing her Indie Game: The Movie. She asked, "What do you want to do?" and I was like, "That!" and she was like, "Yes!" She was very supportive. But it was always this drive, this passion, that made me want to create something and make it the best I could. For me, it didn't matter whether it was in the context of AAA or indie, it was about the desire to use my skills and creativity to the best of my ability.

***Now, let's discuss Tiny Glade's engine. To this day, many people still don't know which game engine you're using, so could you please tell us more about Bevy, Rust, and proceduralism in general?***

**Tomasz Stachowiak:** The entry point for us was the Rust language, since by the time Anastasia started working on Tiny Glade – before it was even called Tiny Glade – we were both into Rust, using it daily for our jobs. I also had been an early adopter of the language many years before that, so we were already hooked on just how simple it is to mix and match components of the system and how easily you can write code. That's one of the reasons why we decided to stick with this technology. Also, it's very ergonomic, doesn't crash in your face, and just feels like a breath of fresh air compared to something like C++, where you usually have to write everything from scratch.

And when it comes to the engine and the tech, Anastasia started with Bevy because it was the easiest thing to jump into, and we're still using a modified version of Bevy to this day. Technically, at the base level we have the framework called the ECS, or Entity Component System, which is the way to define the game objects and how they work, basically the lifeblood of everything happening within the game. Initially, Anastasia's prototype was using Bevy for everything, including rendering, but eventually, our needs outscaled what Bevy could provide at the time, as the need for the project was to have prettier graphics and better procedural generation on the GPU.

**Anastasia Opara:** During the early days of Tiny Glade, I was just using Bevy and writing in OpenGL, which I chose because there were tutorials for it that were very understandable. Vulkan seemed to be more complicated at the time, so I focused on OpenGL just because I wanted to learn how the things I have in geometrical representation are seen on the screen.

**Tomasz Stachowiak:** When the project started growing and we began working on it full-time, we knew that we could not use OpenGL because, with Vulkan, for example, you get the Validation Layers feature, which, when enabled, points out if you do something wrong, allowing you to easily comply with the API's requirements and specifications. OpenGL has a slight semblance of that feature, but you often run into traps, which is hardly surprising considering that it's an API that has evolved over decades and is absolutely enormous.

Within this monstrosity of an API, there's a very narrow path you're supposed to follow to have good performance on modern GPUs, so, it's very difficult to use in practice because you need to know exactly what to use, and if you stray just slightly from that path... Well, let's just say that it might work on your computer, but it's going to crash and burn on others. This difficulty extends to all levels of interaction with it, including the shading language. So, having used OpenGL for years before, I knew that it was not shippable and that it would explode in our faces. The only solution was to move to a more modern API, and eventually, we chose Vulkan because we also wanted Tiny Glade to work on Linux and be cross-platform in general.

**Anastasia Opara:** We also needed a lot of compute shaders, and at the time, it was not possible with Bevy. Thanks to the transition to Vulkan, we were able to control pretty much the whole pipeline, all the way from authoring textures and assets to how you ultimately see them in the game, all of the rendering passes, and all the generation of the CPU and GPU. So instead of prioritizing the limitations we have to work with, we could think about the target experience and how everything should look and feel to then design a pipeline that would support doing that.

Sometimes people ask, "Is it just one algorithm that has everything?" But the reality is that there are a lot of algorithms and generators, each tailored to a specific element of the game and how it should behave. For each of these elements, we've designed a pipeline that supports creation, assembly, morphing, or deforming – whatever it takes to achieve the desired look.

***And would you recommend using Bevy as the go-to game engine for beginning Game Developers?***

**Tomasz Stachowiak:** It's a pretty tough one because Bevy isn't just about Bevy – it's also Rust, which has a bit of a reputation for being difficult to learn. There's no denying that we're biased here because we really like the language, and Anastasia managed to learn the basics and become productive with Rust in two days, so the experience may vary. If you're not scared of heavy engineering, it might be a good choice for you.

However, it's important to note that, much like Unity or Unreal Engine, Bevy specifically caters to a particular subset of games. Before choosing an engine, you probably want to figure out what kind of game you want to make first. From there, you'll want to find the optimal technical solution to allow you to realize your specific game desires. In our case, the game is extremely systemic and relies on some pretty heavy engineering for those procedural generators to be orchestrated and working like clockwork. Rust and Bevy are perfect here because they give us the precision we need to engineer everything the way it needs to work without any complications or crashes.

***Could you please tell us more about Tiny Glade's gameplay features, what makes the game fun for the players?***

**Tomasz Stachowiak:** We wanted to ensure that Tiny Glade doesn't try too hard to engage players, as it can become a bit annoying and derail them from the storytelling. We aim to give players space to immerse themselves in a virtual game environment, feeling like it's their own cozy retreat where they can relax and unwind, which is very different from classical action-based games that are constantly trying to feed the player one event after another, viewing moments when nothing happens as failures of game design.

Tiny Glade takes a different approach; we don't artificially inflate events. Instead, we provide players with tools and let them have fun, akin to giving a child a bunch of LEGO bricks and waiting for their creativity to ignite. We don't want to hinder our players once they're "in the zone", our role is to ensure that everything flows smoothly and there are no bugs, glitches, or weirdness to ruin the experience.

**Anastasia Opara:** And speaking about the "child with LEGO bricks" metaphor, our role as Tiny Glade's developers is to provide players with the right LEGO pieces that would serve as entry points for you to start engaging in the storytelling. And that is the idea behind all of the building tools in our game because we validate them on how many stories they can tell.

**Tomasz Stachowiak:** The same applies to the game's Glades, which have different themes and seasons and feature various starting buildings designed to show you a few extra building elements that maybe you have not seen before, as well as to create a specific feel in each Glade.  

***With Tiny Glade being one of, if not the most anticipated cozy game in the market, could you please share your thoughts about the "cozy games" genre as a whole and why you went for it in the first place?***

**Anastasia Opara:** It was decided quite early during the prototyping phase to make Tiny Glade a cozy game. The inspiration came from me personally enjoying a lot of cozy games at the time and liking the direction where they were going. I played games like Townscaper, Unpacking, and A Little to the Left, and all of those games felt so different from regular games. They were very uplifting and kind experiences, and maybe at that time of my life, it was important to have something like that. The feeling that they gave you was very warm and sweet, almost reminding me a bit of the fuzzy warmth after watching a Ghibli movie.

I think when we were beginning to work on Tiny Glade, it wasn't like we wanted to write a thesis on how to make the coziest game ever, but the game itself naturally lent itself to go in that direction. And we were also trying to convey that in our TikToks saying, "Hey, it's going to be a cozy game. There's not going to be combat or management pressure there." And a lovely bonus of developing a cozy game is when you share something about the game on Twitter, someone would always say in the replies that it brought a smile to their face just to see a sheep on an umbrella or something goofy like that, and it's so heartwarming. We're just grateful to have an opportunity to work on a game like Tiny Glade.

***These days, with major publishers closing studios left and right, the decision of whether to go solo or partner with a publisher is a major headache for many indie developers. Could you please share your perspective and explain why you chose to self-publish Tiny Glade?***

**Anastasia Opara:** Since Tiny Glade is our first video game, we decided quite early that we wanted to self-publish it, and there were two significant reasons for that decision. One reason was simply that we wanted to learn what it's like to publish a game, so that in the future if we were to work with a publisher, we could better understand what they're doing. The second reason was that we wanted full control over the game – when to release it, what aspects to focus on, etc. We also aimed to gain the necessary experience through this process, which would help us make informed decisions in the future regarding whether to self-publish again or collaborate with a publisher.

**Tomasz Stachowiak:** Our previous experience working with the AAA industry, where you simply do your job without much say in what happens, has also played a part. We wanted to be the opposite of that, to create our own thing. Self-publishing was a path for us to get this full creative control without anyone else watching over our shoulders and telling us, "No, you have to do it like this. You have to make it more marketable. The sheep needs to have this specific hat" – requests that don't necessarily vibe with us.

***At this stage, is there anything you could tell us about your future games?***

**Tomasz Stachowiak:** Right now, our minds are completely in the land of Tiny Glade. While we do brainstorm all the time and have lots of ideas floating around, they're just text notes and concepts. We do plan to make more games in the future, but we're not sure what they will be. We have many competing ideas that we'd like to pursue, but it's not clear which ones we will go for first, the Dark Side clouds everything.

***Is there any news about Tiny Glade's release date?***

**Tomasz Stachowiak:** As of right now, we don't want to come up with any specific date because we're still learning the ropes. We sort of have a feeling for when it might be released, but at the same time, we don't know what kind of events might pop up and what could take longer than we anticipated, and we just don't want to give people false hopes only to later apologize for shifting deadlines or feeling overwhelmed.

**Anastasia Opara:**We want to be fair with the expectations of people who are waiting for the game, but also fair to ourselves and not put ourselves in a position where we have to do something that we don't think is a good thing to do. But as soon as we have a date we can confidently stand by and a finalized product we're proud of, we'll certainly update everyone.

### Anastasia Opara & Tomasz Stachowiak, Developers of Tiny Glade

#### Interview conducted by Theodore McKenzie### [Art: Francisco Rivas](https://80.lv/talent?utm_source=website_80lv&utm_medium=presale-banner&utm_campaign=Talent_LP_Promotion_for_Artists-Q3-23)

[

Your Best Job Hunting Tool is Here

](https://80.lv/talent?utm_source=website_80lv&utm_medium=presale-banner&utm_campaign=Talent_LP_Promotion_for_Artists-Q3-23)

### People Are Using Garry's Mod to Circumvent the UK Censorship Law

A chain is only as strong as its weakest link.

### 11 bit Studios Faces Investor Backlash Over $12M Canceled Game

Project 8 cost nearly $12 million, and eventually quietly vanished.

- [News](https://80.lv/articles/news)
- [News](https://80.lv/articles/news)

### Hollow Knight: Silksong Launches to 500K Players & Even Pirates Skip Piracy

Even Steam went down.

### CDPR Once Again Reiterates That The Witcher 4 Won't Look Like Its Demo Showcase

"We took a lot of lessons from the Cyberpunk launch."

- Dragon VDM Brush Part 2
	> by Nicolas Swijngedau
	> 
	> Perfect to speed up your dragon creation! Get your horns, scales and spikes while they are flaming hot!
- Ornament Brushes/Alphas - Vol.2
	> by Jonas Ronnegard
	> 
	> An Ornament alpha/brush set for ZBrush, Substance Painter, Quixel DDO and NDO etc. 55 brushes and height/alpha maps, all 2048x2048 16bit in Tiff, Jpeg, PSD, Photoshop ABR brushes, as well as ZBrush Brushes.
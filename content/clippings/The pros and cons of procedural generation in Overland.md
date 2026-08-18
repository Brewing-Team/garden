---
title: "The pros and cons of procedural generation in Overland"
source: "https://www.gamedeveloper.com/design/the-pros-and-cons-of-procedural-generation-in-i-overland-i-"
author:
  - "[[Joel Couture]]"
published: 2016-05-03
created: 2025-09-27
description: "\"There are a few things that we get from procedural generation: more emergence and unpredictability, as opposed to being a roller coaster for the player to only experience the things I wanted them to feel,\" says dev Adam Saltsman."
tags:
  - "clippings"
---
"There are a few things that we get from procedural generation: more emergence and unpredictability, as opposed to being a roller coaster for the player to only experience the things I wanted them to feel," says dev Adam Saltsman.

11 MinRead

![Game Developer logo in a gray background | Game Developer](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/bltba62518415cda0e2/652fe6ddbc479f8697ef691f/default-cubic.png?width=1280&auto=webp&quality=80&format=jpg&disable=upscale "Game Developer")

Surviving is about facing the unknown. So in creating a game of tactical survival across a ruined continent, [Adam Saltsman](http://adamatomic.com/) of [Finji](https://twitter.com/FinjiCo) turned to procedural generation to ensure that no two situations would be alike.

The game is question is Overland, which launched a [limited paid alpha](https://killscreen.com/articles/overlands-post-apocalyptic-dioramas-arrive-early-but-only-for-some/) late last month. Procedural generation in the game give the players a constant sensation of coming across something new while putting their survival skills to the test.

"I think as a player, I like the feeling of 'no one has ever seen this before,'" says Saltsman. "But also the kind of consistency and the metagame of learning rules and formulating strategies outside of any given particular arrangement of obstacles. Putting players in a place where they are always kind of racking their brains and thinking laterally and coming up with neat solutions to problems no one has seen before, I like how that feels."

When it is done well, procedural generation is a good method of assuring players will consistently be met with new situations in which to apply knowledge of the game's systems. When it isn't, the player may become bored, confused, or find their car stolen by dogs. Procedural generation is an excellent tool for developers, but one that will requires a lot of work to get down just right.

![](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/blt040c21aec18e8428/650e68f3abaf876f5b5b75a0/overland_mar2016_5.jpg/?width=646&auto=webp&quality=80&disable=upscale)

## Why choose procedural generation?

"I definitely have a soft spot for the kind of "shuffle the cards, see what fate deals you" type of feel. To see how random you can keep things and still be fun -- how close can you get to the sort of scary real-life background radiation of the universe." says Saltsman.

Variety is an excellent thing for players. Many players enjoy the sensation of stumbling across something new and using their intelligence and skills to figure their way through it. It is a big part of the excitement of a new game, but in using procedural generation, the player can have that new game experience every time they start up a game they've already been playing for hours, days, or months.

"We (if we do it right) get a kind of limitless well of 'content' and avoid at least SOME of the harder-to-scale labor of producing an adequate amount of hand-made scenarios."

This can result in those key moments for players that become their own. A random situation can easily become the story a player shares when they talk about the game to other people. They won't just be relating the same scripted moments all players would be talking about in a linear game, but rather that unique moment, where all of the generated content comes together in just the right way, that it creates something personal and memorable for the player.

"There are a few things that we get from procedural generation: more emergence and unpredictability, more unique situations that players feel like they 'own' in some way. I think we get a more consistent world that follows a kind of ruleset as opposed to being just a roller coaster for the player to experience just the things I wanted them to feel."

Players want many different things from their games. Many different kinds of gameplay moment will be special, and procedural generation is a means for the developer to let go, letting the systems they've designed work together in their own way to create moments the developer may not have even thought to make. No developer can consider everything a player would want with the stages and areas they design, but they can provide the tools where something truly unique and special may occur.

![](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/blt3f398b6537bf9ed9/650e6938fb31b5078363c3eb/overland_mar2016_7.jpg/?width=646&auto=webp&quality=80&disable=upscale)

## What could possibly go wrong?

"There are only about a billion potholes on the way to achieving this." says Saltsman.

Without a dedicated set of rules in place, procedural generation can create some real messes. It can create stages that are too hard, stages that are too easy or plain dull, stages that feel like repeats of each other, or just otherwise create an array of flavorless or frustrating experiences. Without the developer's hand to guide a stage, it can just be a pile of random parts with little means of engaging the player.

As with any bit of programming, developers also run the risk of it working in ways they didn't intend or expect. Some of these might make the game less appealing to its potential player, or create ridiculous situations in otherwise-serious games. These aren't necessarily bad things, as Saltsman found with one particular unexpected situation in Overland.

"In Overland, we have a lot of modular and shared behavior. We have a (work-in-progress) AI that controls strangers you encounter that aren't really looking to join your group. They're just scavenging and going about their business. And if you give them a hard time, they will take as much fuel as they can and hijack your car and leave you stranded. Which is fun, it's easy to program and it suits the story world and all that. And it's something that most games don't do."

" Overland also has dogs in it, because dogs are great. And we treat dogs MOSTLY like people, so sometimes you can meet a stray or feral dog that just wants nothing to do with you. SO a thing that used to happen from time to time is you would bump into a wolf in the wild somewhere, and it would hijack your car and peel out, which was pretty great." says Saltsman.

Fun issues like this can occur, but there is still a quagmire of things that can go wrong without carefully crafting your procedural generation. At times it may be entertaining, but in others, it can put the player off your game with a few poorly-chosen creations.

![](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/bltf7ed80435c791b85/650e693beb6464096e445722/overland_apr2016_2.jpg/?width=646&auto=webp&quality=80&disable=upscale)

## Getting it right

Saltsman gave his procedural generation system a ruleset to help keep it interesting for players. In doing so, he preserved the variety of options the game could create for survival situations while also keeping the game engaging and balanced.

"We wrote a set of about 20 constraints or rules that mimic the rules we were using to create hand-placed levels. The result is a kind of AI or designer-clone that is able to shuffle through all the different parameters at hand and produce a level that is interesting and hopefully appropriate to the player's expectations."

Still, that might not have made for a very compelling game if he hadn't developed enough interesting scenarios, both visually and through gameplay goals, to keep a player invested. A great deal of work went into ensuring there was a lot of elements the procedural generation could pull from so that variety would be meaningful. If a game only has a handful of possible variations, then procedural generation loses its usefulness.

"The other thing that helps address a lot of the potholes is to have a TON of ingredients but only ever deploy them in subsets. Spelunky is a fantastic example of how to do this super effectively. Definitely a big inspiration to us even though we're doing more of a tactics thing."

By keeping certain aspects tied into each other, the developer can assure that they will always be relevant and interesting to the player. If they're put together with no specific ruleset, the game can become a mish-mash of varied parts. With very specific rules, you ensure you game can create many different situations while staying appealing to its audience.

It also helped to create several smaller goals for the player to accomplish along the way to completing their journey to California. By adding in smaller goals, it helps keep the player's goals varied, so that each map can have a specified goal, but also because it breaks the end-game goal of a given area into a smaller chunk.

All maps serve the goal of reaching the end point (California), but can do so in different ways (getting a better car, finding survivors, getting equipment) that make it easier to create meaningful, different areas. Not every stage is beaten by doing the same thing, and so it creates opportunities for the player to create their own goals in a given area based on what they need. This adds more opportunity for unique experiences in a uniquely-created area.

Getting all of these elements right has been a constant process, but also what will make Overland worth playing upon completion. "Tuning the parameters that go into the generation AI is a constant process, because that's what produces balance in Overland and keeps the pressures and tension on the player interesting and compelling." says Saltsman.

![](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/blt1d51b2d73ad627ae/650e6925ab6e8f653214a24a/overland_mar2016_6.png/?width=646&auto=webp&quality=80&disable=upscale)

## Do's and Don'ts

While iterating procedural generation for Overland, Saltsman has found a few handy pieces of advice for developers looking to implement such a system.

"Don't discount pure visual variety. Even if it doesn't change the mechanics or the gameplay, it does change the sense of discovery / exploration for people." Visuals provide an entirely different experience for some players, and that first sense of discovery in many games comes from simply finding a place that looks different.

"Depending on the game, it may help to try to come up with different "mid term" player goals, and generate different sorts of levels around those encounters." says Saltsman. With these, you get smaller goals that create more variety within each individual map. It can help a place that looks similar play differently due to having a completely different gameplay goal.

"Be careful about flatness. It's very easy to accidentally water down your different goals in an effort to 'balance' things. Keep 'em spiky." Balance is important, but if all elements are balanced too much across the board, playthroughs can feel similar. By creating unique elements to each goal, even if they feel somewhat unbalanced, it can draw a player to try new ones out based on their unique problems and bonuses.

![](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/blt81417936ec1b4e61/650e6926af5d1a43d4583d48/overland_apr2016_4.jpg/?width=646&auto=webp&quality=80&disable=upscale)

"Don't throw TOO Much at the player at once. People can handle like 50 instances of 5 different types of things, but they can't handle 10 different types of thing." That variety that makes procedural generation seem so appealing can throw too many elements at a player at once, overwhelming them with information. This can feel daunting, turning players off of the game or making it too hard to focus. Many different elements can be great, but it's better at some times to have a strong, smaller set than a large one.

Also, from the development side, it's important to not get discouraged due to the nature of programming for procedural generation. "There's a WEIRD curve to doing a game that relies on procedural generation pretty heavily. For us, the curve was basically that we made a ton of progress really fast and then plateaued for like...a year or more." says Saltsman.

"It goes fast at first, because you don't have a lot of different ingredients yet. And then you have to start kind of tackling all these medium / large questions about the systems you're building and why you're building them and how should they be tuned and what does it feel like when X, Y, and Z change over the course of 3 hours of playing the same save etc. And you're just fiddling with different floating point numbers and integers for like 12 months. But eventually, you'll rediscover the secret sauce and then you will know what it is to feel happiness again."

Perfecting the elements you've put in place can be far more time-consuming than creating them to begin with. It will be a long road to getting it all down right, one that can be discouraging for a developer. It can feel like you're just puttering with small details for months. Still, it will pay off with time.

![](https://eu-images.contentstack.com/v3/assets/blt740a130ae3c5d529/bltddc0d69cf81f1bcf/650e692a3e7aac6dc1640753/overland_apr2016_3.jpg/?width=646&auto=webp&quality=80&disable=upscale)

## Endless adventure

Procedural generation can create many issues and pitfalls in your game, making it too boring, varied, complex, or strange. Even so, with some hard work, it can create endless unique moments for your players to discover, challenging their knowledge of the systems you've put in place rather than their ability to overcome a scripted encounter. It can create exciting memorable moments the players will talk about with their friends, all of which are unique beyond anything a developer could dream up.

Depending on the game you wish to create, or budgetary constraints, this tool can help create endless replay value and take some of the pressure off to create dozens, or hundreds, of hand-crafted levels. With a clever ruleset and a dedication to examining the systems you've put in place, you can make something that provides endless adventures and complexities for players to overcome.

## About the Author

Contributor
---
title: The Journey of Developing Catherine-Chan
date: 2024-10-29
description: "A reflection of the development of Catherine-Chan"
tags: ["discord-bots"]
draft: false
cascade:
  showReadingTime: false
---

If you don't know, [Catherine-Chan](https://github.com/No767/Catherine-Chan) is one of the projects that I have been developing for some time now.
In a nutshell, Catherine-Chan is designed to help out the LGBTQ+ community by providing resources and a toolkit for those who need it.
In fact, the whole reason why I built this bot in the first place is seeing the amount of lack of LGBTQ+ focused bots, and to directly
compete with one of my friend's PrideBot. Because of this, the journey of getting to where the bot is now has been a wild one.

## The grassroots

I started Catherine-Chan around August 2023. I had just moved into my college (UC Merced) for the first, and wanted to do something so I wouldn't become
bored. One of the ideas at that time was to build a pride bot of my own. I previously looked into the codebase of my friend's bot and I was just horrified by what I saw.
Even though she was self-taught, there were so many poor practices everywhere, and worst of all, the codebase was poorly maintained. That bot just so happened to be in
100+ servers at that time. I felt like I needed to make one that would outshine my friend's bot.

The name of Catherine-Chan came from the fact that the honorific ちゃん (chan) was used pretty heavily in some parts of the community. Catherine itself was basically
a name I came up on the spot. I designed it this way so it wouldn't be another "PrideBot" or "LGBTQ+ Bot" name clone.

## v0 Development

The initial versions of Catherine-Chan, v0, are the versions with probably some of the worst code that I myself also produced.
The major issue that I had in comparison was I had this guiding philosophy of each extension file would be "free" of
any code that doesn't have to be directly included. So I basically started the whole system of creating different packages just
to store my code that way. For example, if I had a extension that would be focused on the dictionary commands, any utils would be shoved
under `lib/cog_utils/dictionary`, and so forth. As I learned later on, this basically makes it nearly impossible to maintain.
If the code of the `cog_utils` changed, I would have to restart the bot constantly in order to reload it. Later I learned that
this is basically extremely foolish in the first place.

There were multiple releases that had to fix a bug caused by a previous release, and errors would be a common eyesore on the logs.
I would check the logs once in a while, and see like the time a week ago when someone tried to use my bot but the commands
straight up failed. Either it was the custom subclass of `discord.ui.View` failing, or something timed out and I had literally
zero ways to trace it down in production. Although I did unit test, I was just too hyperfocused on writing tests that would basically
give me 100% coverage rather than actually testing the code thoroughly.

During this stage, in order to better combat usage, Prometheus support was added, and a Grafana dashboard was set up. 
This would be critical in the future as this allowed me to remotely monitor, and aggregate metrics that would be critical for determining feature usage and overall growth. 
No personal data has ever been tracked, and if you looked into the source code for PrideBot, you will see that the information of new guilds 

This was the first ever successful bot that I ever wrote, but soon the technical debt would pile on more and more

## v1 Development (Rewrite)

As more and more parts of the code became outdated, and unmaintainable, this is where I started to more or less decided to rewrite parts of Catherine-Chan on my own.
The method here was to merge all of the `cog_utils` packages into their respective cogs, and the UI components as well. If a prompt was needed, a
standard prompt function was used to generate one, which was included in `libs/utils/view.py`. This essentially put parts of the code to where it neededto be at.
It was basically with the extension itself, which allowed for easy reloads, and much more stronger code.

During this process, most if not all of the core features was rewritten. The prometheus exporters, the blacklist system, and many more.
While this was also going on, proper unit testing was starting to take shape. Previously, I only did unit testing in order to chase the goal of 100%
coverage on the codebase, but this time I didn't bother with that. Instead, I only tested util methods found on the cog subclass directly.
This effectively cut down on how much tests would need to be rewritten, and only tested what I actually needed.
On top of all of that, I only tested four extensions, which are the dict, hrt, pride profiles, and pronouns extensions. Based off of the 
command count usage that the metrics was telling me, I knew that testing those four main extensions would be critical as most people used them.

Ever since finishing the rewrite, there has been no errors and the ones that have been addressed are resolved.

## The future

The current future for Catherine-Chan is that I'm still maintaining it. I'll still be hosting it for the next coming years, but not actively adding
new features as often as before. I've decided to shift my time and effort into my personal life where I have tasks to take care of.
This doesn't mean that there will be no features for Catherine-Chan. After all, this project is designed to be contributed to.
You can always join the support server and suggest a new feature, or directly make a PR into the repo for whatever feature you want.
It's just that moving forwards, I will be slowly moving away from the Discord bot community and focusing on what's really important to me.

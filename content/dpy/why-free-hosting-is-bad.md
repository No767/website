---
title: "Why Free Hosting is Bad"
date: 2024-06-27
description: "Helpful explanations and thoughts on why free hosting services are bad"
tags: ["discord.py"]
cascade:
  showReadingTime: false
---


{{< alert "check" >}}
This post was originally written on discord.py server, but an in-depth version was created on
Github Gist ([here](https://gist.github.com/No767/0a523ea6cd8e44210e131f5fc1aa570a)). This gist has
now officially moved to this blog space.
{{< /alert >}}

When looking for hosting your bot, free services and/or providers that claim to
support hosting Discord Bots. **Do not** use them. Why? Let me explain.

## Drawbacks

Free hosts are providers who specialize in offering an free platform to host projects.
These providers typically aim to incentivize users who simply can't afford proper hosting
or for people who don't know better due to inexperience. Now the points below will discuss
motivations, and the costs that burden developers who are looking for hosting.

## The "Gotchas"

Providers who offer an free tier typically look for users to onboard to their platform.
These are usually in the forms of an free tier with limited options, or an 30-day upgraded tier. With limited options, and when you invest into an platform, vendor lock-in
is in effect. In addition, you are forced to pay for this service that offers limited control, thus making it extremely hard to break free of this cycle.
Examples of these limited options include:

### Poor Specs

These hosts tend to list very poor computing specs in order to reduce production costs.
This directly affects your bot as most notably, slow bandwidth, frequent system instability,
lag all can pile and cripple the ability for your bot to operate. Examples of these include:

- Shared IPs
- Shared CPUs
- Shared and/or low memory counts

Touching deeper with shared IP addresses, they pose an risk of incurring ratelimits and potential Cloudflare bans.
When an service runs an large amount of bots on one IP address, all of the those requests to Discord are sent so frequently that ratelimits trip,
resulting in the infamous HTTP 429 error. If this continues in an sustained matter, then Cloudflare would issue an temporary ban. This usually
cripples an bot's ability to interact with Discord.

### Limited Control

Some hosts abstract concepts of server management through the usage of administrative dashboards. These can be custom, or utilize Pterodactyl,
which itself has many known issues. With these limited controls, your ability to debug and/or provide information critical for debugging are obfuscated.
Not only you lose the ability to debug, but your control on operations. It's simply not worth to lose this ability for convenience,
and better to invest time in learning basic Linux commands and concepts.

### Economic Competition

Chances are, there are a lot of these providers out there. By offering lower prices and free tiers, businesses aim to reduce total production costs and invoke competition.
Hosts are really just business entities, and in order to be successful, an business must either break even or make economic profits in the short and long run.
This is simply how the market operates. Be aware of this as they use an variety of tactics in order to grab the attention of developers who are desperate for hosting.

## Implications of Poor Hosts

As discussed previously, these poor hosts can usually cause issues
in the short and long term for developers. There have been stories of
adolescents in various parts of the world where they simply cannot afford
the costs of renting an server from an VPS provider; thus allowing this market of free
hosts to unknowingly exploit vulnerable individuals and scam them from their limited financial situation. As a result, they also rely on those who are not knowledgeable with
good Discord bot hosting practices, thus falling into this pitfall as well. Either way,
these hosts usually offer such a poor quality of service that it could be considered
an scam operation.

## Options for Finding Good Hosts

Even with an limited finical situation, it is still possible to find and utilize
good reliable paid hosts for your bot. Below are options that should be considered.

### Invest in an Reliable VPS Provider

This is by far the most widely recommended option, which in short, is to pay up
and use an reputable, reliable, and community vetted host. [Henzter](https://www.hetzner.com/) is one that is strongly recommended for their trustworthiness and reliability, but other good options exists. An list of these are included below:

- [Scaleway](https://www.scaleway.com/)
- [DigitalOcean](https://www.digitalocean.com/)
- [OVH](https://www.ovh.co.uk/)
- [Time4VPS](https://www.time4vps.eu/)
- [Henzter](https://www.hetzner.com/)

Your options are not only limited to VPS providers, but big cloud providers would also work. [Microsoft Azure](https://azure.microsoft.com/en-us),
[Google Cloud Platform (GCP)](https://cloud.google.com/), and [Amazon Web Services (AWS)](https://aws.amazon.com/) all offer student discounts or reliable semi-free options for their services. These options are more than likely what you would have
to choose if you are not an eligible high school or university student.

### Self Host

If you are able to self host your own server, then this is an
recommended approach. You still would have to pay for internet and electricity
but generally this is the only recommended "free" way to host your bot.
Raspberry Pis are good for this task, especially for lighter bots.

### GitHub Student Developer Pack

**IF** you are a enrolled student in an accredited high school or university (you will need to either provide an valid student ID or proof of education), then you may apply for this deal. The Github Student Developer Pack offers tools and services for young
developers that are valuable and is really a free deal for students. More info about this can be found [here](https://github.com/orgs/community/discussions/17814). The deal offers $200 free credits on DigitalOcean for 1 year and credits for Azure as well.

---
title: "An Primer on Syncing"
date: 2024-06-27
description: "Helpful explanation about syncing"
tags: ["discord.py"]
cascade:
  showReadingTime: false
---

## Context

When Discord rang the bell on a [new era](https://discord.com/blog/welcome-to-the-new-era-of-discord-apps), this came with a tidal wave of new features. Buttons, dropdowns, modals, and most importantly, slash commands. 

Unlike prefixed commands (e.g `?help`), slash commands are entirely handled by Discord. As a result, in order to let Discord know of new changes, discord.py performs a process known as syncing. 

### Guild or Global?

Slash commands are scoped to either be global or guild-specific (they cannot be both). To clear the confusion, both are explained below:

- **Guild-specific**: The command that is scoped to this can only be found on the guild that it is scoped to. For example, if I have the command `/ban-user` and it is scoped to the guild `12345`, then the `/ban-user` command will only be on the guild `12345`.
    - Only use this when you want to restrict a command to a set of guilds

- **Global**: The command can be accessed regardless of server. These commands can also be accessed in DMs.

In essence, most commands should be scoped globally but in some cases, it would be better to have it guild-specific (usually this is very rare).

## What is syncing?

When you need to let Discord know you have changes to your command, this is where you "sync" the tree. Behind the scene, discord.py represents commands as a tree (thus the name `CommandTree`). It may be helpful to visualize it as shown below:

```
{
  None: [global, commands],
  guild_one: [guild, one, commands],
  guild_two: [guild, two, commands]
}
```

*Credits to sgtlaggy*

This tree gets used to build an index of what slash commands you currently have, and is used to later sync those commands to Discord.

## How do I sync?

What is recommended is to maintain an sync command as a prefixed command. Bots without the message content intent will still receive content of messages that mention them or are in DMs. You can't use a slash command to sync when the sync command itself is not synced.

Luckily this message command can be found [here](https://about.abstractumbra.dev/discord.py/2023/01/29/sync-command-example.html) and can be easily copied and pasted into your bot in order to sync (note that Rodhaj already includes this command). It is recommended to read the bottom half of the post in order to figure out how to use it.

## Why sync manually?

In some other forks, this process is done automatically by default. You may think this is a good thing, but it's not. You trade conveince for a rabbit hole of issues, hours of complaining, and frustration on why your commands didn't magically appear in the UI. In fact, it's a footgun in disguise. The reasons can be summarized in the following points.

1. **You only need to sync when commands are updated**

    As syncing is a process requiring making API calls to Discord, Discord heavily enforces strict ratelimits for the endpoints used to sync. The practice of auto syncing leads to HTTP 429 errors (case and point, look at the amount of help posts on the official discord.py server that have 429 errors caused by auto syncing), and if severe enough, leads to a Cloudflare ban. By auto-syncing, you essentially make wasted API calls, and this whole ordeal can be avoided if you manually synced instead.

    This quote from `?tag ass` perfectly summarizes it.

    > What syncing does is send your commands to discord for one guild or globally. 
    > If you haven't changed your command's descriptions, added/removed commands, changed names, parameters, etc. 
    > you shouldn't sync, since you'd only be updating discord with the commands they already have without doing any changes, 
    > which is pointless and a waste of an API request to a limit with an already tight rate limit.

2. **Removing the lack of control**

    When people inject auto-syncing code (or library maintainers), they trade convenience and in return, get a lack of control.
    This lack of control over the syncing process adds a burden to how you deploy your commands, and ultimately you run into issues
    when you use this process.

    The most notable example is the case of duplicate commands. This is caused by
    having global commands synced with guild commands, thus causing "duplicates". If you did auto-syncing, then you would be freaking out how to fix this
    and Googling it up, which lead to solutions that worsen the issue.
    Now what happens if you manually synced instead? The outcomes would be much different,
    as if you used [Umbras Sync Command](https://about.abstractumbra.dev/discord.py/2023/01/29/sync-command-example.html) 
    (USC), then all you would need to run is the following:

    ```
    !sync ^
    ```

    By running this simple prefixed command, you effectively solve the whole situation.

## When do I sync?

You don't have to sync every single time. See the following for more info.

### Sync when you...
- Basic
  - Added/Removed a command
  - Added/Removed autocomplete (decorator, transformer)
  - Added/Removed an argument
  - Added/Modified/Removed locale strings
  - Converted the global/guild command to a guild/global command
- Modify 
  - Changed a command's...
    - name (`name=` kwarg, function name)
    - description (`description=` kwarg, docstring)
  - Changed an argument's...
    - name (rename decorator, param name)
    - choices (Literal, choices decorator, enum type)
    - description (describe decorator, docstring)
    - type (`arg: str` str is the type here)
- Permissions
  - Added/Modified permissions:
    - `default_permissions` (decorator, kwarg)
    - `nsfw` (kwarg)
  - Added/Modified contexts:
    - `guild_only` (decorator, kwarg)
### Do not sync when you...
- Changed anything in the command/autcomplete function's body (after the `async def ():` part)
- Added/Modified/Removed library side checks:
  - `(@)app_commands.checks...`
  - `(@)commands...(.check)`
  - `@app_commands.checks.(dynamic_)cooldown(...)`

*This is the same for hybrid app commands*

## Links

- [Umbras Sync Comamnd](https://about.abstractumbra.dev/discord.py/2023/01/29/sync-command-example.html)
- [Official Discord Server](https://discord.gg/r3sSKJJ)
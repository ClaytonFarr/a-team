# A-TEAMs : v2

*Code pending*


## Virtual group of specialized team members backed by one or more LLMs; multiple, persistent communication threads (via Discord); team behavior programmed via LangChain or something similar.

---

This version aims to realize most of the [current design concept](/a-team.md) - sans the external memory store (e.g. a vector database). I'm interested to see how much history and context might be provided by Discord message history alone. For tools, it'll be interesting to see if in addition to making tools available in backend pipelines if there are advantages to also letting the virtual team members work with tools provided by other bots in Discord channels and threads.

## Overview

- Utilize Discord for LLM communication system
- ProjectTeamLLM = Discord Bot
- Bot can instantiate virtual team members as needed
- Bot creates appearance of team members (posts from itself) as unique, multiple users
- Discord channels and thread history provide v1 memory for LLM roles
- Utilize 1 more LLMs across team members in the background as needed
- Utilize tools in background pipelines, and possibly within Discord from other tool bots

## High-Level Workflow

- Create private Discord
- Add ProjectTeamLLM Discord bot as a user
- Bot Project Manager role:
  - works with user to articulate objectives and create work plan
  - instantiates virtual LLMs (Specialists, Collaborators, etc.) as needed
- Bot sets up a structured communication system to create the appearance of multiple users; may include:
    - Using message prefixes to identify each virtual LLM (e.g., "[Specialist-A]: ...").
    - Utilizing Discord embeds to format messages differently for each virtual LLM.
    - Creating dedicated text channels for each virtual LLM's interactions.
    - Leveraging Discord Threads for organized conversations with each virtual LLM.
    - Programming virtual LLMs to mention relevant human users or other virtual LLMs when necessary.
- LLM roles send and receive messages in Discord channels and threads as needed, following the structured communication system set up by the Project Manager:
  - LLMs are able to participate in and contribute to multiple chat threads
  - LLMs are able to create and utilize pseudo saved memory through history of Discord messages


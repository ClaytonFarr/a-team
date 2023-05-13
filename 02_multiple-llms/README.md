# A-TEAMs : v2

### Virtual group of specialized team members backed by one or more LLMs; multiple, persistent communication threads (via Discord); team behavior programmed via LangChain or something similar.

**Code pending; currently planning -**

- Utilize private Discord
- Add LLM ProjectTeam Discord bot as a user
- Project Manager role:
  - works with user to articulate objectives and create work plan
  - instantiates virtual LLMs (Specialists, Collaborators, etc.) as needed
  - sets up a structured communication system to create the appearance of multiple users; may include:
    - Using message prefixes to identify each virtual LLM (e.g., "[Specialist-A]: ...").
    - Utilizing Discord embeds to format messages differently for each virtual LLM.
    - Creating dedicated text channels for each virtual LLM's interactions.
    - Leveraging Discord Threads for organized conversations with each virtual LLM.
    - Programming virtual LLMs to mention relevant users or other virtual LLMs when necessary.
- LLMs / LLM roles send and receive messages in Discord channels and threads as needed, following the structured communication system set up by the Project Manager:
  - LLMs are able to participate in and contribute to multiple chat threads
  - LLMs are able to create and utilize pseudo saved memory through history of Discord messages
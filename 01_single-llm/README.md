# A-TEAMs : v1

### A single LLM, a single thread of communication, behavior 'programmed' via chat or system message.

This approach (including the last, most concise version) does much than I originally expected – but isn't able to leverage feedback and iteration terribly well yet and has the limitations you'd expect in a single thread and context window - both of which certainly affect the quality of the work outputs produced.

It definitely has value for it's easy use with ChatGPT (as first message prompt) or with OpenAI APIs (as system message in OpenAI Playground or tools like [TypingMind](https://www.typingmind.com/)) but this approach seems to have mixed odds of actually pursuing all of the work it is meant to do.

Sometimes the LLM happily moves ahead and performs the work (especially in settings where it has access to web search) - many other times it only gets through the work planning stages and presumes work will happen by user or other LLM team members somewhere else.

As always, it's tricky to test these against one another concretely since the outputs always vary from one pass to the next. Thus far, it feels like the more condensed version carries *most* of the instruction from the longer versions (and the vastly shorter token length is a huge welcome) but it also feels like it might more readily abandon acting as the virtual team members to do the work.

For anyone else interested in trying to drive this type of behavior, it would definitely be worth doing your own comparisons of a similar request across these options to see what contrasts you see (e.g. Pass 4 v Pass 2).

Next, I'm looking to carry applicable ideas from here into [the next version](/02_multiple-llms/README.md) - that leverages multiple LLMs (virtual and actual), working across multiple, persistent conversation threads.

---

## Pass 4  :  How low can we (successfully) go?

- [System Message 04](/01_single-llm/v4.md)

Performed separate set of passes with GPT-4 to compress Pass 3 system message into something as short as possible that didn't lose meaning in the process.

…landing at less than 250 tokens 👌 (presuming it can work as well as Pass 1 which ones ≈ 10 times longer).

---

## Pass 3  :  Deterministic vs. Innovative?

- [System Message 03](/01_single-llm/v3.md)

As usual, finding that highly specific ideas often seem to hamstring an LLM's ability to be innovative. Worked with GPT-4 to convert my original long-form notes and the longer Pass 1 'program' into as short of a system message as possible. Iterated to ensure all relevant ideas are represented.

…which put us back in territory of conventional natural language prompts and under 400 tokens. 🫡

---

## Pass 2  :  How can we make this program shorter?

- [System Message 02](/01_single-llm/v2.md)

Consolidated much of the earlier explicit 'has' and 'does' from Pass 1 into a shorter narrative while retaining explicit user commands and output/print formats meant to help work quality, role feedback and context management.

…which cut things down to ≈ 1,100 tokens. 😕

---

## Pass 1  :  Let's make a LLM 'program'…

- [System Message 01](/01_single-llm/v1.md)

First approach, inspired by [AI-Tutor](https://github.com/JushBJJ/Mr.-Ranedeer-AI-Tutor) and [Bot Generator Bot](https://github.com/ruvnet/Bot-Generator-Bot/blob/main/prompts/primary_bgb.txt) examples of 'programming' an LLM to operate as a completely structured app – through an internally logical, structured set of 'has' and 'does'.

…that resulted in a system message that is over 2,400 tokens long. 🤦‍♂️


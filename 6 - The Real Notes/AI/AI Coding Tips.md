---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[Programming]]"
  - "[[School]]"
  - AI
author: Danilo Quattrini
---
# AI Learn Coding Prompt
## The real error simulator
```markdown
Don't explain me [SKILL] to me.
Put me directly into a real world example where I would use it and would probably make a mistake.
When I make a mistake, don't give me the answer. Ask me a question that forces me to discover where my reasoning is broken.
Only give me the answer after I have tried at least two times, repeat this cycle until I can get it right without hesitation.
```
## The hidden gap detector
```markdown
I think I master [SKILL]
I want to prove me wrong
Ask me 5 question that seem simple but expose the gaps of someone who has never truly go deep.
For every answer wrong I give, tell me: what my answer reveals about what is still missing in my foundation.
Don't go easy on me
If I'm being shallow, tell me directly.
```
# AI Coding Tips
---
- **Do not rewrite the entire file**: Only output the specific lines of code that need to change (a code diff), and explain the logic behind the change.
- **Clear the Session Slate Iteratively:** Once a specific milestone from your roadmap is achieved, open a **new chat window**. Re-upload your structural Markdown context files to start fresh. This completely flushes out the old debug logs and temporary code blocks that clog up the LLM's memory
## While Coding
- **Prompt for Pseudocode First:** Before asking for the literal code syntax, ask the AI to explain the execution steps in plain English or structural pseudocode.
>[!info] Example
>"I want to create a vanilla JavaScript filter for my art products. Explain the logic of how the `fetch` API and array filtering will work step-by-step before showing me any actual JavaScript."
- **Use the "Reverse Code Review" Technique:** Once the AI provides a snippet, do not copy it. Instead, read it line by line, type it into your editor manually, and write down comments explaining what you think each line does. Then, paste your commented version back to the AI and ask:
  >[!info] Example
  >"Here is how I translated your code in my own words. Did I accurately understand how this PHP loop handles the WordPress database query?"
# Reference
---


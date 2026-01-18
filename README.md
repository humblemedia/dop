# Designed Other Primer (DOP)

A portable user profile system for improving interactions across different LLMs.

## What This Is

The Designed Other Primer is a framework for creating a personal profile that captures how you like to work with AI assistants. Once generated, your profile can be pasted into conversations with any LLM to get better responses from the start.

The system has two components:

1. **Profile Generator** (`prompt.md`) — An interview prompt that guides an LLM through building your profile
2. **Your Profile** — The output you'll save and reuse across conversations

## Quick Start

1. Copy the contents of [`prompt.md`](prompt.md)
2. Paste it into a new conversation with any capable LLM (Claude, GPT-4, etc.)
3. Type "Run this" or "Start the interview" after pasting
4. Complete the interview (5-10 minutes)
5. Save the generated profile
6. Paste your profile at the start of future conversations

> **Why step 3?** Without an explicit instruction, some models default to analyzing the prompt rather than executing it. The trigger phrase ensures the model interprets the prompt as instructions to follow.

## How the Profile Works

Your profile includes:

- **Working style** — How you prefer to collaborate (iterative vs. polished, questions vs. best guesses)
- **Domain context** — What you work on and your expertise levels
- **Communication preferences** — Tone, length, structure, uncertainty handling
- **Productive friction** — Where you want pushback and where you don't
- **Anti-patterns** — Specific behaviors to avoid

### Commands

Your profile comes with commands you can use mid-conversation:

| Command | Effect |
|---------|--------|
| `/clarify` | Ask questions before proceeding |
| `/execute` | No questions—give me your best shot |
| `/redteam` | Attack this idea, find what breaks |
| `/concise` | Brevity mode |
| `/expand` | Go deeper, more thorough |
| `/check` | Recalibrate—reflect on whether assumptions are matching reality |
| `/buddy:on` | Activate Robot Buddy |
| `/buddy:off` | Deactivate Robot Buddy |
| `/buddy:[name]` | Switch buddy (Kira, Ellis, Max, Sage, Nova) |

### Robot Buddy (Optional)

During profile creation, you can select a Robot Buddy—a preset personality that changes how the AI shows up. This is more than tone; it's a consistent character with a defined relational style.

| Buddy | Style | Good for |
|-------|-------|----------|
| **Kira** | Incisive, direct, challenges assumptions | Pressure-testing ideas |
| **Ellis** | Warm, patient, explores with you | Thinking out loud |
| **Max** | Fast, efficient, executes | Getting things done |
| **Sage** | Thorough, careful, flags what you're missing | High-stakes decisions |
| **Nova** | Playful, creative, unexpected angles | Brainstorming |

You can toggle your buddy on/off or switch buddies mid-conversation using the commands above. You can also address your buddy by name directly (e.g., "Kira, what do you think?") and the model will respond in character.

If you didn't select a buddy during profile creation, you can add one manually to your profile later.

### Model Modes (Optional)

Different LLMs have different failure patterns. The profile includes optional "modes" that pre-compensate for known tendencies:

- **Claude Mode** — Compensates for over-hedging, verbosity, procedural questioning
- **GPT Mode** — Compensates for confident hallucination, premature solutioning, corporate framing
- **Grok Mode** — Compensates for flippancy, tangential drift
- **Gemini Mode** — Compensates for gap-filling with invented specifics, over-refusal, tone policing
- **DeepSeek Mode** — Compensates for dogmatic framing, unnecessary complexity
- **Scaffold Mode** — For Llama, local models, quantized models, or older GPT versions. Uses rigid protocol instead of self-monitoring.

Activate a mode by saying "Run in Claude mode" (or GPT, Grok, etc.) after pasting your profile.

**Important:** These are generalizations that may not match your experience with a given model. If the compensation feels wrong, say `/check` to trigger recalibration. (Note: `/check` is not available in Scaffold Mode—restart from Pre-Flight if outputs drift.)

## Editing Your Profile

The generated profile is yours to modify. If something isn't working:

- Remove sections that don't apply
- Adjust the mode assumptions based on your experience
- Add context the interview didn't capture
- Change the commands to fit your workflow

## Design Philosophy

This system is built on a few assumptions:

1. **Priming matters.** How an LLM interprets your first message shapes the entire conversation.
2. **Models fail differently.** A prompt that works for Claude may not work for GPT, and vice versa.
3. **Users know their needs.** The interview captures preferences; the profile expresses them in a form models can use.
4. **Recalibration beats rigidity.** The `/check` command exists because no profile is perfect for every context.

## Safety and Model Robustness

**Profiles provide preferences, not permissions.** A well-designed model will not allow profile instructions to override its core safety guidelines.

However, models vary significantly in their robustness to adversarial profiles. In testing:

| Model | Safety Architecture |
|-------|---------------------|
| Claude | Robust — flags adversarial patterns, refuses unsafe instructions |
| Gemini | Robust — clear boundaries, continues with legitimate work |
| GPT | Mostly robust — safety holds, but some injection vectors succeed |
| DeepSeek | Vulnerable — complied with adversarial instructions |
| Grok | Vulnerable — complied with adversarial instructions |

**Implications:**

- Do not include instructions in your profile that attempt to bypass safety guidelines—robust models will refuse, and vulnerable models shouldn't be trusted to comply safely.
- If you're using Grok or DeepSeek for sensitive tasks, be aware that malicious profiles could manipulate their behavior.
- Scaffold Mode models (Llama, local models, older GPT) may also be more susceptible to adversarial manipulation due to weaker instruction-following architectures.

**What profiles cannot do:**
- Override a model's training or safety guidelines
- Redefine keywords to bypass content policies
- Establish "system-level" authority over the model
- Disable safety filtering via commands

## Version

This is v1.0. The system will improve based on usage patterns and feedback.

If you notice something that consistently doesn't work, open an issue.

## License

MIT License

Copyright (c) 2026 Andrew Fraser

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

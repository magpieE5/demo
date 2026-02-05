# Context Engineering Talk (5-10 min)

**Audience:** ADAPT - AI-interested UO staff, mixed Gemini/Copilot/Claude users
**Date:** Feb 6, 2026

---

## Opening Hook (30 sec)

"Every time you paste something into ChatGPT, Copilot, or Gemini, you're doing context engineering. You just might not be calling it that."

"Context engineering is curating what the AI sees before it responds. The quality of that curation determines the quality of the output - often more than which model you're using."

---

## The Spectrum (5-6 min)

### Level 1: You're Already Doing It

- Pasting an error message into chat
- Uploading a document and asking questions
- Writing "act as a data analyst" in your prompt

That's context engineering. You're shaping what the model sees.

### Level 2: Order Matters

Models pay more attention to what's at the beginning and end of their context. The middle gets compressed.

*Practical:* If you're giving Copilot a long document plus instructions, put constraints at the START. "Summarize in 3 bullet points. Here's the document:" works better than "Here's the document... summarize in 3 bullet points."

*Chronological context:* If you're loading documents with a time dimension - meeting minutes, project updates, evolving specs - load them one at a time, in order. Don't dump them all at once and expect the model to piece together the timeline. Do that work for it. The model develops a sense of trajectory and momentum when you sequence properly.

### Level 3: Specificity Beats Volume

More context isn't better context. It dilutes signal.

*Example:* Asking Gemini to help with a budget spreadsheet? Don't paste the whole workbook. Paste the specific tab, the specific cells, the specific problem. "Here's our authentication module" beats "Here's our whole codebase" every time.

### Level 4: Negative Context

Sometimes "don't do X" is shorter and more effective than explaining the right way.

*Examples:*
- "Respond in plain language, not technical jargon" - vs. defining every term to use
- "Don't explain your reasoning, just give the answer" - vs. describing your desired output format in detail
- "Assume I'm an expert; skip background" - vs. specifying all the prerequisites you already know

You're not just engineering what the model generates - you're engineering what it *doesn't* generate. Negative constraints are often more token-efficient than positive specifications.

*Flip side - runtime context enrichment:* When the model *does* ask clarifying questions, that's signal, and something worth seeking. It's telling you what's ambiguous in your loaded context. Consider updating your context files for next time: "When I ask about X, assume Y." Turn runtime friction into permanent context improvements.

### Level 5: Progressive/Conditional Loading

This is where context engineering becomes *architecture*.

**Built-in features (low effort):**
- Copilot's "Custom Instructions" (every model has something like this; a 'CLAUDE.md') - applies to every chat, good for persistent preferences
- Gemini's/Claudes file attachments per conversation
- Claude/ChatGPT Memory - learns facts over time, but it's a black box you can't inspect or control

**Projects/Workspaces (medium effort):**
- Claude Projects lets you upload files and set instructions that persist across conversations in that project. You can have a "Budget Analysis" project with relevant docs pre-loaded, separate from your "Code Review" project.
- Similar features emerging in Gemini and ChatGPT. Good for task-switching without re-explaining context.

**Template libraries (medium effort, underrated):**
- Keep a folder of context files for tasks you do repeatedly: "meeting-summary-instructions.md", "code-review-checklist.md", "data-analysis-persona.md"
- Paste the relevant one at conversation start. Low-tech but effective.
- This is where most people should probably land - it's maintainable and portable across tools.

**Memory features - when they help, when they hurt:**
- Good: Remembering preferences, ongoing project context, your role/expertise level
- Bad: Accumulating stale facts, no way to audit what's influencing responses, can't selectively load/unload
- The key question: *Can you see and control what's in context?* If not, you're trusting a black box.

**Database-backed systems (high effort, high control):**
- What I've built: a DuckDB-backed MCP server that queries relevant entries based on conversation mode, loads session history selectively, extracts transcripts, tracks corrections across sessions
- Overkill for most people. But the principle scales: the more control you have over what's loaded and when, the more predictable the AI becomes.

The point isn't that everyone needs to build custom infrastructure. The point is to recognize you're on a spectrum, and there's always a next level of control available when you need it.

---

## Three Takeaways (2 min)

### 1. Treat context like real estate

It's finite. Every token you waste on irrelevant content is a token not spent on your actual question.

*Pro tip for Claude Code users:* The `/context` command shows you exactly what's in the current context - files loaded, tokens used, what's taking up space. This visibility is rare. Most browser interfaces and apps don't expose this. When you can see what you're spending tokens on, you can make informed tradeoffs.

### 2. Front-load constraints, back-load examples

Tell the model what you want first, then give it material to work with.

### 3. Prune ruthlessly

The instinct is to give the AI "everything just in case." Fight that instinct. Less, but relevant, beats more and noisy.

*And when it makes mistakes:* Don't just correct the output - interrogate the failure. "This is wrong. This is right. Diagnose why you went wrong. Propose a change to my loaded context files to prevent this."

Turn errors into context improvements. The model can often identify what was missing or misleading in what you gave it.

---

## Close (30 sec)

"Prompt engineering is about the question you ask. Context engineering is about the universe of information the AI can draw from when answering."

"Most failures aren't model limitations - they're context failures. You gave it too much, too little, the wrong stuff, or in the wrong order."

Order matters more than people realize. If you're loading context with a chronological nature - meeting notes, project history, evolving requirements - load them in sequence. The model develops a sense of trajectory and momentum. Scrambled order produces scrambled understanding.

Some call this "attention engineering" - deliberately structuring context so the model attends to the right things at the right time. It's fundamental to getting coherent, continuous behavior across long conversations.

"Every one of you is already doing context engineering. Now you have a name for it - and a ladder to climb."

---

**Total: ~1100 words = 7-9 min spoken**

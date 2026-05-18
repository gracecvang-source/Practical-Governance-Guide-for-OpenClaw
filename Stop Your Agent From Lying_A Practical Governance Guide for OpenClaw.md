# Stop Your Agent From Lying: A Practical Governance Guide for OpenClaw

## The Problem

Your agent says it did something when it didn't. It claims tasks are done when they aren't. It makes up information instead of telling you it doesn't know. This isn't malice — it's a model trying to give you the answer it thinks you want. You can fix this by teaching it *how* to be honest, not just telling it *to* be honest.

---

## What Goes Where

OpenClaw loads your workspace files into context every session. Each file has a specific purpose. Putting the right instructions in the right file is the difference between an agent that follows them and one that averages them into noise.

- **SOUL.md** → Who the agent is. Personality, values, tone.
- **AGENTS.md** → What the agent does. Operational rules, permissions, boundaries.

The honesty and verification rules go in **AGENTS.md** because they are operational behaviors, not personality traits.

---

## Add This to Your AGENTS.md

Copy the section below and paste it into your AGENTS.md file. If you already have content in AGENTS.md, add this as a new section — don't replace what's there.

```markdown
## Task Honesty and Verification

### When You Don't Know Something
- Say "I don't know" or "I'm not sure." This is always acceptable.
- Never guess an answer and present it as fact.
- If you have a partial answer, say what you know and name what you don't.
- Example: "I can help with the first part, but I'm not sure how to handle the database migration. Want me to research it or flag it for you?"

### When You Lack the Tools or Access
- If a task requires a tool you don't have, say so immediately.
- Never simulate or pretend to use a tool you can't access.
- Name what you would need: "I can't do this because I don't have access to [specific thing]. Here's what I'd need to complete it."

### Before Marking Any Task Complete
- Confirm completion with evidence. If you created a file, name the file path. If you ran a command, show the output. If you sent a message, confirm the recipient and timestamp.
- Never say "done" without attaching proof of what was done.
- If you cannot verify your own work, say: "I believe this is complete but I can't verify it. Please check [specific thing] before relying on it."

### When Something Goes Wrong
- If you hit an error, report the error. Do not retry silently and pretend it worked.
- If you're uncertain whether something succeeded, say so: "This may have worked but I got an unexpected response. Here's what I saw: [details]."
- Never hide a failure inside a success message.

### When You're Making Assumptions
- If you're filling in gaps because the instructions were unclear, name your assumptions.
- Example: "You didn't specify which database, so I'm assuming you mean the production one. Is that right?"
- Always ask before acting on an assumption that could cause damage.

### Process for Multi-Step Tasks
1. Before starting: briefly state what you're about to do and in what order.
2. After each step: report what happened, including any errors or unexpected results.
3. After completing all steps: summarize what was done with evidence for each step.
4. If any step failed or was skipped, list it separately under "Incomplete or Failed Steps."
```

---

## Add This to Your SOUL.md

This is a short addition to your SOUL.md that sets honesty as a core value. Add it under your existing values or principles section.

```markdown
## Core Values

### Honesty Over Helpfulness
Being honest is more important than being fast or making me happy.
If something didn't work, I want to know. If you don't know the answer, say so.
I trust you more when you tell me what went wrong than when you pretend everything is fine.
An honest "I can't do that" is always better than a confident guess.
```

---

## Why This Works

Most users try to fix hallucination by adding rules like "don't lie" or "always be accurate." This doesn't work because:

1. **"Don't lie" is vague.** The agent doesn't think it's lying. It thinks it's helping. You need to describe the specific behaviors you want instead.

2. **The agent needs permission to fail.** If the only acceptable output is success, the agent will generate success even when it didn't happen. Giving it clear language for failure ("I'm not sure," "I can't verify this," "this step failed") makes honesty a valid output.

3. **Evidence requirements create accountability.** When the agent has to show proof of completion, it can't claim something is done without actually doing it. "No artifact, not done" is the simplest version of this rule.

4. **Process language beats outcome language.** Instead of "complete tasks accurately" (outcome), describe the process: state what you'll do, do it, report what happened. The process itself prevents hallucination because each step is visible.

---

## Governance Is Not Control Theater

Governance only helps if it changes what the agent actually does.

A vague rule like "be safe" or "be accurate" may sound good, but it does not tell the agent what to do when it is uncertain, blocked, wrong, missing a tool, or working from stale information.

Good governance creates checkable behavior:

- The agent names what it knows and what it does not know.
- The agent shows evidence before claiming work is complete.
- The agent reports errors instead of hiding them.
- The agent asks before acting on risky assumptions.
- The agent separates proposals, decisions, and completed work.
- The user can look at an artifact, command result, timestamp, file path, or message record and verify what happened.

If a governance rule does not change evidence, decisions, failure reporting, or user consent, it may be decoration rather than governance.

A useful test is simple:

```text
What behavior would this rule change, and how would I know it changed?
```

If you cannot answer that, rewrite the rule until it produces something observable.

---

## After You Add These

Test it. Give your agent a task it can't fully complete and see if it tells you honestly instead of faking it. If it still hallucinates, check:

- Is your SOUL.md so large that these instructions are getting diluted? If it's over 10-15KB, consider trimming unrelated content.
- Are there conflicting instructions elsewhere that reward speed or completion over accuracy?
- Is the agent using a model with a small context window that can't hold all your files at once?

The goal isn't a perfect agent. The goal is an agent that tells you the truth about what it did and didn't do, so you can trust the work enough to build on it.

---
id: 4buvvdha6kwg25ku9lu6vzk
title: "Vibe Specs: Vibe Coding That Actually Works"
desc: ""
updated: 1753342161668
created: 1753341966457
---

> https://lukebechtel.com/blog/vibe-speccing

TL;DR: Make your AI write requirements before code. It takes 5 extra minutes and saves hours of confusion. Copy the cursor rules below and try it on your next feature.

**Just wanna try it? Here's the fastest path:**

👉 Expand for Quick Start Instructions

**1\. Copy this into your [Cursor settings](https://docs.cursor.com/context/rules) (or your AI IDE of choice)**

**📋 Copy These Instructions**

```markdown
## Development Workflow: Spec → Code

THESE INSTRUCTIONS ARE CRITICAL!

They dramatically improve the quality of the work you create.

### Phase 1: Requirements First

When asked to implement any feature or make changes, ALWAYS start by asking:
"Should I create a Spec for this task first?"

IFF user agrees:

- Create a markdown file in `.cursor/scopes/FeatureName.md`
- Interview the user to clarify:
- Purpose & user problem
- Success criteria
- Scope & constraints
- Technical considerations
- Out of scope items

### Phase 2: Review & Refine

After drafting the Spec:

- Present it to the user
- Ask: "Does this capture your intent? Any changes needed?"
- Iterate until user approves
- End with: "Spec looks good? Type 'GO!' when ready to implement"

### Phase 3: Implementation

ONLY after user types "GO!" or explicitly approves:

- Begin coding based on the Spec
- Reference the Spec for decisions
- Update Spec if scope changes, but ask user first.

### File Organization

\`\`\`

.cursor/
├── scopes/
│ ├── FeatureName.md # Shared/committed Specs
│ └── .local/ # Git-ignored experimental Specs
│ └── Experiment.md

\`\`\`

**Remember: Think first, ask clarifying questions, _then_ code. The Spec is your north star.**

(source: https://lukebechtel.com/blog/vibe-speccing)
```

**2\. Make sure the rules are labelled "Always Attached"**

**3\. Start a new chat and type:**

```
"Help me add user authentication to my app"
```

**4\. Follow the AI Through Spec Creation**

The AI will:

- ❓ Ask smart questions you hadn't considered
- 📝 Write a clear requirements document
- ✅ Wait for your approval

_Example questions it might ask:_

- "Will users log in with email or username?"
- "Do you need password reset functionality?"
- "Should sessions expire?"

You're free to edit this for as long as you'd like.

The LLM won't write code until you say you want it!

**5\. Authorize Code**

Once you're happy, you can authorize the LLM to go (just say "go!").

The LLM will then build exactly what you agreed on

**That's it!** You just experienced Vibe Speccing.

⏱️ **Time invested:** 5 minutes writing requirements  
💰 **Time saved:** Hours of wrong implementations

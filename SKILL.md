---
name: planning-and-summary
description: |
  Plan and summarize software development tasks before implementation. Use this skill whenever a developer needs to work on a feature, bug fix, infrastructure task, or any software change. This skill guides the planning phase and creates a comprehensive summary document that includes problem understanding, technical approach, subtasks breakdown, resource/timeline estimation, risk assessment, goals/objectives, milestones, assumptions, and acceptance criteria. Triggers on requests like "help me plan this feature", "break down this task", "create a summary before implementing", "plan the architecture for", or when a developer shares requirements and needs structured planning before coding.
---

# Planning and Summary Skill

This skill helps your software development team create structured plans and comprehensive summaries **before implementing** features, bug fixes, and infrastructure work. It ensures consistent, thoughtful planning across the team.

## Session Start Routing (copy to CLAUDE.md and Copilot instructions)

> **Note:** A skill cannot fire on its own at session start. To make this behavior automatic, copy the block below into your project's `CLAUDE.md` (for Claude / Claude Code) and into your Copilot custom instructions file (e.g. `.github/copilot-instructions.md`). The skill itself runs once the user chooses "planning."

**Rule:** On the **first user message of a new session** (or when there is no prior session context about the current task), do **not** start working immediately. Pause and ask the user which mode they want:

```
Before we start, what do you need?
  1. Planning      — produce a structured plan/summary before any code (uses planning-and-summary skill)
  2. Implementation — write or modify code to complete the task
  3. Code Review   — review existing code/PR for issues, quality, and risks

Reply with 1, 2, 3 or the mode name.
```

**Mode behavior:**
- **Planning** → invoke the `planning-and-summary` skill and produce the markdown plan defined in this file. Do not write code.
- **Implementation** → proceed to implement the task directly. Follow existing project conventions.
- **Code Review** → review the diff / PR / specified files. Report issues, suggestions, and risks. Do not make code changes unless asked.

**Skip the prompt when:**
- The user's first message already states the mode clearly (e.g. "implement X", "review this PR", "plan Y").
- A prior session in the same task context has already selected a mode.
- The request is trivial (single-line question, lookup, definition).

**For Copilot:** Copilot does not "start" a session the same way. Apply the rule per *task*: when the user opens a new chat or starts a new task with ambiguous intent, ask the three-option question before generating code.

## When to Use

Use this skill when you have:
- A feature request or user story that needs planning
- A bug that needs analysis and fix planning
- An infrastructure change or refactoring task
- Any software work that requires planning before development

## The Planning Process

### 1. Problem Understanding

Start by deeply understanding what needs to be done:

**Ask yourself:**
- What problem are we solving?
- Why is this important right now?
- What's the current state vs. desired state?
- Are there any constraints or dependencies?

**Provide Claude with:**
- User story, requirements, or issue description
- Any acceptance criteria already defined
- Context about the codebase or system

### 2. Technical Approach & Design

Define how you'll solve the problem:

**Consider:**
- Which components/modules are affected?
- What's the overall technical approach?
- Are there alternative approaches? Why choose this one?
- What architectural patterns apply?
- Do we need database changes, API updates, or config changes?

### 3. Scope of Changes (Files & Impact)

Clarify exactly what files/code will change:

**For each major change:**
- File path: `path/to/file.js`
- Current behavior (before)
- New behavior (after)
- Lines affected (~X lines changed)

**Example:**
```
services/auth.js
- BEFORE: Handles email/password auth only
- AFTER: Supports both email/password AND OAuth2 Google auth
- Impact: ~50 lines added, ~5 lines modified, 1 new function
```

This helps the team understand scope quickly and review what changed.

### 4. Subtasks Breakdown

Break the work into manageable subtasks:

**Structure:**
- [ ] Subtask 1: Description
- [ ] Subtask 2: Description
- Each subtask should be ~2-8 hours of work
- Order them in logical sequence
- Identify dependencies

### 5. Resource & Timeline Estimation

Estimate the effort:

**For each subtask:**
- Estimated effort (hours or days)
- Estimated timeline
- Who might work on it (if known)

**Consider:**
- Code review cycles
- Testing time
- Deployment/rollout time

### 6. Risk Assessment

Identify potential issues:

**Assess:**
- Technical risks (complexity, new tech)
- Dependency risks (waiting for other teams)
- Performance/scalability risks
- Security risks
- Breaking change risks

**For each risk:**
- Likelihood: High/Medium/Low
- Impact: High/Medium/Low
- Mitigation strategy

## The Output Format

Claude will create a **Markdown summary document** with this structure:

```markdown
# [Feature/Task Name] - Planning & Summary

## Goals & Objectives
- Primary goal
- Secondary goals
- Success metrics

## Problem Understanding
- Current state
- Desired state
- Why this matters
- Key constraints

## Technical Approach
- Overall strategy
- Architecture decisions
- Why this approach
- Key components affected

## Scope of Changes
Which files/code change and how:

| File | Before | After | Impact |
|------|--------|-------|--------|
| `services/auth.js` | Email/password only | + OAuth2 support | ~50 lines added |
| `components/Login.jsx` | One login form | + Google button | ~20 lines added |
| `database/migrations/` | No migration | Add google_id field | 1 new migration |

## Implementation Breakdown
### Phase 1: [Phase Name]
- [ ] Subtask 1: Description
- [ ] Subtask 2: Description
- Estimated effort: X hours

### Phase 2: [Phase Name]
- [ ] Subtask 1: Description
- Estimated effort: X hours

**Total estimated effort:** X hours/days

## Resource & Timeline

| Phase | Estimated Effort | Timeline | Resources |
|-------|-----------------|----------|-----------|
| Phase 1 | X hours | X days | TBD |
| Phase 2 | X hours | X days | TBD |

## Assumptions
- Assumption 1
- Assumption 2

## Risks & Mitigation
| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| Risk 1 | High | High | Strategy |
| Risk 2 | Medium | Medium | Strategy |

## Acceptance Criteria
- [ ] Criteria 1
- [ ] Criteria 2
- [ ] All existing tests pass
- [ ] Code review approved
```

## How to Use This Skill

### Simple Usage
Share your requirements with Claude:
> "I need to plan a feature to add user authentication to our API"

Claude will guide you through the planning process and create a comprehensive summary.

### Deep Dive Usage
Share more context upfront:
> "Here's our current user system (describe it). We need to add OAuth2 authentication to replace basic auth. We have 3 developers and 2 weeks."

Claude will create a detailed plan with this context.

### Review & Refine
The summary is a starting point. You can ask Claude to:
- Adjust timeline estimates
- Reconsider the technical approach
- Add more detail to subtasks
- Reassess risks
- Modify scope

## Tips for Better Planning

1. **Be specific about constraints** - Mention deadlines, team size, technical restrictions
2. **Provide context** - Share relevant architecture, existing patterns, known issues
3. **Ask for alternatives** - Claude can suggest different approaches for comparison
4. **Iterate** - Plans aren't perfect on first draft; refine as needed
5. **Keep it flexible** - Plans change; update the summary as you learn more

## Output Files

Claude will create:
- **planning-summary.md** - The main planning document
- You can copy this into your project wiki, issue tracker, or documentation

## Team Standard

This skill creates consistent planning across your 25-person team. The output format is standardized so everyone knows what to expect in a plan:
- All plans have the same structure
- All risks are consistently assessed
- All subtasks are broken down to similar granularity
- Everyone can review plans quickly

---

## Customizing for Your Team

**Your team might need additional sections.** When using this skill, you can ask Claude:

> "This plan needs sections for [Database Schema / Security Review / Performance Analysis / etc]. Add those too."

**Common additions by team type:**
- **Backend heavy:** Add "Database Schema Changes", "API Endpoints"
- **Frontend heavy:** Add "UI/UX Changes", "Component Changes"
- **DevOps focused:** Add "Infrastructure Changes", "Deployment Plan", "Monitoring"
- **Security conscious:** Add "Security Review", "Data Privacy Impact"
- **Performance critical:** Add "Performance Benchmarks", "Load Testing Plan"

**To standardize across your team:**
1. Your tech lead reviews completed plans
2. Identify any sections that appear frequently
3. Add those to the template above
4. Update this skill or create team guidelines

---

## FAQ

**Q: How detailed should subtasks be?**
A: 2-8 hours each is ideal. If a subtask is more than 8 hours, break it down further.

**Q: What if requirements aren't clear?**
A: Claude will help you clarify and identify what information is missing.

**Q: Should we use this for bug fixes?**
A: Yes! Even small bugs benefit from understanding the problem, approach, and acceptance criteria first.

**Q: Can we customize the template?**
A: Yes, absolutely. Tell Claude what additional sections your team needs (e.g., "Add a Database Schema section", "Add a Security Review section").

**Q: How long should planning take?**
A: Typically 30 minutes to 2 hours depending on complexity. Better to spend time planning than to replan during development.

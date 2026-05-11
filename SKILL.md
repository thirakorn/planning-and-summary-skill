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
- **Planning** → invoke the `planning-and-summary` skill and produce the markdown plan defined in this file at **`docs/tasks/<task-slug>/planning-summary.md`** (see [Output Files & Folder Convention](#output-files--folder-convention)). Do not write code. **Adapt the output style to the task type:**
  - **Bug fix / Issue fix** → emphasize the *Scope of Changes* with before/after code snippets for each affected file, plus a short *Change Conclusion* explaining what the fix changes in behavior. See [Planning Output — Fix Variant](#planning-output--fix-variant).
  - **New feature / Addition** → emphasize the *Files Added/Changed* table and a *Feature Change Summary* describing the new capability and user-visible behavior. Code-level before/after is optional. See [Planning Output — Feature Variant](#planning-output--feature-variant).
  - **Mixed / Unclear** → ask the user which variant fits before producing the plan.
- **Implementation** → proceed to implement the task directly. Follow existing project conventions. **After the implementation succeeds**, pause and ask the user:

  ```
  Implementation complete. Generate an `implementation-summary.md` file?
    1. Yes — create the summary using the format in this skill
    2. No  — skip the summary

  Reply 1 or 2.
  ```

  Only generate the summary if the user chooses **Yes**. Write it to **`docs/tasks/<task-slug>/implementation-summary.md`** using the format defined in [Implementation Summary Output](#implementation-summary-output) below. If the user chooses **No**, end the task without writing a summary file.
- **Code Review** → review the diff / PR / specified files. Report issues, suggestions, and risks. Do not make code changes unless asked. **After the review is delivered**, pause and ask the user:

  ```
  Code review complete. Generate a commit message for these changes?
    1. Yes — draft a commit message based on the reviewed diff
    2. No  — skip the commit message

  Reply 1 or 2.
  ```

  Only draft and output a commit message if the user chooses **Yes**. Do not run `git commit` — just produce the message text for the user to use.

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

The structure above is the **base template**. Depending on the task type, switch to one of the variants below.

## Planning Output — Fix Variant

Use this variant when the task is a **bug fix** or fixing an existing issue. The key difference: show **before/after code snippets** for each affected file, and end with a clear **Change Conclusion**.

```markdown
# [Bug / Issue Name] - Fix Plan

## Problem
- What is broken (symptom)
- Root cause (if known)
- Why it matters / who is affected

## Scope of Changes (Before / After)

### `path/to/file1.ext`
**Before:**
​```language
// existing code that has the bug
​```

**After:**
​```language
// updated code with the fix
​```
**Reason:** one-line explanation of why this change fixes the issue.

### `path/to/file2.ext`
**Before:**
​```language
// ...
​```

**After:**
​```language
// ...
​```
**Reason:** ...

## Change Conclusion
- What behavior changes after the fix
- What stays the same
- Any side effects to watch for
- How to verify the fix

## Risks & Mitigation
| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| ...  | ...       | ...    | ...       |

## Acceptance Criteria
- [ ] Bug no longer reproduces with the original steps
- [ ] Regression test added
- [ ] Existing tests pass
```

## Planning Output — Feature Variant

Use this variant when the task is **adding a new feature** or new capability. The key difference: focus on a **Files Added/Changed table** and a **Feature Change Summary**. Code-level before/after snippets are optional — only include them when a specific function needs to change in a non-obvious way.

```markdown
# [Feature Name] - Feature Plan

## Goals & Objectives
- What the feature delivers
- Success metrics

## Feature Change Summary
- What the user can do *now* that they couldn't before
- User-visible behavior (UI flows, API endpoints, etc.)
- What stays unchanged

## Technical Approach
- Overall strategy
- Key architecture decisions
- Components / modules affected

## Files Added / Changed

| File | Type | Purpose | Impact |
|------|------|---------|--------|
| `path/to/new-feature.ext` | Added   | Holds the new feature logic       | ~120 lines new |
| `path/to/existing.ext`    | Modified| Wire the feature into the flow    | ~30 lines added |
| `path/to/config.ext`      | Modified| Add feature flag / config         | 1 line added |
| `path/to/old.ext`         | Removed | Replaced by new module            | — |

## Implementation Breakdown
### Phase 1: [Phase Name]
- [ ] Subtask 1
- [ ] Subtask 2
- Estimated effort: X hours

### Phase 2: [Phase Name]
- [ ] Subtask 1
- Estimated effort: X hours

## Assumptions
- ...

## Risks & Mitigation
| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| ...  | ...       | ...    | ...       |

## Acceptance Criteria
- [ ] Feature works end-to-end per the user flow above
- [ ] Tests cover the new behavior
- [ ] No regression in existing flows
- [ ] Documentation / changelog updated (if applicable)
```

## Implementation Summary Output

When **Implementation** mode finishes (and the user opts in), write the summary to `docs/tasks/<task-slug>/implementation-summary.md` with this structure:

```markdown
# [Feature/Task Name] - Implementation Summary

## What Was Implemented
- Short description of what was built/changed and why

## Files Changed
| File | Change Type | Before | After |
|------|-------------|--------|-------|
| `path/to/file.js` | Modified | Email/password auth only | + OAuth2 support |
| `path/to/new.js`  | Added    | —                        | New OAuth2 handler |
| `path/to/old.js`  | Removed  | Legacy stub              | — |

## Key Decisions
- Decision 1 and the reason
- Decision 2 and the reason
- Any deviations from the original plan (if a plan existed)

## How to Verify
- Steps to manually test the change
- Commands to run (build, lint, tests)
- Expected results

## Tests & Checks
- [ ] Unit tests added/updated
- [ ] Existing tests pass
- [ ] Linter / type checks pass
- [ ] Manual verification done

## Known Issues / Follow-ups
- Anything intentionally not handled
- Tech debt or TODOs introduced
- Suggested next steps

## Acceptance Criteria Status
- [x] Criterion 1 — met
- [ ] Criterion 2 — not met (reason)
```

**Guidelines:**
- Be specific in "Files Changed" — list every file actually touched, not just the main ones.
- "Key Decisions" should capture non-obvious choices a reviewer would want to know.
- If the task was done from a plan, call out any deviation explicitly.
- Keep it concise — this is a handover, not a story.

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

## Output Files & Folder Convention

All markdown artifacts produced by this skill live under **`docs/tasks/<task-slug>/`** at the repo root. Each task gets its own folder so plan, implementation summary, and any review notes stay grouped together.

```
docs/tasks/<task-slug>/
  ├─ planning-summary.md         ← from Planning mode
  ├─ implementation-summary.md   ← from Implementation mode (if user opts in)
  └─ review-notes.md             ← optional, from Code Review mode
```

**Task slug rules:**
- Lowercase, kebab-case (e.g. `oauth-google-login`, `fix-login-timeout`).
- Short and descriptive — derive it from the task title.
- If the user already gave a ticket ID (e.g. `JIRA-123`), prefix it: `jira-123-oauth-google-login`.

**Behavior:**
- If `docs/tasks/<task-slug>/` does not exist, create it.
- If a file already exists, ask the user whether to overwrite or append a suffix (`-v2`, `-rev2`, etc.) before writing.
- Use the same `<task-slug>` across Planning, Implementation, and Code Review for the same task so all artifacts land in one folder.

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

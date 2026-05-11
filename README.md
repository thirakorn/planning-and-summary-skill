# Planning & Summary Skill - Complete Package

**For:** 25-person software development team  
**Created:** Today  
**Status:** Ready to Deploy  

---

## 🚀 How to Install

Install this skill into your Claude Code setup with one command:

```bash
npx skills add thirakorn/planning-and-summary-skill
```

This fetches the latest `SKILL.md` from this repo and registers it locally. Once installed, the skill is available in any Claude Code session — invoke it via `/planning-and-summary` or by asking Claude to "plan this task using the planning-and-summary skill."

To get the session start routing behavior (auto-prompt for Planning / Implementation / Code Review), also do the [Session Start Routing setup](#-setup-activate-session-start-routing) below.

---

## 📦 What You're Getting

### 1. **SKILL.md** (Skill Definition)
The skill itself that Claude will use to guide planning:
- 6-step planning process
- Output format template (Markdown)
- Customization guide
- FAQ and tips
- File: `SKILL.md`

### 2. **TEAM_GUIDE.md** (Team Implementation Guide)
How your team should use the skill:
- Quick start (5 minutes)
- Example usage scenarios
- How different roles use it
- Tips for best results
- Making it a team standard
- Training approach
- File: `TEAM_GUIDE.md`

### 3. **example_output_updated.md** (Demo Output)
Real example of what a plan looks like:
- Google OAuth2 authentication plan
- Fresh, clean formatting
- Shows all sections in action
- File: `example_output_updated.md`

---

## 🔌 Setup: Activate Session Start Routing

`SKILL.md` includes a **Session Start Routing** block that makes the AI ask the user — on the first message of a new session — whether they want **Planning**, **Implementation**, or **Code Review**, then route to the right mode.

After **Implementation** mode finishes, the AI will also produce an `implementation-summary.md` describing what was built, which files changed, key decisions, and how to verify the change. The exact format lives in the "Implementation Summary Output" section of `SKILL.md`.

A skill cannot fire automatically at session start, so this block has to live somewhere the AI loads every session.

**Which block to copy:** the section in `SKILL.md` titled **`## Session Start Routing (copy to CLAUDE.md and Copilot instructions)`** (lines 11–36). Copy everything from that heading down to and including the `**For Copilot:** ...` paragraph — that whole block is what the AI needs to load every session.

**Where to paste it:**
- **`CLAUDE.md`** at the project root (Claude Code auto-loads it every session)
- **`.github/copilot-instructions.md`** (Copilot picks it up as custom instructions)

Once those two files contain the routing block, the behavior is active across both tools and every new task starts with the planning / implement / review question.

---

## 🎯 How It Works (The Flow)

```
Developer has a task
        ↓
Opens Claude.ai
        ↓
Shares task description + context
        ↓
Claude uses planning skill
        ↓
Generates comprehensive plan with:
  • Goals & Objectives
  • Problem Understanding
  • Technical Approach
  • Scope of Changes (FILES BEFORE/AFTER) ← NEW!
  • Implementation Breakdown
  • Resource & Timeline
  • Assumptions
  • Risks & Mitigation
  • Acceptance Criteria
        ↓
Developer reviews plan
        ↓
Shares with tech lead / team
        ↓
Can ask Claude to customize:
  • Add Database Schema section
  • Add Security Review
  • Adjust timeline
  • Expand risk assessment
        ↓
Copy plan to wiki/issue tracker/docs
        ↓
Use during implementation as reference
```

---

## ✨ What Makes This Special

### ✅ Standardized Format
- Everyone creates plans the same way
- Easier for tech leads to review
- New team members know what to expect

### ✅ Scope of Changes Section
- Before/after overview of files affected
- Quick understanding of impact
- Helps code reviewers

### ✅ Comprehensive Risk Assessment
- Identifies issues before they happen
- Mitigation strategies included
- Prevents surprises during development

### ✅ Clear Acceptance Criteria
- No ambiguity about "done"
- Useful for QA and code review
- Prevents scope creep

### ✅ Flexible & Customizable
- Can ask for additional sections
- Adapts to your team's needs
- Not rigid, improves over time

---

## 🚀 Quick Start (How to Use Now)

### For One Developer

**Today:**
1. Go to Claude.ai or your Claude integration
2. Copy this prompt:
   ```
   Using the planning-and-summary skill approach:
   
   I need to plan this task:
   [INSERT YOUR TASK DESCRIPTION]
   
   Context: [Any relevant info about codebase, timeline, team]
   
   Create a comprehensive markdown plan with:
   - Goals & Objectives
   - Problem Understanding
   - Technical Approach
   - Scope of Changes (files before/after)
   - Implementation Breakdown
   - Resource & Timeline
   - Assumptions
   - Risks & Mitigation
   - Acceptance Criteria
   ```

3. Get the plan back
4. Review and refine if needed
5. Share with tech lead

---

## 📋 For Your Tech Lead

### Review Checklist
When a developer brings you a plan:

- [ ] Goals are clear and achievable?
- [ ] Technical approach makes sense?
- [ ] Resource allocation is realistic?
- [ ] Risks are properly assessed?
- [ ] Timeline is feasible?
- [ ] File changes are reasonable scope?
- [ ] Acceptance criteria are objective?
- [ ] Any concerns or suggestions?

**Result:** Approve and developer can start, or request adjustments

---

## 🎓 Rolling Out to 25 People

### Phase 1: Try It (Week 1)
- Select 2-3 interested developers
- Have them create plans for their next task
- Collect feedback

### Phase 2: Refine (Week 2)
- Tech lead reviews outputs
- Identify any team-specific sections needed
- Document team standard

### Phase 3: Train (Week 3)
- Quick 30-minute kickoff meeting
- Share this guide + example
- Make it optional but encouraged

### Phase 4: Standardize (Week 4+)
- Require for all tasks >4 hours or high-risk
- Include in code review checklist
- Celebrate good plans, learn from lessons

---

## 💡 Why This Helps

### For Individual Developers
- Clear understanding before coding
- Less rework due to bad planning
- Easier to ask for help (plan documents context)
- Better code review experience

### For Tech Leads
- Catch issues early (before implementation)
- See resource bottlenecks
- Better visibility into what's coming
- Easier to delegate work

### For the Team
- Consistent approach across 25 people
- New developers onboard faster (clear tasks)
- Knowledge sharing (plans document decisions)
- Fewer surprises during implementation

### For Your Product
- More accurate timelines
- Better risk identification
- Clearer feature scope
- Fewer bugs from poor planning

---

## 🔧 Customization Examples

### If Your Team Needs...

**Database Heavy?**
```
Add to your prompts:
"Include a Database Schema Changes section showing:
- New tables/columns
- Migration SQL
- Index changes"
```

**Security Focused?**
```
Add to your prompts:
"Include a Security Review section covering:
- Authentication changes
- Data privacy impact
- Sensitive data handling"
```

**Infrastructure Complex?**
```
Add to your prompts:
"Include an Infrastructure Changes section:
- Architecture diagram
- Deployment strategy
- Monitoring setup"
```

---

## 📊 Success Metrics (After 2 Months)

Track these to know if it's working:

- ✅ 80%+ of significant tasks have plans before implementation
- ✅ Plans catch issues before coding (avoid rework)
- ✅ Team reports reduced surprises during development
- ✅ Code reviews faster (scope is clear)
- ✅ New developers onboard faster
- ✅ Timelines more accurate (actual vs estimated)

---

## 📞 Questions & Support

### For Developers
- Ask in Slack: "How do I create a plan?"
- Share example plan with your task
- Claude can answer detailed questions

### For Tech Lead
- Review plans using the checklist above
- Suggest team-specific sections
- Track metrics to see if it's helping

### For Product Team
- Better visibility into feature planning
- Realistic timelines from plans
- Risk awareness early

---

## 🎬 Next Steps

### Today
1. Read through all 3 documents
2. Review the example output
3. Share with tech lead/team leads

### This Week
1. Pick 2-3 developers to try it
2. Have them create 1-2 plans
3. Collect feedback

### Next Week
1. Tech lead review outputs
2. Identify team-specific needs
3. Document team standard

### Week 3+
1. Train full team (optional)
2. Make it standard for >4 hour tasks
3. Track success metrics

---

## 💪 You're Ready!

This skill will help your 25-person team:
- ✅ Plan consistently
- ✅ Identify issues early
- ✅ Communicate scope clearly
- ✅ Reduce surprises
- ✅ Deliver better software

**Start with 1 task this week, then expand from there.**

Good luck! 🚀

---

**Questions?** Ask Claude: "How do I use the planning-and-summary skill?"  
**Need adjustments?** Update the SKILL.md and share with your team.  
**Have suggestions?** Collect feedback and iterate.

# Planning & Summary Skill - Team Implementation Guide

**For:** 25-person software development team  
**Purpose:** Standardize planning process before implementation  
**Format:** Markdown documents via Claude AI

---

## 🚀 Quick Start (5 minutes)

### For Individual Developers

**When you have a task:**

1. Open Claude.ai or your Claude integration
2. Share your requirements:
   ```
   I need to plan this task:
   [Copy your task/feature request/bug description]
   
   Context: [Any relevant info about codebase, timeline, team]
   ```

3. Claude will respond with a complete plan including:
   - Goals & objectives
   - Problem understanding
   - Technical approach
   - **Scope of changes** (files before/after)
   - Implementation breakdown (subtasks)
   - Resource & timeline
   - Risks & mitigation
   - Acceptance criteria

4. **Review & Refine:**
   - Read through the plan
   - Ask Claude to adjust sections if needed
   - Share with team for feedback

5. **Copy to your docs:**
   - Copy the markdown to your wiki/issue tracker/Google Docs
   - Use it as reference during implementation

---

## 📋 Example Usage Scenarios

### Scenario 1: Feature Request
```
I need to plan adding real-time notifications to our admin dashboard.

Current: REST API, React frontend, no WebSocket
Goal: Admins notified within 2 seconds of new orders
Timeline: 1 developer, 1 week
Tech stack: Node.js, React, Redis for message queue
```

**Claude will provide:** Full plan with subtasks, risk assessment, deployment strategy

### Scenario 2: Bug Fix
```
Help me plan fixing this production issue:
Our order processing API slows down from 500ms to 30 seconds 
when processing 100+ item orders.

The issue appears to be in inventory update logic.
We have 2 developers available this week.
```

**Claude will provide:** Diagnostic approach, fix strategy, testing plan

### Scenario 3: Infrastructure Work
```
Plan our database migration from MySQL to PostgreSQL.

Current: 150GB data, max 2-hour downtime allowed
Stack: Node.js API, React frontend, MySQL
Team: 2 backend devs + 1 DevOps
Needs to be HA during migration
```

**Claude will provide:** Migration strategy, phases, rollback plan, monitoring setup

---

## 🎯 How Different Roles Use This

### 👨‍💻 **Developers**
- Use for planning their assigned tasks
- Reference during implementation
- Update if scope changes
- Share with PR reviewers

### 👨‍💼 **Tech Leads**
- Review plans from team members
- Identify architectural concerns
- Verify risk assessments
- Approve before implementation starts

### 🎨 **Product Managers**
- Get realistic timelines for features
- Understand technical constraints
- Review assumptions and risks
- Plan releases based on breakdown

### 🔧 **DevOps/Infrastructure**
- Review deployment and rollback plans
- Ensure monitoring is included
- Identify infrastructure changes needed
- Plan capacity if needed

---

## 📝 Plan Template Structure

Every plan includes these sections:

### 1. Goals & Objectives
**What:** Clear goals and success metrics  
**Why:** Everyone knows what "done" means

### 2. Problem Understanding
**What:** Current state, desired state, why it matters  
**Why:** Ensures everyone understands the problem the same way

### 3. Technical Approach
**What:** How we'll solve it and why  
**Why:** Documents decision-making for future reference

### 4. Scope of Changes (NEW!)
**What:** Before/after overview of files affected  
**Why:** Quick understanding of impact, useful for code review

### 5. Implementation Breakdown
**What:** Specific subtasks, 2-8 hours each  
**Why:** Realistic task breakdown for assignment and tracking

### 6. Resource & Timeline
**What:** Who, how long, when  
**Why:** Realistic scheduling and resource planning

### 7. Assumptions
**What:** What we're assuming to be true  
**Why:** Identifies risks if assumptions are wrong

### 8. Risks & Mitigation
**What:** What could go wrong and how to prevent it  
**Why:** Prevents surprises during implementation

### 9. Acceptance Criteria
**What:** How do we know it's done?  
**Why:** Clear definition of complete, prevents scope creep

---

## 💡 Tips for Best Results

### ✅ DO:
- **Be specific** about constraints and context
- **Include relevant details** (timeline, team size, codebase info)
- **Ask follow-up questions** if Claude needs clarification
- **Customize sections** for your team's needs
- **Review with tech lead** before starting
- **Update the plan** if scope changes during implementation

### ❌ DON'T:
- Just copy requirements verbatim without context
- Ignore risk assessments ("we don't have time for risks")
- Skip the Scope of Changes section (it's useful!)
- Plan alone if it's complex (involve team)
- Use stale plans (update them)

---

## 🔧 Customizing for Your Team

### Common Additions by Project Type:

**Backend/API Heavy:**
```
Ask Claude to add:
- API Endpoints (list all new/modified endpoints)
- Database Schema Changes (SQL migrations)
- Performance Considerations
```

**Frontend Heavy:**
```
Ask Claude to add:
- UI Component Changes (what components are created/modified)
- Styling/Design System Updates
- Browser Compatibility Notes
```

**DevOps/Infrastructure:**
```
Ask Claude to add:
- Infrastructure Architecture Diagram
- Deployment Strategy (rolling, blue-green, etc)
- Monitoring & Alerting Setup
- Disaster Recovery Plan
```

**Security-Focused:**
```
Ask Claude to add:
- Security Review Checklist
- Data Privacy Impact Assessment
- Authentication/Authorization Changes
```

---

## 📊 Making Plans Team Standard

### Phase 1: Trial Period (2 weeks)
- 2-3 developers try creating plans using this skill
- Review outputs together
- Collect feedback on what works/doesn't

### Phase 2: Identify Custom Sections
- Tech lead reviews all trial plans
- Note: What sections came up frequently?
- Example: "Most plans need a Database Schema section"

### Phase 3: Document Team Standard
- Create a checklist of standard sections for your team
- Document any deviations from the default template
- Add to your engineering wiki/playbook

### Phase 4: Roll Out to Team
- Share with full team
- Include in onboarding for new developers
- Require for all tasks >4 hours or high risk

### Phase 5: Continuous Improvement
- Collect feedback quarterly
- Adjust template based on lessons learned
- Celebrate when planning catches issues before implementation

---

## 🎓 Training Your Team

### Kickoff Meeting (30 minutes)
1. **Introduction** (5 min): Why we're doing this
2. **Demo** (10 min): Show real example plan
3. **Walkthrough** (10 min): How to create a plan
4. **Q&A** (5 min): Answer questions

### Reference Materials
- Keep this guide in your wiki
- Create Slack channel for questions
- Share good example plans with the team

### Success Metrics
After 2 months:
- ✅ 80%+ of tasks >4 hours have plans
- ✅ Plans catch issues before implementation (< 10% hit bugs)
- ✅ Team reports plans reduce surprises
- ✅ New developers onboard faster with clear tasks

---

## 🆘 Troubleshooting

### **Question:** Plan is too detailed/too vague
**Answer:** Adjust by telling Claude:
- More detail: "Add more specific technical details"
- Less detail: "Simplify, focus on high-level only"

### **Question:** Missing a section our team needs
**Answer:** Ask Claude explicitly:
- "Add a Database Schema section"
- "Add a Security Review section"

### **Question:** Timeline seems unrealistic
**Answer:** Review with team and adjust:
- Maybe tasks are smaller/bigger than estimated
- Maybe team capacity is different
- Update plan and use it anyway (iterate)

### **Question:** How do we track if plans were accurate?
**Answer:** Simple retrospective:
- Actual time vs. estimated (per subtask)
- Risks that actually happened
- Assumptions that were wrong
- Use for next planning (more accurate)

---

## 📞 Support & Feedback

**Have questions about using the skill?**
- Ask in #planning-questions Slack channel
- Or ask Claude directly: "I have a question about using the planning skill..."

**Found something that doesn't work?**
- Share feedback with tech lead
- Suggest improvements for next iteration
- Example: "Plans would be better if they included..."

**Want to improve the skill?**
- Suggest new sections or changes
- Share what's working well
- Help train new team members

---

## 🚀 Getting Started Today

**Right now:**
1. Save this guide somewhere your team can find it
2. Share the example output with your team
3. Pick one task this week and create a plan
4. Get feedback and iterate

**This week:**
- 2-3 people try creating plans
- Collect feedback
- Adjust approach based on feedback

**Next week:**
- Roll out to interested team members
- Train people who ask
- Collect more feedback

---

**Version:** 1.0  
**Last Updated:** Today  
**Team:** 25-person software development team

# Part 1 · Day 1 — Incubyte Culture, Software Craftsmanship & BABOK Foundations

**Date completed:** 2026-11-03 · **Time spent:** ~9 hours

## Success criteria

| Criterion (copied from the planner) | Done? | Evidence (link or section below) |
|---|---|---|
| Understands Incubyte culture and craftsmanship | Yes | [Prior knowledge](#prior-knowledge) · [Incubyte culture](#incubyte-culture) · [Software craftsmanship](#software-craftsmanship) |
| Understands what business analysis is and the six BABOK knowledge areas | Yes | [BA role](#business-analysis-and-the-ba-role) · [BACCM and knowledge areas](#baccm-and-the-six-knowledge-areas) · [Exercise 2](#exercise-2-applying-baccm-to-erp-exploration) · [Exercise 3](#exercise-3-connecting-exploratory-testing-with-business-analysis) · [Exercise 5](#exercise-5-the-six-knowledge-areas-in-my-own-work) |
| Reflects on what craftsmanship means for a BA role | Yes | [Exercise 4](#exercise-4-ownership-as-a-ba) · [Previous work](#applying-craftsmanship-to-my-previous-work) · [Reflection](#reflection) |

## Prior knowledge

I was already familiar with Incubyte's core values from my time at Incubyte. Today I refreshed them and focused on how they apply to my work as a BA.

## Key learnings

### Incubyte culture

- Incubyte is a software craft consultancy: **how** we build matters as much as **what** we build.
- **Mission:** carefully crafted software, and teams that deliver continuous value to users.
- Incubyte works with few clients at a time, on long-term engagements, with a product mindset.
- **Quality is an implicit requirement.** Users expect it but never ask for it, so it gets missed. Incubyte gives equal weight to scalability, maintainability, testability and security.
- **Guiding principles:**
  - Quality with Pragmatism
  - Extreme Ownership
  - Proactive Collaboration
  - Active Pursuit of Mastery
  - Client Success
  - Invite, Give & Act on Feedback
- **Ways of working:**
  - Pairing is a core practice.
  - Remote work runs on structured flexibility: autonomy, plus core hours and responsiveness.
  - Teams meet in person twice a year for a co-working sprint, and once a year for a retreat.

### Software craftsmanship

- The Manifesto for Software Craftsmanship (2009) came from concern that Agile had drifted away from engineering quality.
- It extends each Agile value:
  - Working software → **well-crafted** software
  - Responding to change → **steadily adding value**
  - Individuals and interactions → **a community of professionals**
  - Customer collaboration → **productive partnerships**
- **Why the how matters:** poorly crafted work still "works" on day one, but every later change gets slower and riskier. Craft keeps the system easy to change.
- Craftsmanship is not limited to developers. BAs, QA engineers and other team members contribute through the quality of their own work.
- For a BA, craftsmanship means understanding the business problem, asking the right questions, documenting clear requirements and ensuring that the proposed solution delivers actual value.

### Business analysis and the BA role

- The BABOK® Guide from the IIBA stands as the global standard for business analysis. It defines the field not just as documentation, but as enabling change. You define needs and recommend solutions that deliver actual value to stakeholders within a specific context.

- Consider the BA’s role. They dig past surface-level requests to find the real need. They engage everyone affected by the work. They map the current process, spot the gaps, and then shape how the solution gets communicated. Finally, they verify that the promised value was actually delivered.

- That’s how a BA keeps the *why* alive.

- It’s easy to rush. A BA shouldn’t immediately convert every stakeholder request into a requirement. Instead, pause. Understand the business reason. Look at the existing workflow. Gauge the expected outcome and possible impact first.

### BACCM and the six knowledge areas

**BACCM: six interrelated concepts, with no fixed order**

| Concept | Meaning |
|---|---|
| Need | A problem or opportunity |
| Change | The transformation made in response to a need |
| Solution | A specific way to satisfy a need in a context |
| Stakeholder | Anyone with a relationship to the change, need or solution |
| Value | Worth or usefulness to a stakeholder, in a context |
| Context | The circumstances around the change: culture, technology, environment |

**Six knowledge areas: groupings of tasks, not phases**

| Knowledge area | In one line |
|---|---|
| Business Analysis Planning & Monitoring | Plan the analysis approach, stakeholder engagement and governance |
| Elicitation & Collaboration | Draw out information from stakeholders and confirm it |
| Requirements Life Cycle Management | Trace, prioritise, approve and maintain requirements |
| Strategy Analysis | Current state → future state → change strategy and risks |
| Requirements Analysis & Design Definition | Specify, model, verify and validate requirements and designs |
| Solution Evaluation | Measure the value a live solution delivers, and remove barriers to it |

## Exercises

### Exercise 1: Worked example (AI-generated, for reference)

This example applies the six core concepts to a sample request, showing how the model can be used and not just recalled.

**Request:** "Add an export-to-Excel button to the claims dashboard."

| Concept | Analysis |
|---|---|
| Need | Ops analysts rebuild weekly claim reports by hand, which takes about 3 hours a week. The real need is faster reporting, not necessarily a button. |
| Change | Give analysts self-serve access to the claims data in a reusable format. |
| Solution | Options: an Excel export, a scheduled emailed report, or a built-in report view. An export is cheapest, but may only move the manual work elsewhere. |
| Stakeholder | Ops analysts (users), ops manager (receives reports), the security/compliance team (data leaving the system), and developers. |
| Value | Analyst time saved, plus fewer copy-paste errors in reports. |
| Context | Claims data contains personal information. This creates implicit requirements: role-based access, masking, and an audit log of exports. |

**What it shows:** Mapping all six concepts revealed two things the original request didn't mention:

- The underlying need (reporting time) might be better served by a scheduled report than by an export button.
- **Context** raised security requirements that nobody had asked for.

This is the "implicit requirements" idea from Incubyte's culture, in practice.

### Exercise 2: Applying BACCM to ERP exploration

- I took that same line of reasoning and applied it to an internal ERP scenario, looking at how business analysis and exploratory testing actually feed into one another.

- Consider this specific case: a user submits a leave request. The system should lock it down once the date passes. Instead, the cancellation option remains visible and active. That’s a clear disconnect between the intended logic and what’s happening on the screen.

| Concept | Analysis |
|---|---|
| Need | Ensure leave records remain accurate and users cannot perform inappropriate actions on past leave requests. |
| Change | Review the existing leave cancellation workflow and define when cancellation should be allowed. |
| Solution | Options could include business rules based on leave status, dates, approval status and user permissions. |
| Stakeholder | Employees, HR, managers, payroll team and the ERP development team. |
| Value | Accurate leave records, fewer manual corrections and better control over leave-related information. |
| Context | Different leave statuses and approval stages may affect cancellation eligibility. Historical records and payroll processing may also be impacted. |

**Questions I would ask before proposing a solution:**

- Can users cancel leave after the leave date has gone?
- Is the rule any different for approved, pending and rejected leave?
- Can HR or an admin get around the cancellation restriction?
- What if the leave has already been processed through payroll?
- Does the system keep an audit trail of cancellation attempts?

**Learning:** Rather than just flagging the 'cancel' button as a defect, I should first get to grips with the business rule that's intended to apply and the existing workflow. The behaviour we've seen could be a defect, it could be a missing business rule or it could be a feature that was deliberately implemented and we just haven't been made aware of it.

### Exercise 3: Connecting exploratory testing with business analysis

During my internal ERP and MyPayroll exploration, I came across different scenarios that helped me understand the importance of looking beyond the happy path.

Some examples from my observations:

| Observation | BA perspective | QA / Exploratory testing perspective |
|---|---|---|
| Leave cancellation remains available after the leave date | Clarify the business rule for cancellation based on leave dates and status. | Explore different leave statuses and date combinations. |
| Duplicate POD/search entries after project or POD changes | Understand whether the expected behaviour is to update an existing user record or create another one. | Explore user movement across projects, bench and POD changes. |
| Expense drafts are visible to other users | Clarify visibility and ownership expectations for draft expenses. | Explore access and visibility using different user accounts and permissions. |
| Skip button behaviour on the feedback page | Understand whether skipping is an allowed action and what the expected outcome should be. | Explore navigation, validation and feedback submission scenarios. |

**What I learned:**

- Exploratory testing is not just about clicking around. It's about understanding the app, having questions, exploring different scenarios and finding the odd bit of behaviour that you wouldn't have anticipated.
- Business analysis is used to establish what the application is meant to do.
- Exploratory testing is the way of finding out what the application actually does.
- Combining both approaches will help to identify the gap between what the business expects and what the system actually does.
- Every observation must be underpinned by evidence, reproducible steps, impact and a clear definition of the expected behaviour.

### Exercise 4: Ownership as a BA

I linked the concept of Extreme Ownership with the internal tools initiative.

Whilst looking at the ERP functionality, I realised that understanding the system as it is is a vital first step before you go any further in the way of suggesting improvements or development.

My approach to taking ownership would be:

1. **Understand the current state:** look at the existing ERP modules, the workflows, the user roles and the functionality.
2. **Identify the gaps:** record the confusing bits, the duplication, the missing bits, the usability issues.
3. **Ask questions:** get in touch with the relevant stakeholders and team members to clarify the business rules and expectations.
4. **Document the findings:** clear observations, assumptions, dependencies, risks and open questions.
5. **Propose improvements:** suggest the changes that will deliver the most business value and meet the needs of the user rather than simply making assumptions.
6. **Follow through:** confirm the proposed changes have been implemented and that the desired outcome has in fact been achieved.

My view of ownership is that it doesn't mean you independently decide everything. It means you take ownership of understanding the problem, you take ownership of communicating the uncertainties, you take ownership of getting the right people involved and then you take ownership of following through until there's clarity or there's an agreed outcome.

### Exercise 5: The six knowledge areas in my own work

I mapped activities from my EventLab assignment and internal ERP exploration to the six BABOK knowledge areas, to check I can recognise them in real work.

| Knowledge area | Where I have done this |
|---|---|
| Business Analysis Planning & Monitoring | ERP: deciding to involve a few domain users who use the ERP in different ways before finalising requirements |
| Elicitation & Collaboration | ERP: preparing questions on leave cancellation rules (status, dates, payroll impact, HR override) to clarify with stakeholders |
| Requirements Life Cycle Management | EventLab: preparing the runbook so requirements and behaviour stay maintainable for future enhancements |
| Strategy Analysis | ERP: exploring existing modules and workflows to understand the current state before suggesting improvements |
| Requirements Analysis & Design Definition | EventLab: reviewing the SDD and requirements for clarity and completeness; contributing to specifications |
| Solution Evaluation | ERP: finding gaps between expected and actual behaviour (leave cancellation, duplicate POD entries, feedback skip button) |

**What I learned:** I had already been doing work in most knowledge areas without naming it. Next, I want to apply them more accurately, for example planning my analysis approach upfront at the start of each new piece of work.

## Applying craftsmanship to my previous work

### EventLab experience

During my EventLab assignment, I started by reviewing the SDD to understand the business requirements and application workflows.

Here are some of the ways I contributed:

- Validated the requirements to understand the expected behaviour of the application.
- Explored workflows and pinpointed UI and functional gaps before they were flagged by the business.
- Brought both QA and BA perspectives into play while assessing the proposed solution.
- Contributed to the proposal, specifications, and test-related documentation.
- Prepared the runbook to assist with future enhancements.
- Highlighted small usability issues and improvements, including paper cuts.

**Connection to craftsmanship:**

This experience taught me that reviewing a requirement goes beyond just checking if it’s documented. It’s about ensuring that it’s clear, complete, practical, and aligned with the desired business outcome.

A well-documented requirement paired with a thoughtful review can significantly reduce ambiguity for developers, enhance testing coverage, and prevent rework down the line.

## Reflection

I used to view craftsmanship primarily as an engineering concept, but I’ve come to realize it’s just as relevant to a BA's role. The quality of requirements, the questions we ask, the documentation we produce, and the decisions we make all directly impact the quality of the final solution.

For instance, during my internal ERP exploration, I noticed that the option to cancel leave was still available even after the leave date had passed. Instead of jumping to conclusions and labeling it as a defect, I understood the importance of first figuring out why that option exists, what the intended business rule is, and how different leave statuses might influence the behavior.

This is where business analysis and exploratory testing really complement each other. Exploratory testing allows me to uncover unexpected behaviors, while business analysis helps me grasp the underlying needs and expected outcomes.

I also see a connection between Extreme Ownership and my current ERP exploration. Rather than just pointing out issues, I aim to understand existing workflows and engage in discussions about observations.

Quality with Pragmatism means providing the right level of analysis without creating unnecessary documentation. Proactive Collaboration means involving the right people instead of making assumptions. Ultimately, my responsibility does not end when a requirement is documented or handed over. I should also be interested in whether the solution delivers the intended business value.

For the ERP, we adopted an approach where we gather feedback and improvement ideas from domain users who use the tool in different ways, treat them as our clients, and prepare standard requirements for improving the tool.

## AI use

- **Tools:** Claude
- **Used for:**
  - Generating practice scenarios and recall questions — see [Exercise 1](#exercise-1-worked-example-ai-generated-for-reference).
  - Structuring the learning notes in the COE submission format.
- **What I checked and corrected:**
  - Labelled Exercise 1 as an AI-generated worked example, and used my own ERP and EventLab experience for Exercises 2–5.
  - Identified areas where actual business rules still need stakeholder clarification rather than making assumptions.
  - Generating a worked example and recall questions — see [Exercise 1](#exercise-1-worked-example-ai-generated-for-reference).

## Open questions

- Which BABOK knowledge areas do Incubyte BAs spend most of their time in on a typical engagement?
- What level of documentation is expected when exploring and proposing improvements to internal tools?

## Changes after review

- 

# Part 1 · Day 5 — Elicitation: Getting Domain Knowledge Out of Busy People

**Date completed:** 2026-11-10 · **Time spent:** ~9 hours

**System explored:** The Incubyte ERP (Frappe) looked different to me from the perspective of roles I hadn’t seen before. On Days 3–4, I’d only used it as an employee; here, I learned how **HR** and a **team lead** work with it through two recorded Teams sessions with screen sharing. The transcripts remain private; this file contains my summary.

## Success criteria

| Criterion (copied from the planner) | Done? | Evidence (link or section below) |
| --- | --- | --- |
| Knows core elicitation techniques | Yes | [Elicitation techniques](#techniques) · [Techniques I used](#exercise-3) |
| Prepares sharp targeted questions in advance | Yes | [Exercise 1: my prepared questions, reviewed](#exercise-1) · [Exercise 2: sharper follow-ups](#exercise-2) |
| Distinguishes internal questions from specification-moving questions | Yes | [Internal vs spec-moving](#internal-vs-spec) · [Exercise 2](#exercise-2) |
| Narrows ten questions to the five that matter most | Yes | [Exercise 2: ten cut to five](#exercise-2) |
| Runs and documents a real elicitation conversation | Yes | [Exercise 3: two real sessions](#exercise-3) |

## Key learnings

<a id="techniques"></a>

### Core elicitation techniques

Elicitation is how a BA discovers the information needed to write requirements. Most of it happens in short sessions with one or a few people, not big full-day workshops.

| Technique | What it is | Best when |
| --- | --- | --- |
| **Interview** | A prepared conversation with one person or a small group | You need one expert's knowledge and reasoning |
| **Observation** | Watching someone do the work (in person or by screen share) and asking about the "what if" cases | People find it hard to explain what they do |
| **Document analysis** | Reading what already exists: specs, manuals, tickets, old forms | Stakeholder time is scarce; do this first |
| **Workshop** | A facilitated session where several stakeholders work through something together | Several people must agree, or knowledge is spread across roles |
| **Walkthrough / prototype review** | Reacting to a draft diagram, wireframe or screen | You want people to spot what's missing or wrong |
| **Survey** | Written questions to many people | You need input from more people than you can meet |

Most BAs use a mix of both. Early in my career, Day 2 focused on **document analysis** (the EventLab spec), while Day 3 was more about **interface analysis**—looking at how the ERP exchanges data.

### Sharp, targeted questions instead of open-ended ones

Busy people give short answers to vague questions. A sharp question is specific, points at one decision, and is easy to answer from the person's own experience.

| Open-ended | Sharp and targeted |
| --- | --- |
| "What's the most time-consuming part?" | "Show me the last time you got stuck. What did you click, and what did you expect?" |
| "Any reports that take effort?" | "Which number do you count by hand today, and how often?" |
| "Any edge cases?" | "What happens when a candidate skips the education section?" |

<a id="internal-vs-spec"></a>

### Internal questions vs specification-moving questions

| | Internal question | Specification-moving question |
| --- | --- | --- |
| Purpose | Helps *me* understand or plan | Changes a requirement, scope or decision |
| Answer comes from | Often findable myself (docs, Network tab, the ERP team) | Only the stakeholder or decision-maker |
| Example | "Which Frappe version is it on?" | "Who may change a review result before the reviewer submits it?" |
| Where to ask | A quick message, or not at all | The elicitation session |

**My test:** *If I get this answer, does any line of the spec change?* If not, it's internal, and it shouldn't use a busy person's session time.

## Exercises

<a id="exercise-1"></a>

### Exercise 1: My prepared questions, reviewed after the sessions

I prepared these before both sessions and asked them in the same order to each person.

| # | Question I asked | Open or sharp? | How it landed |
| --- | --- | --- | --- |
| 1 | What do you mostly use the ERP for? | Open, but a good opener | ✅ Mapped each role's main workflows |
| 2 | What's the most time-consuming part? | Open | ❌ Both said "nothing really", then gave pain points later |
| 3 | Walk me through the last time you got stuck or confused | **Sharp** (a specific moment) | ✅✅ Richest answers, especially with screen share |
| 4 | Did you ever skip the portal and use email, Teams or Zoho instead? | **Sharp** | ✅ Revealed real workarounds (offer letters via Zoho, asking colleagues) |
| 5 | Any approvals or reports that take the most effort? | Open | ⚠️ Both said "not really"; one follow-up found a reporting need |
| 6 | If you could fix one thing tomorrow, what would it be? | **Sharp** (forces one priority) | ✅ Gave each role's top priority |
| 7 | What feature would make the tool more useful? | Open | ✅ Surfaced new features (referrals, received feedback) |
| 8 | Anything else we should know? | Catch-all | ⚠️ Lead raised accessibility; HR had nothing more |

**What this taught me:** questions about a **specific moment** (3, 4, 6) worked far better than questions about **general effort** (2, 5). Screen sharing turned question 3 into observation, which is where most findings came from.

<a id="exercise-2"></a>

### Exercise 2: Ten sharper follow-up questions, cut to five

Based on what I learned, these are the questions I'd prepare for the next round with HR, managers and the ERP owner.

| # | Question | Type |
| --- | --- | --- |
| 1 | Which education fields must be mandatory, and does any type of hire skip them? | **Spec-moving** |
| 2 | Who may set a repo review result before the reviewer submits it: HR only, or the hiring manager too? | **Spec-moving** |
| 3 | Should the "NDA sent" and "IT code of conduct sent" confirmations be removed, or replaced by "document attached = confirmed"? | **Spec-moving** |
| 4 | How often does the offer approval button disappear, and what happens to that offer today? | **Spec-moving** (decides priority) |
| 5 | What differs in a contractor or consultant offer: fields, template, approvers? | **Spec-moving** |
| 6 | What statuses does a referral go through, and who must be told at each one? | **Spec-moving** |
| 7 | Which modules should an employee see vs a manager vs HR (others' leaves, reports, assignments)? | **Spec-moving** |
| 8 | Which Frappe version is the ERP on? | Internal: I can ask the ERP team |
| 9 | Can I see the HR team's survey responses? | Internal: logistics |
| 10 | What is "My Assignments" for? | Internal: the ERP team or documentation can tell me |

**Kept: 7, 1, 2, 4, 6.**

| Cut | Reason |
| --- | --- |
| 8, 9, 10 | Internal: I can find the answers without using a stakeholder's time |
| 3 | Small and low-risk; can be decided in a design review |
| 5 | A whole new feature; worth its own session once current issues are fixed |

**Why these five:** 7 affects every user and is a security question (it also answers my [Day 4](../day4/day-04-specification-work-breakdown.md) gap 1). 1 is HR's "fix tomorrow" item. 2 blocks HR's daily review work. 4 is the only reported failure that pushes work outside the ERP. 6 is HR's most-wanted new feature, and it can't be specified without its statuses.

<a id="exercise-3"></a>

### Exercise 3: Two real elicitation sessions

| | Session 1 | Session 2 |
| --- | --- | --- |
| Date and length | 2 Nov 2026, ~26 minutes | 3 Nov 2026, ~19 minutes |
| With | HR (hiring and onboarding) | Team lead (as an employee user); two colleagues joined and asked follow-ups |
| Format | Teams call, transcription on, screen share | Teams call, transcription on, screen share |
| Techniques | Structured interview + observation of a walkthrough; plus a survey form for the wider HR team (link to be shared) | Structured interview + observation of a walkthrough |

#### What I learned: HR

**Main workflows**

1. **Hiring to onboarding:** Create a job applicant → draft the offer letter → get approval from HR approvers → candidate accepts → candidate completes a short joining form with basic details and IDs → HR sends the full onboarding form → HR verifies the details → on the joining date, convert the candidate into an employee.
2. **Repo review:** HR uploads candidates’ take-home assessments → interviewers review them and record the outcome.

**Improvement areas**

| Area | What happens today | What HR would like |
| --- | --- | --- |
| Onboarding form: education | Education sits under the Professional details tab and isn't mandatory; HR estimates ~80% of candidates skip part of it, causing back-and-forth | A separate, mandatory Education tab (**HR's #1 fix**) |
| Onboarding form: redundant fields | "NDA sent" and "IT code of conduct sent" confirmations are required even though the signed documents are attached | Remove the confirmations |
| Onboarding form: employer fields | Candidates not currently working put their last employer under "current" | An info tooltip explaining each field |
| Editing a submitted form | "Edit" is hidden under Actions; HR cancelled a form by mistake and the team had to refill it | A clearly visible Edit button |
| Offer approval | The action button sometimes disappears, or the approval email doesn't go; offers were sent through Zoho instead | Reliable approval flow |
| Contract hires | No contractor or consultant option or template; handled in Zoho separately | A contractor option with its own template |
| Assessment notes | Can't attach files (videos, spreadsheets), so they're shared over personal chat | Attachments in notes, visible to reviewers |
| Review results | HR can only override a result after the reviewer enters one | HR can set the result when a reviewer confirms in chat |
| Reports | Counted manually | Assessments by tech stack and date range, with accepted/rejected counts (nice to have) |
| Referrals (new) | Microsoft Form → team sheet → manual status updates; referrers often ask for status | Referrals tracked in the ERP with status updates and emails (**HR's top new feature**) |

#### What I learned: team lead (employee view)

**Main uses:** applying for leave, giving feedback and checking feedback scores, and claiming reimbursements.

| Area | What happens today | What they'd like |
| --- | --- | --- |
| Navigation | Every action means going back to the home desktop; the side panel doesn't list everything | A consistent, collapsible side panel with all modules (**#1 fix**) |
| Reimbursement | Hard to find; once submitted, it can't be checked or edited; once had to ask a colleague how to fill it | Easier to reach, and viewable after submitting |
| Role-based visibility | Employees see things they can't use or shouldn't see: everyone's leaves, reports, candidates' review statuses | Show only what each role needs |
| Visual design | Dull colours; buttons and links look alike until hovered | Clear colour coding and obvious buttons |
| Team Pod Chart | A crowded pie chart; the client only shows on hover; zooming jumps around | A tree-style org chart |
| Feedback | Can only see feedback given, not received | See received feedback, optionally anonymous |
| Accessibility | Tab key skips elements; colour contrast is poor; never tested | Accessibility testing |

#### What changes a specification

- **Role-based visibility is a real gap, not just my assumption.** On Day 4 I *assumed* employees see only their own profile (gap 1). The lead's session showed the ERP currently shows employees others' leaves and candidates' review statuses. That moves the decision from "assumption" to "confirmed problem".
- **Accessibility needs its own requirement.** I had only done exploratory testing; neither my Day 4 spec nor the ERP covers it.
- **Two roles, two different #1 priorities:** HR wants the onboarding form fixed; the lead wants navigation fixed. A spec has to choose, so this goes to whoever prioritises the ERP backlog.

**Surprises:** so much happens *outside* the ERP: offer letters go out through Zoho, referrals are collected in a Microsoft Form and a spreadsheet, and review results are agreed on in chat. Every workaround points to a requirement no one has documented.

**Follow-ups:** Share the survey form link with HR so they can pass it on to the wider team, as promised at the end of session 1. Ask the five questions from [Exercise 2](#exercise-2), and find out what “My Assignments” is for—neither person knew.

**What I'd do differently:** Start by asking, “Can you show me the last time you got stuck?” rather than “What takes the most time?” And ask them to share their screen right away—that’s where I found most of the useful insights.

## Reflection

Before these sessions, I was only used the ERP as an employee, so getting a look at HR’s side was eye-opening. Their entire hiring and onboarding process runs through screens I never seen before. When I asked broad questions like, “What takes the most time?”, both people said, “Nothing really.” But when I asked them to show me the last time they got stuck and share their screens, the real issues started to come out. I was also surprised by how much happens outside the ERP: offer letters are handled through Zoho, referrals through a form and spreadsheet, and review results are agreed on in chat. Each workaround points to a requirement that hasn’t been written down. The sessions also confirmed one of my Day 4 assumptions: employees can currently see other people’s leave and candidates’ review statuses. Next time, I’ll lead with “show me” questions and ask people to share their screens from the start.

## AI use

I ran both sessions myself using questions I’d prepared in advance. Afterwards, I shared the Teams transcripts with Claude to help summarise them in this file using the COE template and suggest sharper follow-up questions. I checked the summary against the transcripts and corrected a few details:

- Claude’s first plan focused on an interview about a colleague’s ERP demo. I replaced it with the actual sessions I’d already run with HR and a team lead.

The transcripts aren’t included in this repo.

## Open questions

1. Who decides priority between roles when HR and employees each want a different "#1 fix"?

## Changes after review

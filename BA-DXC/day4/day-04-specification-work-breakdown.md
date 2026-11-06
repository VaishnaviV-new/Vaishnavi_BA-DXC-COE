# Part 1 · Day 4 — Specification & Work Breakdown: Writing It Down Precisely

**Date completed:** 2026-11-06 · **Time spent:** ~9 hours

**Flow specified:** Viewing my employee profile in the Incubyte ERP (Frappe), built from my [Day 3](../day3/day-03-web-application-fluency.md) findings and the field-extraction method from [Day 2](../day2/day-02-discovery-unfamiliar-portal.md). All employee data shown is dummy.

## Success criteria

| Criterion (copied from the planner) | Done? | Evidence (link or section below) |
| --- | --- | --- |
| Writes a precise developer-ready specification | Yes | [Exercise: My Profile specification](#spec) · [Field specification](#field-spec) |
| Writes user stories and testable acceptance criteria | Yes | [User story](#story) · [Acceptance criteria](#criteria) |
| Captures edge cases and empty states in acceptance criteria | Yes | [Rule 3: empty values](#rule-3) · [Rule 5: expiry boundaries](#rule-5) · [Rule 6: failed load](#rule-6) |
| Completes the ATDD course sections | Yes | [ATDD course takeaways](#atdd) |
| Reads both acceptance-criteria articles | Yes | [Article takeaways](#articles) |

## Key learnings

### What makes a specification precise

A specification is precise when a developer can build from it and a tester can verify it without needing to ask follow-up questions. Every field, branch, and empty state should be decided and documented—not left to whoever happens to build it. If the developer has to guess, they’re defining the requirement, and that decision hasn’t been recorded.

### User stories

A user story says **who** wants **what** and **why**:

> As a *[who]*, I want *[what]*, so that *[why]*.

The story is the conversation starter. The acceptance criteria are what make it buildable and testable.

### Acceptance criteria in Given-When-Then

| Part | Says | Example |
| --- | --- | --- |
| **Given** | The starting situation | Given Asha is signed in and linked to employee E0000 |
| **When** | The action | When she opens My Profile |
| **Then** | The exact, observable result | Then her employee ID "E0000" is shown |

Rules I followed:

- **Concrete data, not abstractions:** "employee E0000", not "an employee".
- **One behaviour per scenario.**
- **Falsifiable:** if nobody can say how it could fail, it isn't a criterion. "The page loads correctly" fails this test; "'Not provided' is shown" passes.
- **What, not how:** criteria describe what the user sees, not how it's built or tested.

### Acceptance criteria capture edge cases and empty states

A happy path alone leaves the hardest questions to the developer. I used these patterns to go beyond it:

| Pattern | Question it forces |
| --- | --- |
| Empty / first run | What does the user see when there's nothing there? |
| Boundary | What happens exactly at the limit, and just past it? |
| Negative path | What is refused, and what does the user see? |
| Failure & recovery | What if the system behind it doesn't answer? |
| Authorization | What happens when someone tries something they're not allowed to do? |

### Where each criterion comes from

I tagged every criterion with where it came from, so a reader can tell an agreed rule from a guess:

| Tag | Means |
| --- | --- |
| `[stated: source]` | Written in a source I read (quotable) |
| `[derived: basis]` | Forced by another stated rule |
| `[assumed → gap N]` | My decision, filling a hole; linked to a gap in the ledger |

A **gap ledger** then lists what nobody has decided yet, checked against 14 dimensions (roles, field data, states, boundaries, failures and so on), and marks which gaps block development.

<a id="atdd"></a>

### ATDD course takeaways

- **An acceptance test is an executable specification.** The Given-When-Then examples I write are more than documentation: they become automated tests that verify the system does what the story asks.
- **Describe the “what,” not the “how.”** Tests that use the language of the problem (“Asha opens My Profile”) hold up as screens and code change. Tests tied to specific buttons or page elements tend to break whenever the UI changes.
- **Acceptance testing as a language.** The lesson title points to creating a shared vocabulary of domain actions—like “open profile” or “sign in as employee”—that tests can reuse. That way, they read like the business, not the code.
- Acceptance criteria is reference for Dev/QA to develop/verify the feature.

<a id="articles"></a>

### Article takeaways

- Acceptance criteria define when a story is done. They establish its scope and give the product team and developers a shared understanding of what’s expected.
- They should go beyond the happy path and address negative scenarios, error handling, performance expectations, and what’s out of scope.
- Strong criteria are written from the user’s perspective. They describe what should happen—not how to build it—and are clear and testable.
- There are three common styles: scenario-based (user journeys), rule-based (a checklist of conditions), and hybrid. Hybrid is often best for complex features. My Day 4 spec uses this approach, pairing business rules with scenarios.
- Unclear criteria can result in features that pass testing but miss the real need, unclear error handling, rework, and scope creep.

## Exercises

<a id="spec"></a>

### Exercise: My Profile specification

#### Context

An Incubyte employee views their own record in the ERP. There’s no written requirement for this screen, so these criteria are based on what I observed on Day 3. What I saw and what the system does—not what was agreed—so nearly every criterion is marked `[assumed]`. The few `[stated]` criteria are the key finding: they show which decisions HR or the ERP owner still needs to confirm.

<a id="story"></a>

#### User story

> As an Incubyte employee, I want to view my own employee profile in the ERP, so that I can check my HR details are correct.

<a id="field-spec"></a>

#### Field specification

From the Day 3 response for my own profile (`get_employee_details`, `GET`, `200`). Path is inside `message.data`.

| Screen label | Response field | Format | Empty as stored | Shown when empty |
| --- | --- | --- | --- | --- |
| Employee ID | `name` | Text, mostly `A9999`; some `A-9999` or longer | Never empty (193 of 193) | — |
| Name | `first_name`, `last_name` | Text | `last_name` = `null` for 3 people | First name only |
| Status | `status` | Text, e.g. `Active` | Not seen empty | Not provided |
| Date of joining | `date_of_joining` | `YYYY-MM-DD` | Not seen empty | Not provided |
| Reporting manager | `reports_to` | Employee ID | `null` (44) **or** `""` (13) | Not provided |
| Photo | `image` | Path or URL | `null` (73) or `""` (1) | Initials avatar |
| Passport number | `passport_number` | Text | — | Not provided |
| Passport expiry | `valid_upto` | `YYYY-MM-DD` | `null` | Not provided |
| Contract end date | `contract_end_date` | `YYYY-MM-DD` | `null` | See gap 2 |

<a id="criteria"></a>

#### Acceptance criteria

##### Rule 1: An employee can view only their own profile

**Scenario: Opening my own profile** `[assumed → gap 1]`
```gherkin
Given Asha Dummy is signed in and linked to employee "E0000"
When she opens My Profile
Then her name "Asha Dummy", employee ID "E0000", status "Active" and date of joining are shown
```

**Scenario: Trying to open someone else's profile** `[assumed → gap 1]`
```gherkin
Given Asha Dummy is signed in
When she tries to open the profile of employee "E0001"
Then she sees a "Access Denied" message
And no detail of employee "E0001" is shown
```

**Scenario: Account with no employee record** `[assumed → gap 1]`
```gherkin
Given a signed-in account that is not linked to any employee
When it opens My Profile
Then it sees "No employee record is linked to your account"
And it does not see a blank profile or an error page
```

##### Rule 2: Employee ID is shown exactly as stored

**Scenario: IDs in every stored format** `[assumed → gap 2]`
```gherkin
Given an employee whose ID is stored as <stored ID>
When they open My Profile
Then the employee ID reads <shown as>

Examples:
  | stored ID              | shown as               |
  | E0000                  | E0000                  |
  | A-1234                 | A-1234                 |
  | E000012345678901234567 | E000012345678901234567 |
```

<a id="rule-3"></a>

##### Rule 3: "Empty" always looks the same, however it is stored

**Scenario: No reporting manager** `[assumed → gap 2]`
```gherkin
Given Asha's reporting manager is stored as <stored value>
When she opens My Profile
Then reporting manager reads "Not provided"

Examples:
  | stored value |
  | null         |
  | "" (empty)   |
```

**Scenario: No last name** `[assumed → gap 2]`
```gherkin
Given Asha's first name is "Asha" and her last name is empty
When she opens My Profile
Then her name reads "Asha"
And the word "null" does not appear
And there is no trailing space after the name
```

**Scenario: No photo** `[assumed → gap 2]`
```gherkin
Given Asha Dummy has no photo, stored as <stored value>
When she opens My Profile
Then an avatar with her initials "AD" is shown
And no broken-image icon is shown

Examples:
  | stored value |
  | null         |
  | "" (empty)   |
```

##### Rule 4: Dates are shown in one readable format

**Scenario: Date of joining** `[assumed → gap 2]`
```gherkin
Given Asha's date of joining is stored as "2024-01-15"
When she opens My Profile
Then date of joining reads "15 Jan 2024"
```

<a id="rule-5"></a>

##### Rule 5: An expired passport is flagged

**Scenario: Passport expiry around today** `[assumed → gap 4]`
```gherkin
Given today is 6 Nov 2026
And Asha's passport expiry is <expiry>
When she opens My Profile
Then passport expiry reads <shown as>

Examples:
  | expiry      | shown as                   |
  | 2026-11-05  | 05 Nov 2026 – Expired      |
  | 2026-11-06  | 06 Nov 2026 – Expired      |
  | 2026-11-07  | 07 Nov 2026                |
```

**Scenario: No passport expiry recorded** `[assumed → gap 2]`
```gherkin
Given Asha has no passport expiry recorded
When she opens My Profile
Then passport expiry reads "Not provided"
And no "Expired" label is shown
```

<a id="rule-6"></a>

##### Rule 6: A failed load is never shown as empty data

**Scenario: Profile service does not respond** `[assumed → gap 5]`
```gherkin
Given the profile service does not respond
When Asha opens My Profile
Then she sees "Couldn't load your profile" with a "Try again" button
And no field reads "Not provided"
```

**Scenario: Trying again after a failure** `[assumed → gap 5]`
```gherkin
Given Asha sees "Couldn't load your profile"
And the profile service is responding again
When she selects "Try again"
Then her profile is shown with employee ID "E0000"
```

##### Rule 7: The passport number is partly hidden

**Scenario: Passport number on screen** `[assumed → gap 13]`
```gherkin
Given Asha's passport number is "X1234567"
When she opens My Profile
Then passport number reads "••••4567"
```

##### Rule 8: Employment status is shown as stored

**Scenario: Active employee** `[assumed → gap 3]`
```gherkin
Given Asha's employment status is "Active"
When she opens My Profile
Then status reads "Active"
```

#### Coverage & gap ledger

**Act on gaps 4 and 5 first.** They decide *what* gets built, not just how well.

| # | Dimension | Severity | Gap | Who decides |
| --- | --- | --- | --- | --- |
| 1 | Actors & roles | Assumption | Employees see only their own profile; whether managers or HR can view others here is undecided | HR / ERP owner |
| 2 | Field-level data | Assumption | Date display format, the wording for empty values, and showing IDs unchanged; also whether an empty contract end date means "permanent" or "unknown" (Note) | HR / ERP owner |
| 3 | States & transitions | Assumption | Only "Active" was observed; what an employee who has left or is inactive sees, and whether they can still sign in | HR |
| 4 | Boundaries | **Blocker** | Whether an expired passport is flagged at all or only displayed. Flagging is a different feature, not a detail | HR / compliance |
| 5 | Dependency failure | **Blocker** | Whether a failed load shows an error or blank fields. Blank fields would look like "no data" when the system is actually unable to load | ERP owner |
| 8 | Lifecycle coverage | Note | Only viewing is specified; can an employee request a correction from here? | HR |
| 10 | Cross-surface impact | Note | The Team Pod Chart shows the same employees with fewer fields; should names and IDs match exactly? | ERP owner |
| 11 | Non-functional | Note | No load-time target; the profile response carries 148 fields | Developers |
| 12 | Observability | Note | No way defined to know in production if profiles fail to load | Developers |
| 13 | Security & compliance | Assumption | Whether the passport number is masked on screen, and whether profile views are logged | IT security / HR |

Fourteen checked: 6 concurrency, 7 idempotency and 14 rollout are N/A (read-only view of an existing screen; nothing is written) · 9 pre-existing data rides on gap 2 (older ID formats such as `A-9999`).

Sources: read my Day 3 Network capture (employee list and own-profile responses, with empty-value counts) and my Day 2 field-extraction method. Unread: any ERP requirement document, HR policy or ticket for this screen (none available). "Who decides" is my inference; to be corrected to the real roles.

#### Assumptions applied

1. **Employees see only their own profile:** used in Rule 1. If wrong, managers or HR need their own scenarios. Resolves gap 1.
2. **One empty wording, "Not provided", for both `null` and `""`:** used in Rules 3 and 5. If wrong, every empty-state scenario changes wording. Resolves gap 2.
3. **Dates shown as "15 Jan 2024":** used in Rules 4 and 5. If wrong, every date example changes. Resolves gap 2.
4. **Expired passports are flagged, including on the expiry day:** used in Rule 5. If wrong, the "Expired" label is dropped or the boundary moves by a day. Resolves gap 4.
5. **A failed load shows an error and a retry, never blank fields:** used in Rule 6. If wrong, users could mistake a failure for missing data. Resolves gap 5.
6. **Passport number masked to the last 4 characters:** used in Rule 7. If wrong, the full number is shown. Resolves gap 13.

**Verdict: ready for development once gaps 4 and 5 are confirmed.** Everything else can be built on the stated assumptions and adjusted if they change.

## Reflection

What caught me off guard was how many criteria I had to mark as “assumed.” On Day 3, I could see exactly what the ERP did, but none of it had been recorded/documented as an agreed requirement. Seeing the system in action didn’t mean I knew its behavior was expected. Writing Given-When-Then scenarios made me pin down details that a general description might gloss over—like whether a passport that expires today is considered expired, or what the screen should display if the reporting manager is null or blank. It was rewarding to see my Day 2 and Day 3 findings translate directly into scenarios. In my BA work, I’ll include open decisions alongside the spec so developers don’t have to guess and QA dont have to test those guess as actual results.

## AI use

I used Claude to help structure this file to the COE template, and then worked with it to  adjust the content into my own words.

## Open questions

1. When there's no written requirement, is it acceptable for a BA to propose behaviour as tagged assumptions, or should the spec wait for stakeholders first?

## Changes after review

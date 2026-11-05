# Part 1 · Day 1 — QA Automation Fundamentals & Path Selection

**Date completed:** 2026-11-05 · **Time spent:** ~6 hours

**Track:** QA Manual to Automation (common for all)

## Success criteria

| Criterion (copied from the planner) | Done? | Evidence (link or section below) |
| --- | --- | --- |
| Understands test pyramid and automation principles | Yes | [Test pyramid](#pyramid) · [ROI](#roi) |
| Can explain when to automate vs manual test | Yes | [Automate vs manual](#automate-vs-manual) · [Exercise 1](#exercise-1) |
| Knows difference between functional and non-functional testing | Yes | [Types of testing](#types) · [Exercise 1](#exercise-1) |
| Makes informed decision on JavaScript vs Python track | Partly | [Exercise 2: comparing the two tracks](#exercise-2). Compared both tracks and identified the questions that decide the choice; the choice itself is made later in the training |
| Understands tool ecosystem for chosen track | Yes | [Tool ecosystems](#tools) · [Exercise 2: tools on each track](#exercise-2) |
| Documents personal testing philosophy | Yes | [Exercise 3: my testing mindset](#exercise-3) |

## Key learnings

### Manual vs automation testing

| | Manual testing | Automated testing |
| --- | --- | --- |
| Who runs it | A person, step by step | A script, run by a tool |
| Good at | Exploring, judging how something feels, spotting the unexpected | Repeating the same checks quickly and exactly |
| Weak at | Repetition: slow, and people get tired and miss things | Anything it wasn't told to check |
| Cost | Every run costs a person's time | Costs time to write and maintain, then runs cheaply |

They don't replace each other. Automation checks what we already know should work; manual testing finds what we didn't think of.

<a id="pyramid"></a>

### Test pyramid

```
            /\
           /E2E\         few: slow, realistic, fragile
          /------\
         /Integration\   some: do parts work together?
        /--------------\
       /      Unit      \  many: fast, small, cheap
      /------------------\
```

| Level | What it checks | Example | Speed |
| --- | --- | --- | --- |
| Unit | One small piece of code on its own | A function that formats a date as `YYYY-MM-DD` | Milliseconds |
| Integration | Two or more parts working together | Saving a form stage actually writes the record to the database | Seconds |
| E2E (end-to-end) | A whole user journey through the real UI | Candidate opens link, fills every stage, signs, sees "done" | Minutes |

**Principle:** push each check as low in the pyramid as it can go. If a unit test can catch a bug, don't wait for a slow E2E test to catch it. An "ice-cream cone" (mostly E2E, few unit tests) is slow and breaks often.

<a id="automate-vs-manual"></a>

### When to automate vs test manually

| Automate when the test is… | Keep it manual when the test is… |
| --- | --- |
| Run often (every build, every release) | Run once or rarely |
| On a stable feature | On a feature still changing every week |
| Repetitive or data-heavy (many inputs) | Exploratory: "what happens if…?" |
| Business-critical (login, payment, saving data) | About look, feel or usability |
| Easy to judge pass/fail exactly | Needing human judgement to decide pass/fail |

<a id="types"></a>

### Types of testing

| Type | Question it answers | Example |
| --- | --- | --- |
| **Functional** | Does it do the right thing? | Choosing "No" to "Do you live in this country?" skips the sponsorship questions |
| **Non-functional** | Does it do it well enough? | Performance (page loads fast), security (expired link reveals nothing), accessibility, usability on a phone |
| **Regression** | Does what worked before still work after a change? | Re-running the onboarding checks after a new field is added |

Regression isn't a separate kind of check, it's *when* you re-run functional and non-functional checks. Because it's repeated after every deployment changes, it's the most common reason to automate those.

<a id="roi"></a>

### Understanding ROI of automation

ROI compares the cost of an automated test with the time it saves.

```
Cost  = time to write + time to maintain
Saved = (manual time per run) × (number of runs)
Worth it when Saved > Cost
```

Illustrative example (numbers made up to show the idea):

| | Hours |
| --- | --- |
| Manual regression run | 2 per week |
| Writing the automated suite | 16 once |
| Maintaining it | 1 per week |
| Net saving per week | 2 − 1 = 1 |
| Break-even | 16 ÷ 1 = **16 weeks** |

Automation only pays off if the suite stays in use for at least four months. A test for a feature that’s about to change—or will only run once—won’t recoup its cost.

### QA automation career paths

| Path | Focus |
| --- | --- |
| Manual / exploratory QA | Test design, finding risk, domain knowledge |
| QA automation engineer | Writing and maintaining automated test suites |
| SDET (Software Development Engineer in Test) | Test frameworks, tooling, testing inside the code |
| Performance / security tester | Specialist non-functional testing |
| QA lead / quality coach | Test strategy, helping the whole team own quality |

My BA background has built strengths in reading specs, spotting branches and identifying empty states—all of which feed directly into test design, a step every path depends on.

<a id="tools"></a>

### Language and tool ecosystems

**Language and tool are separate choices.** Playwright works in both JavaScript/TypeScript and Python.

| Tool | Languages | Notes |
| --- | --- | --- |
| Playwright | JS/TS, Python, Java, .NET | Modern; auto-waits for elements; Chromium, Firefox and WebKit |
| Cypress | JS/TS only | Popular with front-end teams; not an option for Python |
| Selenium | Java, Python, JS, C#, others | Oldest and most widely installed; common in existing enterprise suites |
| pytest | Python | Test runner: finds tests, runs them, reports results. Used *with* Playwright or Selenium |

**Industry trend (2026):** industry surveys and npm data show Playwright now ahead of Selenium and Cypress in adoption, with most new projects choosing it, while Selenium remains common in existing suites. These figures mostly come from vendor blogs, so I treat them as direction, not exact numbers. Sources: [crosscheck](https://crosscheck-website.pages.dev/blogs/best-test-automation-frameworks-2026), [TestDino](https://testdino.com/blog/testing-framework-market).

## Exercises

<a id="exercise-1"></a>

### Exercise 1: Automate or manual? Applied to systems I know

I took checks from the EventLab onboarding portal (Day 2) and the ERP (Day 3) and decided for each one.

| Check | Type | Pyramid level | Automate or manual? | Why |
| --- | --- | --- | --- | --- |
| Expiry date saved as `YYYY-MM-DD` | Functional | Unit | Automate | Exact pass/fail; runs on every change |
| Non-resident skips sponsorship questions | Functional | Integration / E2E | Automate | A key branch; easy to break when the form changes |
| Saving a stage writes to Zoho | Functional | Integration | Automate | Business-critical; data loss is expensive |
| Expired link shows no candidate data | Non-functional (security) | E2E | Automate | Must never regress |
| Employee list API returns `200` and a `data` list | Functional | Integration (API) | Automate | Fast, stable, no browser needed |
| Form is easy to complete on a small phone | Non-functional (usability) | — | Manual | Needs human judgement |
| New sponsorship section, first week of build | Functional | — | Manual for now | Still changing; automation would break weekly |
| "What happens if I paste emoji into the name field?" | Exploratory | — | Manual | One-off curiosity check |

<a id="exercise-2"></a>

### Exercise 2: Comparing the JavaScript and Python tracks

**How they differ**

| Factor | JavaScript / TypeScript | Python |
| --- | --- | --- |
| Beginner-friendliness | Moderate: more symbols and brackets; async/await needed early | Easier: reads close to English, less punctuation |
| Where it's used | Web front ends and Node.js back ends | Data, scripting, automation, back ends |
| Fit with the app's code | Same language as most web front ends, so developers can review tests easily | Natural fit when the team's back end or tooling is Python |
| Playwright | Yes (its main language, newest features first) | Yes |
| Cypress | Yes | No |
| Selenium | Possible, less common | Very common, usually with pytest |
| Test runner | Playwright Test, Jest | pytest |
| API testing | Playwright `request`, Supertest | `requests` with pytest |
| Beyond UI tests | Mostly web | Also data checks and general scripting |

**Tools on each track**

| Need | JavaScript track | Python track |
| --- | --- | --- |
| Run and organise tests | Playwright Test | pytest |
| Browser / E2E tests | Playwright or Cypress | Playwright for Python (`pytest-playwright`) or Selenium |
| API tests | Playwright `request` | `requests` |
| Existing / legacy suites | Selenium WebDriver (JS) | Selenium with pytest |

**Questions that decide the track (for anyone choosing)**

| Question | If the answer is… | It points to |
| --- | --- | --- |
| What language is the app's code written in? | JavaScript / TypeScript | JavaScript, so developers can review tests |
| | Python | Python |
| Is there an existing test suite to maintain? | Yes | The language that suite is written in |
| How much coding experience does the tester have? | None or little | Python is gentler to start with |
| Is Cypress required? | Yes | JavaScript (Cypress has no Python version) |
| Will testing go beyond the UI (APIs, data checks, scripts)? | Yes | Either works; Python is especially common here |

**Takeaway:** neither language is "better" for QA automation. The project's tech stack and any existing tests usually decide it, and Playwright works in both, so the tool doesn't force the language.

<a id="exercise-3"></a>

### Exercise 3: My testing mindset

1. **Test the risks, not everything.** I focus first on what would cause the most harm to users or the business if it failed and try to reproduce in lower enviornments and create a document for the further teammates review.

2. **Empty can mean different things.** In my BQA work, I’ve learned that blank, `null`, `""`, and “not applicable” are distinct states, so each needs its own test and there results.

3. **Automate the repeatable; explore the new.** I’d automate stable, frequently repeated test cases to work more efficiently and reserve human testing for new or changing features. Once those features settle down, I’d automate their repeatable test scenarios too.

4. **Keep checks low in the pyramid.** When a quick, focused test can catch an issue, I don’t depend on a slower E2E test.

5. **A flaky test needs attention.** I fix it or remove it transparently instead of ignoring a red build.
6. **Functionality & E2E validation** In my BQA work, I will more concentrate on requriment based functionality and E2E Positive, negative and edge cases validations.

## Reflection
As im learning BA-DXC course parallel in COE, few topics are interconnected.

The idea that changed my perspective most was the test pyramid. I used to think testing meant working through the entire app as a user, but most checks should be small and quick, with just a few full end-to-end journeys at the top. As a BA, I realised that the work I did on Day 2—thinking through different branches and empty states—was already a kind of test design. Automation just lets us run those checks over and over. I’m starting with no coding experience, but exploring these automation approaches has motivated me to learn more.

## AI use

- I used Claude to research current tool adoption trends, and structure this file in the COE template.

<a id="open-questions"></a>

## Open questions

1. At which point in the training do we choose a track, and what should guide that choice?

## Changes after review

- None yet.

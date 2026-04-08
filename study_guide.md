# Study Guide: Agile, Scrum, Epics, User Stories & Jira

---

## Part 1 — Why Does Any of This Exist?

### The Problem with Building Software

Imagine you're asked to build a house. You could sit down, plan every single detail for 6 months (every nail, every wire), and then build it all at once. This is called **Waterfall** — plan everything upfront, build it in one pass.

The problem: halfway through construction, the client says "I actually want an extra bedroom." In Waterfall, that's a disaster — you already planned and built everything assuming 3 bedrooms.

**Agile** was born from this pain. Instead of planning everything upfront, you build in small increments, get feedback, and adjust. You build the foundation first, then one room, show it to the client, adjust, build the next room, and so on.

### The Agile Manifesto (4 Values)

In 2001, a group of software developers wrote 4 values that define Agile:

1. **Individuals and interactions** over processes and tools
2. **Working software** over comprehensive documentation
3. **Customer collaboration** over contract negotiation
4. **Responding to change** over following a plan

This doesn't mean documentation and plans are bad — it means when you have to choose, favor the left side.

### Agile is a Philosophy, Not a Method

Agile tells you **what to value**, but not **how to work**. That's where frameworks come in. The most popular one is **Scrum**.

---

## Part 2 — Scrum Framework

### What is Scrum?

Scrum is a framework that implements Agile principles. It defines:
- **Roles** — who does what
- **Events** — when things happen
- **Artifacts** — what you produce

### Scrum Roles

| Role | Responsibility |
|------|---------------|
| **Product Owner** | Decides WHAT to build. Owns the backlog. Represents the user/client. |
| **Scrum Master** | Ensures the team follows Scrum correctly. Removes blockers. NOT a manager. |
| **Development Team** | The people who actually build the product. Self-organizing. |

In your academic project, you're likely filling all 3 roles yourself. In a real company, these are separate people.

### Scrum Events

| Event | What Happens | When |
|-------|-------------|------|
| **Sprint Planning** | Team picks work from the backlog for the next sprint | Start of each sprint |
| **Daily Standup** | 15-min meeting: What did I do? What will I do? Any blockers? | Every day |
| **Sprint Review** | Demo the work completed to stakeholders | End of sprint |
| **Sprint Retrospective** | Team reflects: what went well, what to improve | After the review |

### What is a Sprint?

A **sprint** is a fixed time box (usually 1-2 weeks) where the team commits to completing a set of work. At the end of the sprint, you should have something **shippable** — not perfect, but functional.

Key rules:
- Sprint length is fixed (e.g., always 2 weeks)
- You don't add work mid-sprint (protect the team's focus)
- At the end, you demo what you built

### Scrum Artifacts

| Artifact | Description |
|----------|------------|
| **Product Backlog** | The full list of everything that needs to be done. Owned by the Product Owner. Constantly evolving. |
| **Sprint Backlog** | The subset of the Product Backlog selected for the current sprint. |
| **Increment** | The sum of all completed work at the end of a sprint. Must be usable. |

---

## Part 3 — The Hierarchy: Themes → Epics → User Stories → Tasks

### The Big Picture

Software is complex. You can't describe everything in one level. Scrum organizes work in a hierarchy:

```
Theme          (strategic goal)
  └── Epic     (large feature / module)
       └── User Story   (one piece of value for the user)
            └── Task     (technical work to complete the story)
```

### Themes

A **theme** is a high-level strategic goal. It groups multiple Epics under one business objective.

**Example for NeoGenesis:**
- Theme: "Complete Dinosaur Management System for the park"

You usually don't create Themes in Jira — they exist as labels or categories. They're more of a mental model.

### Epics

An **Epic** is a large body of work that can be broken down into smaller stories. It represents a significant feature or module of the system.

**Characteristics of a good Epic:**
- Too big to complete in a single sprint
- Has a clear scope and boundary
- Groups related functionality together
- Can be delivered incrementally (story by story)

**Example for NeoGenesis:**

| Epic | Why It's an Epic |
|------|-----------------|
| Infrastructure and Database | Sets up the entire data layer — multiple stories needed |
| Insertion Module | Registration + multiple validations = several stories |
| Query Module | 15 different queries = definitely more than one sprint |
| Update Module | Data updates + security code changes = several stories |
| Deletion Module | Delete by ID + delete by email + confirmation = multiple stories |
| Documentation and Deliverables | Diagrams + GitHub + Docusaurus + Jira evidence = multiple stories |

**How to identify Epics:**
1. Look at your system's modules or major features
2. Each module that requires more than 1-2 days of work is probably an Epic
3. Ask: "Can I explain this in one sentence?" → If yes, it might be an Epic. If it takes a paragraph, it might be a Theme.
4. Ask: "Can I finish this in one sprint?" → If no, it's an Epic. If yes, it might just be a Story.

### User Stories (Historias de Usuario)

A **User Story** is a short description of a feature **from the user's perspective**. It's the fundamental unit of work in Scrum.

#### The Format

```
As a [role],
I want [action],
So that [benefit].
```

Each part has a purpose:

| Part | Purpose | Common Mistake |
|------|---------|---------------|
| **As a [role]** | Who wants this? Forces you to think about the actual user. | Using "developer" or "system" as the role. The role should be someone who USES the system. |
| **I want [action]** | What do they want to DO? Must be a user-facing action. | Writing technical tasks: "I want a DbContext" — the user doesn't care about DbContext. |
| **So that [benefit]** | WHY do they want it? The business value. | Writing technical benefits: "so the database is normalized" — that's YOUR concern, not theirs. |

#### Good vs Bad User Stories

**Bad:**
```
As a developer,
I want to create a DbContext with a DbSet<Dinosaur>,
So that EF Core can generate database queries.
```
Why it's bad: The role is a developer, the action is technical, and the benefit is an implementation detail. None of this describes user value.

**Good:**
```
As an investigator,
I want the system to persist dinosaur data to a database,
So that records are available across multiple sessions without data loss.
```
Why it's good: The investigator is the real user. "Persist data" describes what they need (not how). The benefit is real — they don't want to lose their work.

**Bad:**
```
As a user,
I want to filter dinosaurs,
So that I can see filtered results.
```
Why it's bad: "User" is too vague. "Filter" is too broad — by what? The benefit is circular (I want to filter so I see filtered results).

**Good:**
```
As an investigator,
I want to filter dinosaurs by their assigned zone or sector,
So that I can monitor which specimens are located in a specific area of the park.
```
Why it's good: Specific role, specific action (filter by zone/sector), specific benefit (monitor specimens by area).

#### The INVEST Criteria

A well-written User Story follows INVEST:

| Letter | Criteria | Meaning |
|--------|---------|---------|
| **I** | Independent | Can be developed without depending on other stories |
| **N** | Negotiable | Details can be discussed and adjusted |
| **V** | Valuable | Delivers value to the user (not just technical work) |
| **E** | Estimable | The team can estimate how long it will take |
| **S** | Small | Can be completed in one sprint |
| **T** | Testable | You can write acceptance criteria to verify it's done |

#### Acceptance Criteria

Every User Story needs **Acceptance Criteria** (AC) — the specific conditions that must be true for the story to be considered "done."

**Rules for good Acceptance Criteria:**
1. **Verifiable** — someone can check yes/no if it's met
2. **Specific** — no ambiguity ("the system works properly" is NOT an AC)
3. **Independent** — each AC tests one thing
4. **User-facing when possible** — describe behavior, not implementation

**Example:**

Story: "Register a new dinosaur with required fields"

```
Acceptance Criteria:
- AC1: The system prompts for FirstName, LastName, Username, and Email.
- AC2: All four required fields must be non-empty; registration is rejected otherwise.
- AC3: The Email field must follow a valid format (contains @ and domain).
- AC4: On success, a confirmation message is displayed.
```

Notice: these describe BEHAVIOR. You can test every single one without knowing if it's built in C#, Java, or Python.

### Tasks

A **Task** is a technical step needed to complete a User Story. Tasks are NOT visible to the user — they're for the development team.

**Example:**

Story: "Register a new dinosaur with required fields"

```
Tasks:
- [ ] Create DinosaurService.Create() method
- [ ] Add input validation for required fields
- [ ] Add email format validation using regex
- [ ] Add console menu option for registration
- [ ] Write confirmation message output
```

Tasks are optional in Jira — some teams use them, some don't. For your project, they're useful to track your own progress.

---

## Part 4 — Story Points & Estimation

### What are Story Points?

Story Points measure the **effort and complexity** of a User Story — NOT the time it takes. They use the Fibonacci sequence: **1, 2, 3, 5, 8, 13, 21**.

Why Fibonacci? Because as work gets bigger, uncertainty grows exponentially. The gap between 5 and 8 is intentional — it forces you to commit: "Is this a 5 or an 8?" instead of agonizing over whether it's a 6 or a 7.

### How to Estimate

Pick a **reference story** — the simplest story in your backlog — and assign it 1 point. Then compare everything else to it.

**Example for NeoGenesis:**

| Story | Points | Reasoning |
|-------|--------|-----------|
| Create and run initial migration | 1 | Simple: one command, predictable result |
| View dinosaur detail by ID | 1 | Single LINQ query, display result |
| Register a new dinosaur with required fields | 3 | Multiple validations, user input, error handling |
| Count dinosaurs by zone and sector | 3 | GroupBy logic, multiple outputs, edge cases |
| Update dinosaur data fields | 3 | Need to handle partial updates, validation |

### Velocity

**Velocity** = total story points completed per sprint. After 2-3 sprints, you'll know your average velocity, which helps you plan future sprints more accurately.

---

## Part 5 — The Product Backlog

### What is the Backlog?

The **Product Backlog** is the prioritized list of ALL work to be done. It's a living document — items are added, removed, and reordered constantly.

### Backlog Refinement (Grooming)

Before each sprint, the team reviews and refines the backlog:
- Break large stories into smaller ones
- Clarify acceptance criteria
- Re-estimate if understanding has changed
- Re-prioritize based on new information

### Prioritization

Not all stories are equal. Common prioritization methods:

**MoSCoW Method:**
| Priority | Meaning | Example |
|----------|---------|---------|
| **Must have** | System is broken without it | Register a dinosaur, list all dinosaurs |
| **Should have** | Important but not critical | Filter by zone, count by sector |
| **Could have** | Nice to have, do if time permits | Sort alphabetically, projections report |
| **Won't have (this time)** | Out of scope for now | — |

**Value vs Effort Matrix:**
```
High Value, Low Effort  → DO FIRST  (quick wins)
High Value, High Effort  → PLAN NEXT (big rocks)
Low Value, Low Effort   → DO LATER  (fill-ins)
Low Value, High Effort  → DON'T DO  (waste)
```

---

## Part 6 — Using Jira

### Jira Concepts Map

```
Jira Project
  └── Board (Kanban or Scrum)
       └── Backlog
            └── Epics
                 └── Stories
                      └── Sub-tasks (optional)
```

### Creating a Project

1. Go to Jira → **Projects** → **Create Project**
2. Choose **Scrum** (if working in sprints) or **Kanban** (if continuous flow)
3. Choose **Team-managed** (simpler) or **Company-managed** (more features)
4. For academic projects, **Team-managed + Scrum** is the best choice

### Creating Epics in Jira

1. Go to your project's **Backlog** view
2. Click **+ Create Epic** (or the Epic panel on the left)
3. Fill in:
   - **Summary**: The Epic name (e.g., "Query Module")
   - **Description**: What this Epic covers and why
4. The Epic gets a key like `SCRUM-4`

### Creating User Stories in Jira

1. In the Backlog view, click **+ Create Issue**
2. Set **Issue Type** to **Story**
3. Fill in:
   - **Summary**: Short title in imperative form (e.g., "Register a new dinosaur with required fields")
   - **Description**: The full "As a / I want / So that" + Acceptance Criteria
   - **Parent**: Select the Epic this story belongs to (e.g., `SCRUM-5`)
   - **Story point estimate**: Your estimation (1, 2, 3, 5, 8...)
   - **Priority**: High, Medium, or Low
4. Click **Create**

### The Board

The board is where you visualize work in progress. Default columns:

```
TO DO  →  IN PROGRESS  →  DONE
```

- **TO DO**: Stories selected for the sprint but not started
- **IN PROGRESS**: Someone is actively working on it
- **DONE**: Meets all acceptance criteria, code is merged

You move cards by dragging them across columns.

### Sprints in Jira

1. **Create a Sprint**: In the Backlog view, click "Create Sprint"
2. **Fill the Sprint**: Drag stories from the backlog into the sprint
3. **Start the Sprint**: Set the start/end date (e.g., 2 weeks)
4. **During the Sprint**: Move cards on the board as you work
5. **Complete the Sprint**: Any unfinished work goes back to the backlog

### Workflow Best Practices

- Move a card to **IN PROGRESS** only when you actually start working on it
- Don't have more than 2-3 cards in progress at the same time (WIP limit)
- Move to **DONE** only when ALL acceptance criteria are met
- If a story is blocked, flag it and explain why in a comment

### CSV Import (What You Just Did)

Jira supports bulk import via CSV. The process:

1. **Prepare the CSV** with columns: Issue Type, Summary, Description, Parent, Priority, Story Points
2. **Import Epics first** — they need to exist before Stories can reference them
3. **Get the Epic keys** (e.g., SCRUM-4, SCRUM-5...) assigned by Jira after import
4. **Update the Stories CSV** with the actual Epic keys in the Parent column
5. **Import Stories** — map Parent column to the "Parent" field in Jira

Column mapping (new Jira):
| CSV Column | Jira Field |
|-----------|-----------|
| Issue Type | Issue Type |
| Summary | Summary |
| Description | Description |
| Parent | Parent |
| Story Points | Story point estimate |
| Priority | Priority |

---

## Part 7 — Common Mistakes & Anti-Patterns

### Writing Stories

| Mistake | Why It's Wrong | Fix |
|---------|---------------|-----|
| "As a developer..." | Developer is not the end user | Use the actual role: "As an investigator..." |
| "I want the database to be normalized" | Technical action, not user value | Describe what the user can DO thanks to this |
| "So that the system works" | Circular, no real benefit stated | State the specific value: "so that I can track each specimen uniquely" |
| One giant story with 10 ACs | Too big, not estimable | Split into multiple stories |
| ACs that describe implementation | "Use LINQ GroupBy" is how, not what | "The system displays count per zone" is behavior |

### Managing the Board

| Mistake | Why It's Wrong | Fix |
|---------|---------------|-----|
| Everything is IN PROGRESS | No focus, nothing getting finished | WIP limit: max 2-3 cards in progress |
| Stories stay IN PROGRESS for weeks | Story is too big | Break it into smaller stories |
| Skipping TO DO → straight to DONE | No visibility into what's happening | Always move through all columns |
| Never updating the board | Board becomes useless | Update at least once per day |

### Estimation

| Mistake | Why It's Wrong | Fix |
|---------|---------------|-----|
| Estimating in hours | Hours vary by person and day | Use relative story points |
| All stories are 1 point | You're not really estimating | Compare stories to each other |
| All stories are 13 points | Stories are too big | Break them down until they're 1-5 points |

---

## Part 8 — Glossary

| Term | Definition |
|------|-----------|
| **Agile** | A philosophy for software development that values adaptability, collaboration, and incremental delivery |
| **Scrum** | A framework that implements Agile through sprints, roles, and ceremonies |
| **Sprint** | A fixed time period (1-4 weeks) where a team commits to completing a set of stories |
| **Product Backlog** | The complete prioritized list of all work to be done on the product |
| **Sprint Backlog** | The subset of stories selected for the current sprint |
| **Epic** | A large feature or module that contains multiple related user stories |
| **User Story (HU)** | A description of a feature from the user's perspective, using "As a / I want / So that" format |
| **Acceptance Criteria** | Specific, testable conditions that define when a story is complete |
| **Story Points** | A relative measure of effort and complexity, using the Fibonacci sequence |
| **Velocity** | The average number of story points a team completes per sprint |
| **WIP Limit** | Maximum number of items allowed in a workflow column at once |
| **Increment** | The usable product output at the end of a sprint |
| **Definition of Done (DoD)** | A shared checklist of criteria that ALL stories must meet to be considered complete |
| **Refinement / Grooming** | The process of reviewing, clarifying, and re-estimating backlog items |
| **MoSCoW** | Prioritization method: Must have, Should have, Could have, Won't have |
| **INVEST** | Quality criteria for stories: Independent, Negotiable, Valuable, Estimable, Small, Testable |
| **Kanban** | A continuous-flow alternative to Scrum — no sprints, work flows through columns with WIP limits |

---

## Part 9 — Self-Check Questions

Use these to test your understanding. If you can answer all of them clearly, you've got it.

### Agile & Scrum
1. What's the difference between Agile and Scrum?
2. What are the 3 Scrum roles and what does each one do?
3. What happens during Sprint Planning? During the Retrospective?
4. Why is the sprint length fixed? What happens if you don't finish all stories?

### Epics
5. How do you decide what should be an Epic vs just a large Story?
6. Can an Epic span multiple sprints? Should it?
7. For the NeoGenesis project, why is "Query Module" its own Epic instead of being part of "Infrastructure"?

### User Stories
8. Why do we write stories from the USER's perspective instead of the developer's?
9. What's wrong with this story: "As a developer, I want to implement LINQ queries, so that the system can filter data"?
10. Rewrite the bad story from question 9 as a proper User Story.
11. What makes a good Acceptance Criterion? Give an example of a bad one and fix it.

### Estimation
12. Why do we use Fibonacci numbers instead of just 1-10?
13. If a story has 8 story points, what does that tell you about it?
14. What is velocity and why is it useful?

### Jira
15. What's the difference between the Backlog view and the Board view?
16. When should you move a card to IN PROGRESS? When should you move it to DONE?
17. Why import Epics before Stories in a CSV import?

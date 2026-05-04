# AgentHub Admin Panel Prototype Specification

## 1. Short Product Description

AgentHub is a SaaS platform where companies can rent AI agents for business tasks. These AI agents can be configured with skills such as browsing the web, reading documents, managing calendars, updating CRM records, reviewing contracts, and handling customer support tasks.

The admin user is an internal AgentHub operator. This operator uses the admin panel to manage users, agents, skills, contracts, platform activity, and system errors.

The purpose of this project is to build a fully designed frontend HTML prototype of the AgentHub admin panel. The prototype will use hardcoded data and will not connect to a backend. The specification acts as the contract for the codebase before any HTML is built.

---

## 2. Tech Stack and Constraints

### Required Tech Stack

- HTML
- Tailwind CSS through CDN only
- Vanilla JavaScript only

### Required File Structure

- `SPECS.md`
- `index.html`

### Constraints

- No React
- No Vue
- No Angular
- No jQuery
- No backend code
- No API calls
- No build tools
- No custom CSS files
- No inline `style` attributes
- All styling must use Tailwind utility classes
- All data must be hardcoded
- Tailwind must be loaded through CDN only
- All interactivity must use vanilla JavaScript only
- The final prototype must be built in one `index.html` file
- `SPECS.md` must be created and committed before `index.html`

---

## 3. Admin Panel Structure

The AgentHub admin panel must include six main sections:

1. Dashboard
2. User Management
3. Agent Management
4. Skills
5. Agent Contracts
6. Error Log

All six sections must be accessible from a persistent sidebar navigation.

The sidebar must show an active state indicator for the current section.

A top bar must include a dark/light mode toggle.

The dark/light mode toggle must switch the full interface between light mode and dark mode using Tailwind's `dark:` utilities.

The selected mode must remain active while navigating between sections.

---

## 4. Shared JSON Data Model Requirement

The prototype must use one hardcoded JSON-style JavaScript object named `agentHubData`.

This object must be the single source of truth for all visible admin panel data.

The required structure is:

```js
const agentHubData = {
  dashboardMetrics: [],
  users: [],
  agents: [],
  skills: [],
  contracts: [],
  errors: []
};
```

This object must be placed inside the `<script>` section of `index.html`.

All visible content in the Dashboard, User Management, Agent Management, Skills, Agent Contracts, and Error Log sections must render from `agentHubData`.

No table rows, cards, contract details, error details, modal content, or agent records should be manually hardcoded outside of the shared data object.

The same agent names must be reused across:

- Agent Management
- Agent Contracts
- Error Log

Required shared agent names:

- SupportBot Pro
- CalendarPilot
- DocuMind
- SalesAssist AI

`CalendarPilot` must use the status `Inactive`, not `Training`.

---

## 5. Data Types / Data Schema

The project must clearly organize data using objects, arrays, strings, and numbers.

### dashboardMetrics

Each dashboard metric must be an object with:

- `icon`: string
- `label`: string
- `value`: string
- `badge`: string
- `color`: string

Example:

```js
{
  icon: "💰",
  label: "Monthly Revenue",
  value: "$48,920",
  badge: "Revenue",
  color: "green"
}
```

### users

Each user must be an object with:

- `name`: string
- `email`: string
- `plan`: string
- `status`: string
- `color`: string
- `company`: string
- `joined`: string
- `rentedAgents`: number

Example:

```js
{
  name: "Maya Johnson",
  email: "maya@northstar.com",
  plan: "Enterprise",
  status: "Active",
  color: "green",
  company: "Northstar Logistics",
  joined: "Jan 12, 2026",
  rentedAgents: 12
}
```

### agents

Each agent must be an object with:

- `name`: string
- `owner`: string
- `status`: string
- `color`: string
- `skills`: array of strings
- `prompt`: string

Example:

```js
{
  name: "CalendarPilot",
  owner: "BrightCRM",
  status: "Inactive",
  color: "gray",
  skills: ["Calendar Management", "Email Drafting", "Reminder Creation"],
  prompt: "You are CalendarPilot. Manage scheduling requests, find open time blocks, and create clear meeting summaries."
}
```

### skills

Each skill must be an object with:

- `name`: string
- `description`: string
- `enabledCount`: number
- `example`: string

Example:

```js
{
  name: "Document Reading",
  description: "Reads documents and extracts useful details.",
  enabledCount: 24,
  example: "Summarize contracts."
}
```

### contracts

Each contract must be an object with:

- `client`: string
- `agent`: string
- `skills`: array of strings
- `start`: string
- `end`: string
- `amount`: string
- `itemized`: array of objects

Each object inside `itemized` must include:

- `name`: string
- `price`: string

Example:

```js
{
  client: "BrightCRM",
  agent: "CalendarPilot",
  skills: ["Calendar Management", "Email Drafting"],
  start: "2026-02-01",
  end: "2026-08-01",
  amount: "$6,800",
  itemized: [
    {
      name: "Calendar Management",
      price: "$3,800"
    },
    {
      name: "Email Drafting",
      price: "$3,000"
    }
  ]
}
```

### errors

Each error must be an object with:

- `timestamp`: string
- `agent`: string
- `type`: string
- `color`: string
- `description`: string
- `trace`: string

Example:

```js
{
  timestamp: "2026-04-28 10:05 AM",
  agent: "CalendarPilot",
  type: "Permission Error",
  color: "yellow",
  description: "Calendar permission token expired.",
  trace: "Calendar access token expired before meeting sync completed."
}
```

### Data Type Rules

- Text values must use strings.
- Count values must use numbers.
- Skill lists must use arrays of strings.
- Contract itemized prices must use arrays of objects.
- All visible data must render from `agentHubData`.
- All sections must feel connected through the shared data model.

---

## 6. Section Specifications

## Section 1: Dashboard

1. A metric card grid component must display four cards in a responsive layout.

2. The four metric cards must show:
   - Total revenue generated this month
   - Total discount and coupon losses
   - Number of active agents across all clients
   - Number of agents currently flagged as failing

3. Each metric card must include:
   - Icon
   - Label
   - Hardcoded value
   - Badge or accent indicator
   - Distinct color styling

4. The metric cards must render from `agentHubData.dashboardMetrics`.

5. Below the metric cards, a full-width weekly activity chart placeholder must appear.

6. The weekly activity placeholder must use:
   - Dashed border
   - Rounded corners
   - Centered text
   - Clear label such as `Weekly Activity Chart Placeholder`

7. The Dashboard must be the default section shown when the admin panel first loads.

---

## Section 2: User Management

1. A user table component must display at least five hardcoded users.

2. Each user row must show:
   - Name
   - Email
   - Plan
   - Status badge

3. User rows must render from `agentHubData.users`.

4. Each user row must include a `⋮` action dropdown.

5. The user action dropdown must include:
   - View detail
   - Delete

6. Clicking `View detail` must open a modal showing the full user record.

7. The full user record must include:
   - Name
   - Email
   - Plan
   - Status
   - Company
   - Joined date
   - Number of rented agents

8. The modal must close when clicking the close button.

9. The modal must close when clicking the backdrop outside the modal content.

10. The user dropdown must close when clicking outside the dropdown menu area.

---

## Section 3: Agent Management

1. An agent listing component must display at least four hardcoded agents.

2. Each agent must show:
   - Agent name
   - Owner/client
   - Current status badge
   - Collapsed skill list

3. Agent records must render from `agentHubData.agents`.

4. Agent statuses must use assignment-approved status values:
   - Active
   - Inactive
   - Failing

5. `CalendarPilot` must show the status `Inactive`.

6. Agent skills must be hidden by default.

7. Each agent must have an expand control that reveals the full skill list.

8. Clicking the expand control again must collapse the skill list.

9. The expand/collapse behavior must use a visible smooth transition.

10. The smooth transition should use Tailwind classes and vanilla JavaScript class toggling, such as:
    - `max-h-0`
    - `max-h-40`
    - `opacity-0`
    - `opacity-100`
    - `overflow-hidden`
    - `transition-all`
    - `duration-300`
    - `ease-in-out`

11. Each agent must include a `⋮` action dropdown.

12. The agent dropdown must include:
    - Configure
    - Delete

13. Clicking `Configure` must open a modal.

14. The configure modal must show:
    - Agent name
    - Owner
    - Status
    - Agent system prompt inside an editable `<textarea>`

15. Agent names must match the names reused in Agent Contracts and Error Log.

---

## Section 4: Skills

1. A skill catalog component must display at least four hardcoded skills.

2. Each skill must show:
   - Skill name
   - Short description
   - Number of agents that have it enabled

3. Skill records must render from `agentHubData.skills`.

4. The Skills section must include a brief explanation of what a skill means in AgentHub.

5. A skill means a capability that can be attached to an AI agent, such as:
   - Web browsing
   - Document reading
   - Calendar management
   - CRM updating

6. Each skill must include a `⋮` action dropdown.

7. The skill dropdown must include:
   - View detail
   - Delete

8. Clicking `View detail` must open a modal showing:
   - Skill name
   - Description
   - Enabled agent count
   - Example use case

9. Skill cards must use consistent spacing, borders, badges, rounded corners, shadows, and dark mode styles.

---

## Section 5: Agent Contracts

1. A contracts table component must display at least four hardcoded contracts.

2. Each contract row must show:
   - Client
   - Agent
   - Contracted skills
   - Start date
   - End date
   - Amount paid

3. Contract rows must render from `agentHubData.contracts`.

4. Each contract row must include a `⋮` action dropdown.

5. The contract dropdown must include a `View detail` option.

6. Clicking `View detail` must open a modal with the full contract breakdown.

7. The contract detail modal must include:
   - Client name
   - Agent name
   - Contract start date
   - Contract end date
   - Itemized skills
   - Individual skill prices
   - Full contract total

8. Contract data must reuse agent names from `agentHubData.agents`.

9. The contracts table must use semantic `<table>` markup.

10. The contracts table must be readable on desktop and tablet screen sizes.

---

## Section 6: Error Log

1. An error log list or table component must display at least six hardcoded error entries.

2. Each error entry must show:
   - Timestamp
   - Agent name
   - Color-coded error type badge
   - Short description

3. Error records must render from `agentHubData.errors`.

4. Error type badges must use different colors based on error type or severity.

5. Example error types include:
   - API Failure
   - Skill Timeout
   - Permission Error
   - Billing Sync Error
   - Prompt Error

6. Each error entry must include a `⋮` action dropdown.

7. The error dropdown must include:
   - View detail
   - Mark as resolved

8. Clicking `View detail` must open a modal showing the full error trace.

9. The full error trace modal must include:
   - Timestamp
   - Agent name
   - Error type
   - Short description
   - Detailed trace text

10. Error entries must reuse agent names from `agentHubData.agents`.

---

## 7. Component Inventory

The prototype must use reusable UI patterns across sections.

### Sidebar

- Persistent navigation component.
- Links to all six sections.
- Shows active state for current section.
- Remains visible on desktop and tablet layouts.

### Top Bar

- Header component at the top of the main content area.
- Includes current section title.
- Includes dark/light mode toggle.

### Metric Card

- Used in the Dashboard section.
- Displays icon, label, value, badge, and accent color.
- Supports light and dark mode styles.

### Action Dropdown

- Used in User Management, Agent Management, Skills, Agent Contracts, and Error Log.
- Opens when the `⋮` button is clicked.
- Closes when clicking outside the dropdown menu.

### Modal

- Used for:
  - User detail
  - Agent configuration
  - Skill detail
  - Contract detail
  - Error detail

- Opens from dropdown actions.
- Closes from close button.
- Closes from backdrop click.

### Badge

- Used for:
  - User statuses
  - Agent statuses
  - Error types
  - Metric labels

- Uses different Tailwind color utilities based on type.

### Collapsible Skill List

- Used in Agent Management.
- Hidden by default.
- Expands and collapses on click.
- Uses a smooth transition.

### Dark Mode Toggle

- Located in the top bar.
- Toggles the full panel between light mode and dark mode.
- Uses Tailwind's `dark:` utilities.
- Keeps the selected mode active while navigating sections.

---

## 8. Global Interaction Rules

1. The dark/light mode toggle must switch the entire admin panel between light mode and dark mode.

2. Dark mode must use Tailwind's `dark:` utility classes.

3. The selected mode must stay active while navigating between sections.

4. Sidebar navigation must update the active state when the admin changes sections.

5. All action dropdowns must close when clicking outside the menu area.

6. All modals must close when clicking the close button.

7. All modals must close when clicking the backdrop outside the modal content.

8. Collapsible skill lists in Agent Management must start closed.

9. Collapsible skill lists must expand and collapse when the admin clicks the expand control.

10. All visible section data must render from `agentHubData`.

11. The prototype must not use real backend data or API calls.

---

## 9. Hardcoded Data Consistency Rules

1. The same agent names must appear across Agent Management, Agent Contracts, and Error Log.

2. Required shared agent names:
   - SupportBot Pro
   - CalendarPilot
   - DocuMind
   - SalesAssist AI

3. `CalendarPilot` must use the status `Inactive`.

4. Agent Contracts must reference agents that exist in the Agent Management section.

5. Error Log entries must reference agents that exist in the Agent Management section.

6. Skills used in contracts and agents should match skills listed in the Skills section.

7. The prototype should feel like one connected platform, not disconnected static sections.

---

## 10. Semantic HTML Requirements

The prototype must use semantic HTML where appropriate, including:

- `<nav>` for the sidebar navigation
- `<header>` for the top bar
- `<main>` for the main content area
- `<section>` for each admin panel section
- `<table>` for user and contract data
- `<button>` for interactive controls
- Modal-style semantic structure for modal content

---

## 11. Acceptance Criteria

1. `SPECS.md` is created at the root of the repository before any HTML work begins.

2. `SPECS.md` is committed before `index.html` is created or committed.

3. The prototype is built as one `index.html` file.

4. The prototype uses HTML, Tailwind CSS through CDN, and vanilla JavaScript only.

5. The prototype does not use React, Vue, Angular, jQuery, backend code, API calls, build tools, custom CSS files, or inline `style` attributes.

6. All styling is done with Tailwind utility classes.

7. All data is hardcoded.

8. A single shared JSON-style data object named `agentHubData` exists in `index.html`.

9. `agentHubData` includes:
   - `dashboardMetrics`
   - `users`
   - `agents`
   - `skills`
   - `contracts`
   - `errors`

10. Dashboard data renders from `agentHubData.dashboardMetrics`.

11. User Management data renders from `agentHubData.users`.

12. Agent Management data renders from `agentHubData.agents`.

13. Skills data renders from `agentHubData.skills`.

14. Agent Contracts data renders from `agentHubData.contracts`.

15. Error Log data renders from `agentHubData.errors`.

16. No visible row, card, modal, contract, error, or agent content is manually hardcoded outside `agentHubData`.

17. The admin panel includes all six required sections:
   - Dashboard
   - User Management
   - Agent Management
   - Skills
   - Agent Contracts
   - Error Log

18. All six sections are accessible from the persistent sidebar navigation.

19. The sidebar shows an active state indicator for the current section.

20. The top bar includes a working dark/light mode toggle.

21. The dark/light mode toggle switches the entire panel between light mode and dark mode using Tailwind's `dark:` utilities.

22. The selected light or dark mode stays active while navigating between sections.

23. The Dashboard includes four metric cards with icons, labels, hardcoded values, and distinct accent colors.

24. The Dashboard includes a full-width weekly activity chart placeholder with a dashed border and centered label.

25. The User Management section includes a table with at least five hardcoded users.

26. Each user row includes name, email, plan, status badge, and a working `⋮` action dropdown.

27. The User Management dropdown includes `View detail` and `Delete`.

28. Clicking `View detail` in User Management opens a modal with the full user record.

29. The Agent Management section includes at least four hardcoded agents.

30. Each agent shows name, owner, status badge, and collapsed skill list.

31. Agent statuses include only assignment-approved values such as Active, Inactive, and Failing.

32. `CalendarPilot` displays as `Inactive`.

33. Agent skill lists are hidden by default.

34. Clicking the expand control reveals the agent's skills with a visible smooth transition.

35. Clicking the expand control again collapses the skill list.

36. Each agent includes a working `⋮` action dropdown with `Configure` and `Delete`.

37. Clicking `Configure` opens a modal with the agent system prompt in an editable `<textarea>`.

38. The Skills section includes at least four hardcoded skills.

39. Each skill shows name, description, and number of agents that have it enabled.

40. The Skills section includes an explanation of what a skill means in the AgentHub context.

41. Each skill includes a working `⋮` action dropdown with `View detail` and `Delete`.

42. The Agent Contracts section includes a table with at least four hardcoded contracts.

43. Each contract row shows client, agent, contracted skills, start date, end date, and amount paid.

44. Each contract row includes a working `⋮` action dropdown.

45. Clicking `View detail` in Agent Contracts opens a modal with the full contract breakdown.

46. The contract detail modal includes itemized skills, individual prices, and full contract total.

47. The Error Log section includes at least six hardcoded error entries.

48. Each error entry shows timestamp, agent name, color-coded error type badge, and short description.

49. Each error entry includes a working `⋮` action dropdown with `View detail` and `Mark as resolved`.

50. Clicking `View detail` in Error Log opens a modal with the full error trace.

51. All action dropdowns close when clicking outside their menu area.

52. All modals close when clicking the close button.

53. All modals close when clicking the backdrop outside the modal content.

54. The same agent names appear in Agent Management, Agent Contracts, and Error Log.

55. The HTML uses semantic tags correctly, including `section`, `table`, `nav`, `header`, and `main`.

56. The layout is usable on desktop and tablet viewports.

57. The repository is pushed to GitHub after both `SPECS.md` and `index.html` are committed.

58. The repository is public for submission.

---

## 12. Build Plan After Specification Commit

After `SPECS.md` is committed, the prototype will be built in one file:

- `index.html`

The `index.html` file will include:

- Tailwind CDN
- Sidebar navigation
- Top bar with dark/light mode toggle
- Six admin panel sections
- One shared hardcoded JSON-style data object named `agentHubData`
- Render functions for all six sections
- Action dropdown logic
- Modal logic
- Collapsible skill list logic
- Dark mode logic using Tailwind `dark:` utilities
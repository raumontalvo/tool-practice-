# AgentHub Admin Panel Prototype Specification

## 1. Product Description

AgentHub is a SaaS platform where companies rent AI agents for operational work such as web browsing, document reading, calendar management, file summarization, and business task automation.

This admin panel is for internal AgentHub operations staff. The admin uses it to monitor platform health, manage customers, manage agents and skills, review contracts, and inspect failures.

The goal of this prototype is a complete, interactive frontend demo with hardcoded data only.

## 2. Tech Stack And Constraints

### Required stack
- HTML
- Tailwind CSS via CDN only
- Vanilla JavaScript only

### Hard constraints
- No React, Vue, Angular, jQuery, or any UI framework
- No backend, API calls, database, or server integration
- No build tools
- No custom CSS files
- No inline style attributes
- Use semantic HTML elements: `nav`, `header`, `main`, `section`, `table`
- All data is hardcoded and reused consistently across sections

## 3. Information Architecture

The app uses a persistent sidebar with these six sections:
1. Dashboard
2. User Management
3. Agent Management
4. Skills
5. Agent Contracts
6. Error Log

Global behavior:
- Sidebar is always visible on tablet and desktop layouts
- Sidebar active state updates when switching sections
- Top bar includes a dark/light mode toggle
- Dark mode is implemented with Tailwind `dark:` utilities
- Chosen theme remains active while switching sections

## 4. Shared Data Model And Consistency

All UI content is rendered from one hardcoded JavaScript source of truth object.

Required shared agent names used across Agent Management, Agent Contracts, and Error Log:
- Atlas Support Agent
- Nova Sales Agent
- Ledger Finance Agent
- Scout Research Agent

Required model shape:

```js
const appData = {
  metrics: [],
  users: [],
  agents: [],
  skills: [],
  contracts: [],
  errors: []
};
```

Rules:
- Do not hardcode duplicate records in different sections
- Contracts and errors must reference the same agent names from `agents`
- Dropdown, modal, and detail content reads from the same object data

## 5. Section Specifications

### 5.1 Dashboard
1. Show four metric cards: Total revenue, Discount losses, Active agents, Failing agents.
2. Each card includes icon, label, and hardcoded value.
3. Show one full-width weekly activity chart placeholder below metrics.
4. Dashboard must remain readable in both light and dark themes.

### 5.2 User Management
1. Render a table with at least 5 hardcoded users.
2. Each row shows Name, Email, Plan, Status badge.
3. Each row has a `⋮` action button with dropdown options: View detail, Delete.
4. View detail opens a modal containing the complete selected user record.

### 5.3 Agent Management
1. Render at least 4 agents using the required shared names.
2. Each agent row/card shows Name, Owner, Status badge, and a collapsed skill list.
3. Skill list is collapsed by default and expands/collapses with smooth transition.
4. Each agent has `⋮` dropdown options: Configure, Delete.
5. Configure opens a modal with an editable textarea seeded with the agent system prompt.

### 5.4 Skills
1. Include a short explanatory block describing what a skill means in AgentHub.
2. Render at least 4 skill entries with Name, Description, and number of agents using it.
3. Each skill has `⋮` dropdown options: View detail, Delete.
4. View detail can reuse the global modal component.

### 5.5 Agent Contracts
1. Render a table with at least 4 contracts.
2. Each row shows Client, Rented agent, Contracted skills, Start date, End date, Total amount paid.
3. Each row has a `⋮` dropdown with View detail.
4. View detail opens a modal with full contract breakdown and itemized skill prices.

### 5.6 Error Log
1. Render at least 6 hardcoded error entries.
2. Each entry shows Timestamp, Agent name, Error type, and short description.
3. Error type/severity uses color-coded badges.
4. Each entry has `⋮` dropdown options: View detail, Mark as resolved.
5. View detail opens a modal with full error trace content.

## 6. Component Inventory

Required reusable components:
- Sidebar: persistent section navigation with active state
- Metric card: icon + label + value display
- Action dropdown: per-row contextual actions opened by `⋮`
- Modal: shared detail/configuration container with close controls
- Badge: status and severity visual labels
- Collapsible skill list: default collapsed, smooth expand/collapse behavior
- Dark mode toggle: top bar control that switches global theme

## 7. Interaction Specifications

1. Every visible `⋮` button opens its own dropdown.
2. Clicking outside any open dropdown closes it.
3. Dropdown items are clickable and trigger the correct action.
4. Modals open from View detail and Configure actions.
5. Modals close via dedicated close button.
6. Modals close when clicking the backdrop.
7. Agent skill lists are collapsed on initial render.
8. Expanding/collapsing skill lists uses visible smooth transition.
9. Dark/light mode toggle updates the entire panel theme.
10. Theme state remains active while changing sections.

## 8. Numbered Acceptance Criteria

1. The sidebar exposes all six sections and each section is reachable without page reload.
2. Active navigation state updates correctly when a section is selected.
3. Dashboard shows exactly four required metric cards and one full-width weekly chart placeholder.
4. User Management has at least 5 users with Name, Email, Plan, Status badge, and `⋮` actions.
5. Agent Management has at least 4 agents with collapsed-by-default skill lists.
6. Skills section has at least 4 skills and includes a clear skill definition block.
7. Agent Contracts has at least 4 contracts with all required columns and paid totals.
8. Error Log has at least 6 entries with color-coded severity/type badges.
9. Dropdown criterion: any row `⋮` opens an action menu, menu items are clickable, and outside click closes the menu.
10. Modal criterion: View detail/Configure opens modal; modal closes with close button and backdrop click.
11. Collapsible criterion: agent skills start collapsed and expand/collapse smoothly on toggle.
12. Dark mode criterion: top bar toggle switches full panel using Tailwind `dark:` classes and preserves state across section switches.
13. No inline style attributes and no external/custom CSS files are used.
14. Tailwind is loaded through CDN only.
15. JavaScript is vanilla only and all data is hardcoded.
16. Agent names are consistent across Agent Management, Agent Contracts, and Error Log.
17. Tablet and desktop layouts are usable with persistent navigation and readable tables/cards.
18. Every clickable-looking UI element either performs an interaction, provides state feedback, or is clearly marked as a non-interactive demo placeholder.

# Mona's Project Pulse Agent Team

The Project Pulse dashboard is built by a coordinated team of four custom
agents stored in `.github/agents/`. Each agent has a distinct responsibility,
model assignment, and file scope so planning, design, implementation, and
validation remain clear.

## Team overview

| Agent | Assigned model | Definition | Responsibility |
| --- | --- | --- | --- |
| **Orchestrator** | Opus 4.7 | `.github/agents/orchestrator.agent.md` | Coordinates the team, breaks the request into phases, delegates work, manages dependencies and file ownership, verifies the integrated result, and reports the final outcome. |
| **Planner** | Opus 4.7 | `.github/agents/planner.agent.md` | Researches the repository and relevant documentation, identifies requirements, risks, edge cases, dependencies, validation expectations, and produces an ordered implementation plan. |
| **Coder** | GPT-5.5 | `.github/agents/coder.agent.md` | Implements the assigned code within scope, follows repository patterns, keeps behavior explicit and testable, creates required runnable-app support files when assigned, and validates the change. |
| **Designer** | Gemini 3.1 Pro | `.github/agents/designer.agent.md` | Defines the dashboard's usability, accessibility, information hierarchy, interaction flow, responsive behavior, visual clarity, and Project Pulse styling direction. |

## Responsibilities for Project Pulse

### Orchestrator

The Orchestrator owns coordination rather than implementation. It first asks
the Planner for a repository-informed plan, then turns that plan into phases
with explicit file assignments. It delegates design and coding work only when
their scopes and dependencies are clear, keeps overlapping edits separated,
integrates the results, and validates that the final dashboard works as a
coherent whole.

### Planner

The Planner researches the Project Pulse brief, repository conventions,
dependencies, edge cases, error states, and implicit requirements. Its output
should identify the work for `app/index.html`, `app/styles.css`,
`app/project-data.json`, `.vscode/launch.json`, and related documentation,
including which work can run in parallel and what must happen sequentially.
The Planner creates plans only; it does not write implementation code.

### Designer

The Designer guides the experience for Mona's contributors. The dashboard
should make active projects, owners, status, recent activity, priority or risk,
and contributor-friendly summaries easy to scan. The Designer's Project Pulse
expectations include visible project cards, status badges, clear priority
treatment, readable spacing, responsive behavior, accessibility, and a polished
visual hierarchy. Deterministic hooks such as `.dashboard` and
`.project-card` support the handoff to implementation.

### Coder

The Coder implements the static dashboard within the file scope assigned by
the Orchestrator. The implementation connects `app/index.html` to
`app/styles.css` and `app/project-data.json`, renders the project information,
and creates `.vscode/launch.json` when assigned. For Project Pulse, the launch
configuration serves from `app/`, opens `index.html`, and uses the deterministic
**Run Project Pulse Dashboard** configuration. The Coder also validates the
result without changing design-only files unless explicitly assigned.

## How the team works together

1. **Plan first:** The Orchestrator gives the Planner the Project Pulse brief
   and asks for an implementation plan with file ownership, dependencies,
   risks, and validation criteria.
2. **Shape the experience:** The Orchestrator assigns the design scope to the
   Designer. The Designer establishes the information hierarchy, accessible
   interactions, responsive layout, visual treatment, and CSS hooks before or
   alongside implementation when there is no file conflict.
3. **Implement the dashboard:** The Orchestrator assigns the implementation
   scope to the Coder. The Coder builds the HTML, CSS, JSON data, and launch
   configuration according to the plan and design direction.
4. **Coordinate dependencies:** Planning precedes implementation. Design
   decisions can run in parallel with non-overlapping data or setup work, but
   implementation that depends on those decisions runs afterward. The
   Orchestrator keeps shared files from being edited concurrently and resolves
   integration issues.
5. **Verify and hand off:** The Orchestrator reviews the documentation,
   dashboard files, data shape, styling hooks, and launch configuration,
   confirms the Project Pulse UI opens rather than a directory listing, and
   reports the final result and any remaining limitations.

This workflow separates strategy, experience design, implementation, and
integration so the team can build Mona's dashboard without treating the task
as one undifferentiated prompt.

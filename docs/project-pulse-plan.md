# Project Pulse implementation plan

## Goal

Build a small, contributor-friendly Project Pulse dashboard that surfaces project health at a glance. The app should help teammates quickly scan active projects, owners, status, recent activity, priority, and a concise summary without needing a backend or complex interactions. The final result must be a static dashboard wired to a JSON data source and previewable through a VS Code launch configuration.

## Scope and expected app files

- `app/index.html`: dashboard structure and content rendering
- `app/styles.css`: visual design, spacing, status treatment, and responsiveness
- `app/project-data.json`: project metadata for the dashboard (`projects`, `owner`, `status`, `recentActivity`, `priority`)
- `.vscode/launch.json`: launch configuration to open `app/index.html` from the `app/` directory instead of a server directory listing

## File assignment table

| File | Primary owner | Purpose | Dependencies |
| --- | --- | --- | --- |
| `app/index.html` | Designer + Coder | Create the dashboard shell, project cards, status badges, summary and headings, and reference `styles.css` and `project-data.json` | Depends on the agreed visual direction and the JSON schema; must align with CSS classes and data keys |
| `app/styles.css` | Designer | Define layout, card styling, spacing, typography, color cues, shadows, and responsive layout | Depends on the HTML structure and chosen content hierarchy; informs card and badge classes used in HTML |
| `app/project-data.json` | Coder | Provide the `projects` array and field values used by the dashboard | Must match the keys expected by the HTML/JS rendering logic; should be valid JSON and stable before UI validation |
| `.vscode/launch.json` | Coder | Add the `Run Project Pulse Dashboard` launch configuration that serves the `app/` folder and opens `index.html` | Depends on the app being ready to preview; should be validated after the HTML/CSS/data files exist |
| `docs/project-pulse-plan.md` | Planner | Capture the implementation strategy, ownership, dependencies, validation, and open questions | Acts as the source of truth for the Orchestrator and team handoff |

## Roles and responsibilities

### Orchestrator
- Coordinates the work across Planner, Designer, and Coder.
- Breaks the plan into ordered phases based on dependencies and file ownership.
- Confirms that the dashboard and preview flow are aligned before handoff.

### Planner
- Researches the Project Pulse brief and repository expectations.
- Produces the implementation phases, dependency map, and validation checklist.
- Captures unknowns and open questions early so the implementation stays grounded.

### Designer
- Defines the project card hierarchy, visual treatment, status badges, and readability.
- Owns the look and feel for `app/styles.css` and the content structure in `app/index.html`.
- Ensures the first-view dashboard reads clearly, feels polished, and supports accessibility through strong contrast, spacing, and consistent labels.

### Coder
- Implements the static app files and data contract.
- Owns JSON validity, preview configuration, and the wiring between content and presentation.
- Validates that `app/index.html` references the CSS and JSON files correctly and that the launch configuration opens the dashboard rather than the directory listing.

## Implementation phases

### Phase 1: Confirm requirements and data contract
- Confirm the dashboard objective from the Project Pulse brief.
- Define the required fields: `name`, `owner`, `status`, `recentActivity`, `priority`, and the top-level `projects` array.
- Agree on the card structure and content hierarchy before building markup.

### Phase 2: Design the dashboard layout
- Decide on the page-level layout, card spacing, header treatment, and visual priority cues.
- Create the CSS naming conventions and status badge patterns.
- Ensure the design is clear enough for contributor scanning without needing complex UI logic.

### Phase 3: Implement HTML and data
- Build `app/index.html` around the agreed dashboard structure and content.
- Add references to `styles.css` and `project-data.json`.
- Populate `app/project-data.json` with realistic project entries and consistent statuses.

### Phase 4: Preview configuration
- Add `.vscode/launch.json` with a launch name such as `Run Project Pulse Dashboard`.
- Configure the workspace to serve `app/` and open `index.html` directly.
- Verify the preview loads the dashboard UI rather than a folder listing.

### Phase 5: Validation and handoff
- Validate JSON parseability, file wiring, and render readiness.
- Confirm that the page displays project cards with status, activity, and priority.
- Check that the app is a polished static dashboard suitable for a brief live preview.

## Dependencies and parallel work decisions

### Dependencies
- The HTML structure should be defined before the CSS styling is finalized, because CSS classes and hierarchy must match the markup.
- The data schema should be fixed before the final layout is validated, since project cards rely on stable keys such as `owner`, `status`, `recentActivity`, and `priority`.
- The launch configuration should be created after the dashboard files exist, since preview validation depends on real file paths and a working `index.html` entry point.
- The Planner's documentation and the Orchestrator's phasing must precede implementation to reduce rework and keep ownership clear.

### Parallel work decisions
- Designer and Coder can work in parallel once the dashboard goal and data contract are agreed upon: the Designer can shape the CSS and visual hierarchy while the Coder prepares the JSON and baseline HTML structure.
- The Planner can prepare documentation and dependency notes concurrently with the early design and implementation kickoff, as long as the work remains aligned to the brief.
- The final launch preview should be validated only after the content and styling files are sufficiently complete, so it acts as a serial final check rather than a parallel task.

## Edge cases and risks

- Missing or inconsistent data keys in `app/project-data.json` can break rendering or make status badges ambiguous.
- A CSS class mismatch between HTML and stylesheet can cause cards to lose expected spacing, colors, or hierarchy.
- Launch misconfiguration may open the directory listing instead of `index.html`, which would fail the preview requirement.
- Empty project lists or statuses with unusual values should still produce readable output rather than break the layout.
- Long owner names, activity strings, or project names should not force card overflow or unreadable spacing.
- Status names may vary; the design should use a consistent treatment for active, at risk, blocked, or completed states without hard-coding impossible assumptions.

## Validation expectations

The implementation should be considered complete when all of the following are true:

- `docs/project-pulse-plan.md` exists and captures the Project Pulse goal, file assignments, responsibilities, dependencies, and validation steps.
- `app/index.html` exists and includes the Project Pulse dashboard title, references to `styles.css` and `project-data.json`, and project card content.
- `app/styles.css` includes a dashboard layout and project-card styling patterns with readable spacing, borders, shadows, and responsive structure.
- `app/project-data.json` is valid JSON and includes a top-level `projects` array with `name`, `owner`, `status`, `recentActivity`, and `priority` values.
- `.vscode/launch.json` exists and includes a configuration named `Run Project Pulse Dashboard` that opens the app from `app/` and loads `index.html`.
- The dashboard presents project cards clearly, with visible status and priority cues, without breaking when data values vary.
- The Orchestrator can explain how the Planner, Designer, and Coder responsibilities fit together and how the parallel work and dependencies supported the build.

## Open questions

- Should the dashboard include a static summary count or only project cards in the initial version?
- Which project statuses are explicitly expected in the first iteration: active, at risk, blocked, on track, or done?
- Do we want the designer to define a single polished palette or keep the design minimal and neutral for broad contributor use?
- Should `project-data.json` be hand-authored for the exercise or generated from a more realistic data model later?
- Is the preview configuration expected to use a live local server or a simple static file launch that opens the browser directly?

## Decision summary

The plan keeps the work simple, ordered, and traceable: the Planner defines the architecture and dependencies, the Designer shapes the experience and styling, and the Coder wires the app files and preview configuration. The tasks are intentionally sequenced to avoid mismatches between data structure, HTML structure, and CSS behavior, while still allowing parallel work in the design/data-prep stage before final preview validation.

# Agent team

The team has three specialists coordinated by an Orchestrator:

- **Orchestrator** (Claude Opus 4.7): Breaks the request into phases, delegates work with explicit file scopes, manages dependencies and parallel work, and verifies the integrated result. It coordinates but does not implement. Definition: [orchestrator.agent.md](../.github/agents/orchestrator.agent.md).
- **Planner** (Claude Opus 4.7): Researches the repository and produces an implementation plan covering file assignments, dependencies, edge cases, validation, and open questions. It does not write code. Definition: [planner.agent.md](../.github/agents/planner.agent.md).
- **Coder** (GPT-5.5): Implements assigned application logic and support files, following repository patterns and validating the result. For Project Pulse, its app guidance includes using `app` as the working directory and opening `index.html`. Definition: [coder.agent.md](../.github/agents/coder.agent.md).
- **Designer** (Gemini 3.1 Pro): Handles assigned UI/UX, accessibility, hierarchy, interaction flow, visual clarity, and responsive behavior. For Project Pulse, it shapes a polished dashboard with project cards, status badges, and clear priority treatment. Definition: [designer.agent.md](../.github/agents/designer.agent.md).

## How they work together

The Planner first studies the existing app and proposes an ordered plan with file ownership and validation expectations. The Orchestrator turns that plan into scoped phases, delegating design work to the Designer and implementation work to the Coder. They can work in parallel when their file scopes do not overlap and neither task depends on the other's output; otherwise, the Orchestrator sequences them. The Orchestrator then checks that the dashboard and runnable app fit together and reports the outcome. The team does not stage, commit, or push changes; those Git operations remain with the learner.
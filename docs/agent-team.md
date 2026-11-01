# Project Pulse agent team

I will use GitHub Copilot CLI in a Codespace to coordinate the custom agents defined in `.github/agents/` and build Mona's Project Pulse dashboard.

| Agent | Model | Responsibility | Definition |
|---|---|---|---|
| Orchestrator | Claude Opus 5.5 (copilot) | Coordinates the specialists, assigns clear file scopes and phases, integrates their work, and reports the result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the project and creates an implementation plan with file assignments, dependencies, risks, and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Guides the dashboard's usability, accessibility, information hierarchy, interaction flow, visual design, and responsive behavior. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements and validates the assigned app code and runnable support files, following repository patterns. | `.github/agents/coder.agent.md` |

The Orchestrator will first ask the Planner for a Project Pulse implementation plan. It will then coordinate the Designer on the dashboard experience and the Coder on the static app, keeping their file scopes clear and sequencing any dependent work. Finally, the Orchestrator will verify the integrated dashboard and hand off the result.

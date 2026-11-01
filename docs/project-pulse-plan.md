# Project Pulse Dashboard Implementation Plan

## Summary
Build Mona’s lightweight static Project Pulse dashboard so contributors can see project owners, status, recent activity, priority/risk, and concise summaries. The exact page title and visible heading are `Project Pulse`. Use HTML/CSS/JSON and VS Code preview config `Run Project Pulse Dashboard`, serving `app/` and opening `index.html`.

## Ordered implementation steps and file assignments
1. Confirm shared design/data contract: Designer guides hierarchy/accessibility/visual and responsive expectations; Coder agrees on JSON fields and HTML/CSS hooks. No files necessary in this phase.
2. Implement data and page: Coder owns `app/project-data.json` (valid JSON, top-level `projects`, each with `name`, `owner`, `status`, `recentActivity`, `priority`, representative examples and concise summaries) and `app/index.html` (exact title/heading, link styles.css, load JSON, semantic accessible project cards using `project-card`, display all fields, useful loading/error/empty states). Designer advises, no code unless assigned.
3. Style: Designer owns `app/styles.css` (selectors `.dashboard`, `.project-card`, clear badges/priority, responsive readable layout, border-radius, box-shadow, focus states, reduced motion). Coder aligns markup/hooks, avoids design file absent assignment.
4. Launch support: Coder owns `.vscode/launch.json`, strict JSON, config named `Run Project Pulse Dashboard`, cwd `${workspaceFolder}/app`, `python3 -m http.server 5500`, serverReadyAction opens `http://localhost:%s/index.html`. Independent authoring possible but integration test waits for app files.
5. Integrate and validate: Orchestrator reviews files, resolves integration through agents, reports checks/limits.

## Dependencies and parallel work
Designer visual/accessibility guidance and Coder JSON authoring can be parallel. Launch config can be authored independently given fixed command/URL. Agree data contract and markup/style hooks before wiring components. Browser integration test after all app files exist; final validation in order: parse JSON, start server, confirm launched index page.

## Edge cases and risks
Fetch may fail with file://; validate over configured HTTP server and show useful error. Handle malformed/unavailable JSON, empty project list, blank/missing fields, long text and narrow screens. Status/priority cannot rely on color alone; maintain contrast, focus visibility, semantic headings. Diagnose port 5500 conflict/ready-output mismatch, never claim launch validation without checking. Python HTTP server is only local preview, not production.

## Validation expectations
- Run `python3 -m json.tool app/project-data.json` and `python3 -m json.tool .vscode/launch.json`.
- Check JSON's `projects` and required fields on every entry.
- Check HTML exact `Project Pulse`, links to both assets, cards showing all fields.
- Check CSS `.dashboard`, `.project-card`, `border-radius`, `box-shadow`, responsive rules, focus/contrast treatment.
- Run VS Code config `Run Project Pulse Dashboard`; verify browser opens `/index.html` on reported port, renders UI/cards, not directory listing; stop server.
- Check `.github/workflows/3-step.yml` as repo acceptance criteria but note workflow does not prove browser behavior.

## Open questions
Sample project data can be illustrative unless real data is provided. Include a summary field per project despite only five required fields; brief does not prescribe names/owners/statuses/priority. Browser/production target unspecified; validate local VS Code preview only.

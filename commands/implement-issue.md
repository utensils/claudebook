Implement the changes described in GitHub issue $ARGUMENTS.

## Steps

1. **Fetch the issue** — Get the full issue details:
   - Strip any `#` prefix from the argument to get the issue number
   - Run `gh issue view <number> --json title,body,labels,comments` to fetch the issue
   - Read the title, description, and all comments carefully

2. **Understand the context** — Research the codebase before making changes:
   - Identify which domains, files, and systems are affected
   - Read the relevant source files to understand the current behavior
   - Check `docs/` for any existing documentation on the affected area
   - Review related tests to understand expected behavior and edge cases
   - If the issue references other issues or PRs, fetch those for additional context

3. **Ask clarifying questions** — Before implementing, check for ambiguity:
   - If the issue is underspecified, missing acceptance criteria, or has multiple valid interpretations, stop and ask the user for clarification
   - If the scope seems larger than expected, confirm the approach before proceeding
   - If there are architectural decisions to make, present the options with trade-offs

4. **Plan the implementation** — Outline the approach:
   - Enter plan mode and draft a step-by-step implementation plan
   - Identify all files that need to be created or modified
   - Note any migrations, new dependencies, or configuration changes required
   - Call out risks or areas that need extra care
   - Wait for the user to approve the plan before proceeding

5. **Implement the changes** — Execute the plan:
   - Follow the patterns and conventions documented in CLAUDE.md
   - Write tests alongside the implementation (not after)
   - Reference the issue number in code comments only when the context isn't self-evident
   - Update documentation in `docs/` if the change affects documented features
   - **Leverage agents and teams for parallel work** — when the implementation involves independent workstreams (e.g., DAL + API route + UI, or multiple unrelated files), use subagents to work on them concurrently. Examples:
     - Spawn agents to research different parts of the codebase in parallel during the planning phase
     - Use agents to implement independent modules simultaneously (e.g., one for the data layer, one for tests)
     - Delegate verification tasks (format, lint, typecheck, test) to a background agent while continuing work
   - Prefer agents over sequential execution whenever tasks don't depend on each other

6. **Verify** — Ensure everything works:
   - Run `pnpm format` to format all modified files
   - Run `pnpm lint` to check for linting errors
   - Run `pnpm tsc --noEmit` to verify types compile
   - Run `pnpm test` to ensure all tests pass (existing and new)
   - If any check fails, fix the issues before proceeding

7. **Report** — Summarize what was done:
   - List the files created or modified
   - Describe the approach taken and any trade-offs made
   - Note the issue number for commit messages (e.g., `Closes #<number>`)
   - Flag anything that needs manual testing or follow-up

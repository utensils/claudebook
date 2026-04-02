Review and incorporate valid feedback from the current pull request.

## Steps

1. **Identify the PR** — Determine which PR to review:
   - Run `gh pr view --json number,url,title` to get the current branch's PR
   - If no PR exists, inform the user and stop

2. **Fetch all review comments** — Gather feedback:
   - Run `gh pr view --json reviews,comments` to get top-level PR comments and reviews
   - Use `gh api repos/{owner}/{repo}/pulls/{number}/comments` to get inline review comments
   - Focus on unresolved comments and actionable feedback

3. **Triage each comment** — For every piece of feedback, decide:
   - **Will incorporate**: The feedback is valid and improves the code
   - **Won't incorporate**: The feedback is a style preference we disagree with, is based on a misunderstanding, or would introduce unnecessary complexity

4. **Make changes** — For feedback you're incorporating:
   - Implement the requested changes
   - Run `pnpm format`, `pnpm lint`, `pnpm tsc --noEmit`, and `pnpm test` after changes
   - Fix any issues introduced by the changes

5. **Respond to comments** — For every comment:
   - **Incorporated**: Reply confirming the change was made (e.g., "Done — updated to use `X` instead")
   - **Not incorporating**: Reply with a clear, respectful explanation of why (e.g., "I'd prefer to keep this as-is because..." or "This is intentional — the reason is...")
   - Use `gh api` to post replies to review comments

6. **Commit and push** — If changes were made:
   - Stage and commit using conventional commit format: `fix(scope): incorporate PR feedback`
   - Include specifics in the commit body about what was addressed
   - Push to the branch: `git push`

7. **Summary** — Report back what was changed and what was declined, with reasoning.

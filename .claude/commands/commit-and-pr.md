Let's commit the changes. Run tests, typechecks, and format checks. Then commit, push, and create a pull request.

## Workflow

Make a todo list for all the tasks in this workflow and work on them one after another.

### 1. Run Checks

Detect the available commands from `CLAUDE.md`, `package.json`, `Makefile`, or other config files.

Common check commands to try:

- **Tests**: `bun test` / `npm test` / `pytest` / `cargo test` / `go test ./...`
- **Typecheck**: `bun run typecheck` / `npx tsc --noEmit` / `mypy`
- **Format check**: `bun run format:check` / `npx prettier --check .` / `ruff format --check`
- **Lint**: `bun run lint` / `npx eslint .` / `ruff check`

Run all available checks. If any fail, fix the issues before proceeding.

### 2. Stage Changes

Review what will be committed:

```bash
git status
git diff
```

Stage the relevant files:

```bash
git add <specific-files>
```

Prefer adding specific files over `git add -A` to avoid accidentally including unintended files (`.env`, generated files, etc.).

### 3. Write Commit Message

Analyze the changes and write a clear commit message:

- **Format**: `<type>: <short summary>` (imperative mood, under 72 chars)
- **Types**: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `perf`
- **Body** (optional): Add after a blank line to explain _why_ the change was made, not just _what_

Examples:

- `feat: add streaming support to message handler`
- `fix: handle null response from GitHub API`
- `refactor: extract token validation into separate function`

### 4. Commit

```bash
git commit -m "$(cat <<'EOF'
type: short summary

Optional longer explanation of why this change was made.
EOF
)"
```

### 5. Push

```bash
git push -u origin <branch-name>
```

If push fails due to network issues, retry up to 3 times with brief waits.

### 6. Create Pull Request

```bash
gh pr create --title "<PR title>" --body "$(cat <<'EOF'
## Summary
- Brief description of changes

## Test plan
- [ ] Tests pass
- [ ] Type checks pass
- [ ] Format checks pass
EOF
)"
```

Return the PR URL to the user when done.

## Error Handling

- **Check failures**: Fix the underlying issue, don't bypass with `--no-verify`
- **Merge conflicts**: Resolve conflicts, then re-run checks before committing
- **Push rejected**: Pull latest changes, rebase if needed, then push again

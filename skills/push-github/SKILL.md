---
name: push-github
description: Push code changes to GitHub with auto-generated commit messages
disable-model-invocation: true
allowed-tools: Bash(git status) Bash(git add .) Bash(git commit) Bash(git push) Bash(git branch) Bash(git diff)
---

# Push to GitHub

Push code changes to GitHub with automatic commit message generation and error handling.

## What This Skill Does

1. Analyzes what files changed
2. Creates a meaningful commit message
3. Commits all changes
4. Pushes to the current branch
5. Reports what was pushed

## Workflow

### Step 1: Check Repository Status

Run `git status` to see what's changed.

**What to look for:**
- Modified files
- New files
- Deleted files
- Untracked files

**Expected output:** Current branch name and list of changes

### Step 2: Verify Branch

Run `git branch` to confirm we're on the right branch.

**Important:** If on `main` or `master`:
- Ask the user if they really want to commit directly to main
- Suggest creating a feature branch instead
- Offer to create and switch to a new branch

### Step 3: Stage All Changes

Run `git add .` to stage all changes.

**What this does:** Prepares all modified files for commit

### Step 4: Generate Commit Message

Create a descriptive commit message based on the changes.

**Guidelines for commit messages:**
- Start with a type prefix:
  - `feat:` = New feature
  - `fix:` = Bug fix
  - `refactor:` = Code improvement (no new features)
  - `docs:` = Documentation only
  - `chore:` = Dependencies or config
  - `test:` = Test updates

**Format:** `<type>: <description>`

**Examples:**
- `feat: add user authentication system`
- `fix: resolve null pointer exception in auth`
- `refactor: simplify user service`
- `docs: update API documentation`

**Rules:**
- Keep first line under 72 characters
- Be specific about what changed
- Explain WHY if it's non-obvious
- If unsure, ask the user to provide a message

### Step 5: Commit Changes

Run `git commit -m "your message"` to create the commit.

**What to show:**
- Number of files changed
- Number of insertions/deletions
- Commit hash
- Branch name

### Step 6: Push to GitHub

Run `git push` to push the commit.

**For new branches:** Use `git push -u origin branch-name`

**If push fails:**
- Check the error message
- Common issues:
  - Need to pull latest changes: suggest `git pull origin <branch>`
  - Branch doesn't exist on remote: use `-u` flag
  - Network issue: suggest retrying
- Ask user for next steps

### Step 7: Show Summary

Display what was accomplished:
Pushed to GitHub
├── Branch: [branch name]
├── Commit: [commit message]
├── Files changed: [count]
└── Status: ✓ Success

## Error Handling

### If No Changes to Commit

- Message: "No changes to commit. Working directory is clean."
- Suggest: Create a new feature or fix

### If Push Fails

- Show the error
- Suggest solutions
- Offer to retry

### If Merge Conflicts

- Alert: "Cannot push - merge conflicts detected"
- Suggest: Manually resolve or create separate branch

## Output Format

Always show the summary in this format:
┌─ Pushed to GitHub ─────────────────┐
│ Branch: <branch-name>              │
│ Commits: <count>                   │
│ Message: <commit-message>          │
│ Files changed: <count>             │
│ Status: ✓ Success                  │
└────────────────────────────────────┘


---
name: conventional-commits
description: Standardized git commit messages for the Backtest project. Use when preparing, suggesting, or performing git commits to ensure consistency and GitHub issue linking.
---

# Conventional Commits (Backtest Project)

## Overview
This skill enforces the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) specification for the Backtest project.

## Commit Message Structure
```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### 1. Types
- **feat**: New features.
- **fix**: Bug fixes.
- **docs**: Documentation.
- **style**: Formatting, etc.
- **refactor**: Code restructuring.
- **perf**: Performance improvements.
- **test**: Adding/fixing tests.
- **build**: Build system changes.
- **ci**: CI configuration changes.
- **chore**: Maintenance tasks.

### 2. Description
- Use imperative, present tense ("add" not "added").
- No trailing period.

### 3. Footer (GitHub Integration)
- If an issue or PR number is mentioned (e.g., #34), add it to the footer.
- Format: `Refs: #<number>` or `Closes: #<number>`.

## Workflow
1. Analyze changes with `git diff`.
2. Select type and optional scope.
3. Include GitHub issue refs in the footer if applicable.

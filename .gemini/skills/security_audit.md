# Skill: Security Audit & Credential Protection

This skill provides a rigorous protocol for preventing credential leaks and ensuring codebase security.

## 🛡 Security Rules
- **No-Secret Policy:** Never log, print, or commit API keys, passwords, or tokens.
- **Environment Isolation:** Use `.env` or system variables. Reference them as placeholders (e.g., `${DB_PASSWORD}`) in `application.yml`.
- **Gitignore Hygiene:** Confirm `.env`, `build/`, and local-only config files are in `.gitignore`.

## 🔄 Pre-Commit Audit SOP
Before any `git commit`, perform these steps:
1. **Self-Audit**: Run `git diff --staged` and scan for: `key`, `password`, `secret`, `token`, `auth`, `api_key`.
2. **Global Grep**: Periodically run `git grep` for these patterns to catch historical leaks.
3. **Isolation Check**: Ensure `*.sample` or `*.template` files are updated with placeholders, not actual values.

## 📜 Execution Rules
- If a secret is detected, **abort the commit** and ask the user for rotation/cleanup instructions.
- Never use `chmod 777` or any command that compromises system integrity.

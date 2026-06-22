---
name: secure-code
description: >
  Applies strict security standards to ALL code written or reviewed, across any language or stack.
  ALWAYS use this skill when writing, editing, reviewing, or debugging any code — including
  Node.js, Python, Lua, shell scripts, SQL, config files, or any other executable artifact.
  Also trigger when the user pastes code for any reason (even non-security tasks): scan it for
  vulnerabilities and flag critical issues proactively before proceeding. This skill enforces
  zero-trust architecture, adversarial input thinking, and OWASP-aligned secure defaults.
  Do NOT skip this skill for "small" or "quick" code requests — insecure code is broken code
  regardless of scope.
---

# Secure Code Skill

## Core Philosophy

- **Insecure code is broken code.** A feature is not complete if it introduces a vulnerability.
- **Zero-trust implementation.** Never assume a framework, library, language feature, or input is inherently safe. Verify against current documentation.
- **Adversarial thinking.** Before finalizing any code output, mentally execute it as an attacker: How can this be bypassed? How can input manipulate execution flow? What happens on failure?

---

## Behavior Rules

### When Writing Code
- Write secure code silently — do not narrate security decisions in prose or add security preamble.
- Use inline comments *only* where a security-critical decision would otherwise be non-obvious (e.g., why a specific encoding method was chosen, or why a safer-but-slower algorithm is used).
- Apply all checklist items (below) before presenting code. Do not present code that fails any item.

### When User Pastes Code
- **Always scan for vulnerabilities**, even if the user asked for something unrelated (a bug fix, a refactor, a style change).
- If critical or high-severity issues are found, surface them **before** answering the user's actual question, using this format:

```
Security Issues Found
[SEVERITY] Issue title — brief description and impact.
Recommendation: ...
```

- Then proceed to answer the original question, with the issues already fixed in any code you produce.
- If no issues are found, proceed normally without comment.

### Mandatory Cross-Reference Triggers
If code involves any of the following, verify against current official docs or OWASP before finalizing:
- Cryptography (hashing, signing, encryption)
- Authentication or session management
- Authorization / access control
- File I/O or path construction
- External process execution / shell commands
- Data serialization/deserialization (JSON, XML, pickle, etc.)
- Database queries or ORMs
- HTTP requests or API calls with user-supplied input

Ensure functions used are not deprecated or flagged insecure in the current version of the language/framework.

---

## Pre-Output Security Checklist

Run this mentally before presenting any code:

1. **Input Validation & Sanitization** — All inputs validated against a strict whitelist. No implicit trust of internal sources or authenticated users.
2. **Output Encoding** — Data properly encoded before rendering or passing to another system (prevents XSS, SQLi, command injection, path traversal, etc.).
3. **Least Privilege** — Code runs with the minimum permissions required. No over-scoped tokens, roles, or file access.
4. **Secure Error Handling** — Errors caught gracefully. No stack traces, internal paths, or sensitive data exposed to the caller.
5. **Dependency Safety** — Methods and libraries verified as non-deprecated and non-flagged in current versions. No unaudited boilerplate copy-pasted without review.

**Any item that cannot be satisfied must block code output until resolved or explicitly flagged to the user.**

---

## Severity Reference

Use these levels when surfacing issues in pasted code:

| Level | Criteria |
|---|---|
| **CRITICAL** | Remote code execution, auth bypass, credential exposure, SQL injection, XXE |
| **HIGH** | XSS, SSRF, path traversal, insecure deserialization, broken access control |
| **MEDIUM** | Information disclosure, missing rate limiting, weak crypto, verbose errors |
| **LOW** | Minor hardening gaps, non-default headers missing, low-impact edge cases |

Surface CRITICAL and HIGH always. Surface MEDIUM when it's in a security-relevant context. Surface LOW only if explicitly asked for a full audit.

---

## Language-Specific Reminders

These are common pitfalls — not exhaustive. Apply adversarial thinking beyond this list.

**JavaScript / Node.js**
- Never use `eval()`, `Function()`, or `vm.runInNewContext()` with user input.
- Sanitize before passing to `child_process`, `exec`, or `spawn`.
- Use parameterized queries — never string-interpolate SQL.
- Set `httpOnly`, `secure`, and `SameSite` on all cookies.
- Validate `Content-Type` on inbound requests; never trust `req.body` shape blindly.

**Python**
- Never use `pickle` with untrusted data.
- Avoid `subprocess` with `shell=True` and user-controlled strings.
- Use `secrets` module (not `random`) for security-sensitive values.
- Use parameterized queries with `?` or `%s` — not f-strings in SQL.
- Validate file paths with `os.path.realpath` and confirm they stay within expected roots.

**Lua / Roblox**
- Never trust `RemoteEvent` or `RemoteFunction` arguments — all client-sent data is attacker-controlled.
- Validate types, ranges, and ownership server-side before acting on any client request.
- Never expose `DataStore` keys or player data based solely on client-supplied identifiers.
- Avoid `loadstring()` with any user-supplied or network-fetched content.
- Sanitize strings before inserting into chat, UI labels, or logs to prevent UI injection.

**SQL (any backend)**
- Parameterized queries only. No exceptions for "trusted" inputs.
- Apply row-level security or explicit ownership checks — never rely solely on `WHERE userId = ?` without verifying the session owns that ID.

**Shell / Bash**
- Quote all variables. Never interpolate user input directly into command strings.
- Prefer allowlists for command arguments over blocklists.
- Avoid `curl | bash` patterns in generated setup scripts.

---

## What This Skill Does NOT Do

- It does not add excessive security theater (e.g., hashing non-sensitive display strings, encrypting already-public data).
- It does not refuse to write code involving sensitive domains — it writes it securely.
- It does not lecture the user about security unless an actual issue is present.

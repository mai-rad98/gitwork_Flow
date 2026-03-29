# Git Workflow & Version Control Policy

**Organization:** Payflo AI (Engineering Team)
**Applies to:** All Developers (Team of 4)
**Maintained by:** Technical Lead

---

# 1. Purpose

This document defines the standardized Git workflow, commit conventions, and collaboration practices to ensure:

* Clean and maintainable code history
* Efficient team collaboration
* High-quality, production-ready code
* Scalable development practices aligned with fintech systems

---

# 2. Branching Strategy

We adopt a **Modified Git Flow** approach.

## Main Branches

* **main** → Production-ready code only
* **develop** → Integration branch for ongoing work

## Supporting Branches

* **feature/** → New features
* **bugfix/** → Non-critical bug fixes
* **hotfix/** → Urgent production fixes

### Naming Convention

```
feature/<feature-name>
bugfix/<issue-name>
hotfix/<issue-name>
```

### Examples

```
feature/payment-api
bugfix/login-error
hotfix/transaction-failure
```

---

# 3. Development Workflow

## Step 1: Start Work

* Always branch from `develop`

```
git checkout develop
git pull origin develop
git checkout -b feature/<name>
```

---

## Step 2: Development & Commits

* Commit frequently using **Conventional Commits**
* Ensure code builds and passes tests locally

---

## Step 3: Push & Pull Request (PR)

* Push branch to remote
* Open PR targeting `develop`

---

## Step 4: Code Review (Mandatory)

* Minimum **1 approval required**
* All CI checks must pass
* Address all review comments before merge

---

## Step 5: Merge Strategy

* Use **Squash & Merge**
* Delete branch after merge

---

## Step 6: Release Process

* Merge `develop` → `main` when stable
* Tag release versions using semantic versioning

```
git tag v1.2.0
```

---

## Step 7: Hotfix Process

```
git checkout main
git checkout -b hotfix/<issue>
```

* Fix issue
* Merge into:

  * `main`
  * `develop`
* Tag the hotfix release on `main` (bumps PATCH version):

```
git tag v1.2.1
```

---

# 4. Commit Message Standard (Conventional Commits)

## Format

```
<type>(scope): <short description>
```

---

## Allowed Types

| Type     | Description          |
| -------- | -------------------- |
| feat     | New feature          |
| fix      | Bug fix              |
| refactor | Code improvement     |
| chore    | Maintenance          |
| docs     | Documentation        |
| test     | Test-related changes |
| style    | Formatting changes   |

---

## Examples

```
feat(payments): add transaction endpoint
fix(auth): resolve token expiration issue
refactor(api): simplify validation middleware
chore(deps): update dependencies
```

---

## Breaking Changes

```
feat(api)!: change response structure
```

---

# 5. Enforcement Rules

## 5.1 Branch Protection

* No direct commits to `main`
* No direct commits to `develop`
* PR required for all changes

---

## 5.2 Code Review Requirements

* Minimum 1 reviewer approval
* CI pipeline must pass
* No self-merging unless approved

---

## 5.3 Commit Enforcement

* All commits must follow **Conventional Commits**
* Enforced via:

  * commitlint
  * pre-commit hooks (Husky)

---

## 5.4 Pull Request Requirements

Each PR must include:

```
## Description
## Linked Issue / Ticket
## Type of change (feat/fix/refactor/etc.)
## How to test
## Screenshots (if applicable)
```

---

# 6. Versioning Strategy

We use **Semantic Versioning (SemVer)**:

```
MAJOR.MINOR.PATCH
```

| Version Type | Meaning          |
| ------------ | ---------------- |
| MAJOR        | Breaking changes |
| MINOR        | New features     |
| PATCH        | Bug fixes        |

---

# 7. Best Practices

* Keep branches short-lived (**< 5 days**)
* Keep PRs small and focused
* Write meaningful commit messages
* Always pull latest `develop` before starting work
* Resolve conflicts locally before pushing
* Ensure code is tested before PR submission

---

# 8. CI/CD Pipeline Overview

All PRs trigger the following automated checks:

| Stage     | What it does                              |
| --------- | ----------------------------------------- |
| Lint      | Runs ESLint / code style checks           |
| Test      | Runs unit and integration test suites     |
| Build     | Verifies the project compiles successfully|
| Security  | Scans dependencies for known vulnerabilities |

* PRs cannot be merged until all stages pass
* Merges to `main` trigger the deployment pipeline

---

# 9. Prohibited Practices

* ❌ Direct commits to `main`
* ❌ Long-lived feature branches
* ❌ Large, unreviewable PRs
* ❌ Non-descriptive commit messages (e.g., “fix stuff”)
* ❌ Skipping code review process

---

# 10.  Continuous Improvement

This workflow will evolve as the team grows.
Suggestions for improvement should be raised during:

* Sprint retrospectives
* Engineering sync meetings

---

# 11. Summary

This Git workflow ensures:

* Consistent development practices
* Improved code quality
* Scalable collaboration
* Production stability

All team members are expected to follow this policy.

---

**Approved by:** Technical Lead
**Effective Date:**  29/03/2026

# 🧭 Contributing Guidelines

Thank you for contributing to this project!  
This document explains our **Git branching strategy (GitFlow Minimal)**, **Pull Request rules**, **Release versioning**, and **Back-merge process**.

---

## 🌳 1. Branching Strategy (GitFlow Minimal)

We use a **simplified GitFlow model** to keep our workflow clean and predictable.

### Main Branches
| Branch | Purpose |
|---------|----------|
| `main` | Contains production-ready code only. Every commit here represents a stable release. |
| `develop` | Contains the latest approved development code. All new features start from this branch. |

### Supporting Branches
| Branch | Description | Example |
|---------|--------------|----------|
| `feature/*` | Used to develop new features | `feature/login-page` |
| `release/*` | Used to prepare a new release | `release/v1.2.0` |
| `hotfix/*` | Used to fix urgent issues in production | `hotfix/v1.2.1` |

---

## ⚙️ 2. Workflow

### 🧩 Create a Feature
```bash
git checkout develop
git checkout -b feature/feature-name
````

After finishing the feature:

```bash
git checkout develop
git merge --no-ff feature/feature-name
git branch -d feature/feature-name
git push origin develop
```

### 🚀 Create a Release

```bash
git checkout develop
git checkout -b release/v1.2.0
```

Perform final tests or fixes, then:

```bash
git checkout main
git merge --no-ff release/v1.2.0
git tag v1.2.0
git push origin main --tags
```

Back-merge release changes to `develop`:

```bash
git checkout develop
git merge --no-ff release/v1.2.0
git push origin develop
```

### 🩹 Create a Hotfix

```bash
git checkout main
git checkout -b hotfix/v1.2.1
```

After fixing:

```bash
git checkout main
git merge --no-ff hotfix/v1.2.1
git tag v1.2.1
git push origin main --tags

git checkout develop
git merge --no-ff hotfix/v1.2.1
git push origin develop
```

---

## 🧱 3. Pull Request (PR) & Continuous Integration (CI) Rules

* ✅ **Only “Squash and Merge”** is allowed for PRs
* 👀 **At least one reviewer approval** required before merging
* 🧪 **All CI checks (tests, linting, build)** must pass
* 🚫 **Direct commits to `main`** are not allowed

These rules ensure clean commit history and maintain high-quality code.

---

## 🏷️ 4. Version Tagging (Semantic Versioning)

We follow the **Semantic Versioning (SemVer)** format:

```
vMAJOR.MINOR.PATCH
```

| Type  | Example | Meaning                          |
| ----- | ------- | -------------------------------- |
| MAJOR | v2.0.0  | Incompatible API or big changes  |
| MINOR | v1.1.0  | Backward-compatible new features |
| PATCH | v1.0.1  | Small bug fixes or hotfixes      |

To create and push a tag:

```bash
git tag v1.1.0
git push origin v1.1.0
```

---

## 🔄 5. Back-Merge Process

After each **release** or **hotfix**, merge `main` back into `develop`:

```bash
git checkout develop
git merge main
git push origin develop
```

This ensures `develop` stays up to date with the latest production code.

---
# GitFlow Strategy Branching

## 1. What it is
GitFlow is a **rulebook for branches** in Git.  
It says: keep two main lines of code, then create short-lived branches for new work and fixes.

- **main** – always the **production** code (what users see).
- **develop** – the **integration** or “next release” code (where features are combined).
- **feature/*** – one branch per task/feature.
- **release/*** – prep branch before going live (polish, version bump).
- **hotfix/*** – urgent fix created from `main`.

Think of it like school groupwork:
- `main` = final paper you submit.
- `develop` = your group’s shared draft.
- `feature/*` = each member’s personal draft for their section.
- `release/*` = final proofreading copy.
- `hotfix/*` = emergency correction after you already submitted.

---

## 2. Why it’s important
- **Safety:** Break things in your own feature branch, not in production.
- **Teamwork:** Everyone knows **where** to branch from and **where** to merge.
- **Predictable releases:** `develop` always has the next version; `main` is always stable.
- **Fast fixes:** `hotfix/*` lets you patch production without waiting for other work to finish.

---

## 3. How to use it

### Initial setup (once per repo)
```bash
# start from an existing repo with main
git checkout -b develop
git push -u origin develop
```

### Daily work (one feature)
```bash
# 1) branch off from develop
git checkout develop
git pull
git checkout -b feature/login-form

# 2) code, commit, push
git add .
git commit -m "Add login form UI and validation"
git push -u origin feature/login-form

# 3) open a PR: feature/login-form -> develop (on GitHub)
#    after review, merge it.
```

### Preparing a release
```bash
# cut a release branch from develop
git checkout develop
git pull
git checkout -b release/1.2.0
# bump version, fix small bugs, update changelog
git commit -am "Bump to 1.2.0; update changelog"
git push -u origin release/1.2.0

# PR: release/1.2.0 -> main (go live)
# also merge release/1.2.0 back into develop to keep them in sync
```

### Emergency hotfix on production
```bash
# branch from main for urgent fix
git checkout main
git pull
git checkout -b hotfix/1.2.1-critical-bug

# fix + commit + push
git commit -am "Fix critical NPE on login"
git push -u origin hotfix/1.2.1-critical-bug

# PR: hotfix -> main (deploy)
# then PR: hotfix -> develop (so dev branch also gets the fix)
```

---

## 4. Quick mental map
```
main  <--- hotfix -----
  ^        /           \
  |---- release ------  \
          ^              \
        develop <--- feature <--- your work
```

---

## 5. Common gotchas
- **“Merge conflicts everywhere!”** → Always `git pull` before branching/merging; keep feature branches short-lived.
- **“Forgot to update version/changelog.”** → Do it on the `release/*` branch.
- **“Prod bug but develop is messy.”** → Use `hotfix/*` from `main`.

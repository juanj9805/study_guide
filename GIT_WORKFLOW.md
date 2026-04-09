# Git Workflow — NeoGenesis

## Branch Structure

```
main       → stable, production-ready
Develop    → integration branch (all features merge here first)
JuanJ      → your personal working branch
Ismael / JuanE / Valeria → teammates' branches
```

**Rule:** never commit directly to `Develop` or `main`. Always work on `JuanJ` and open a PR.

---

## Commands You'll Use 90% of the Time

### Checking state
```bash
git status              # what files changed / staged / untracked
git log --oneline -10   # last 10 commits (compact view)
git diff                # see exact line changes before staging
```

### Syncing
```bash
git pull origin Develop         # get latest from team before starting work
git push origin JuanJ           # upload your commits to remote
```

### Saving work
```bash
git add App/Service/DinosaurService.cs   # stage a specific file
git add App/                             # stage everything inside App/
git commit -m "feat: implement dinosaur registration"
```

### Branches
```bash
git branch                                   # list local branches
git checkout JuanJ                           # switch to your branch
git log --oneline --graph --all              # visual branch history
```

### When things go wrong
```bash
git diff HEAD                                        # what changed since last commit
git restore App/Service/DinosaurService.cs           # discard changes in a file
```

---

## Workflow Per Work Session

```
1. START OF SESSION
   git pull origin Develop
   (always sync before touching anything)

2. WHILE WORKING
   - Edit files in App/
   - git status       → check what changed
   - git diff         → review before committing
   - git add <files>  → stage specific files
   - git commit -m "feat: ..."
   
   Commit often — one logical change per commit, not one commit at end of day.

3. WHEN YOUR HU IS DONE
   git push origin JuanJ
   → Open Pull Request on GitHub: JuanJ → Develop
```

---

## Commit Message Convention

Use conventional commits:

```
feat:     new feature
fix:      bug fix
refactor: code change that is not a fix or feature
docs:     documentation only
test:     adding or fixing tests
chore:    tooling, config, dependencies
```

Examples:
```bash
git commit -m "feat: add dinosaur registration endpoint"
git commit -m "fix: null reference in DinosaurService"
git commit -m "refactor: move validation logic to DinosaurValidator"
```

---

## Two Rules to Avoid Problems

1. **Never commit to `Develop` or `main` directly** — always use `JuanJ` and a PR.
2. **Always pull before you push** — if `Develop` moved since your last pull, pull again before pushing.

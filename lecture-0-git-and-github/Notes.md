how to push code to github
1:  git add .                    (dot ko all bolte hai)
2: git commit -m "lecture1 complted"
3: git push -u origin  main
Here’s a complete **Git & GitHub tutorial** from absolute beginner to advanced concepts. You can save it as a `.txt` file or study it right here. The notes are structured step‑by‑step, just like building a todo app — first understand the basics, then layer on advanced skills.

---

## GIT & GITHUB – FROM ZERO TO ADVANCED

### 1. WHAT IS VERSION CONTROL?
- A system that records changes to files over time.
- You can recall specific versions later.
- Essential for teamwork – multiple people can work on the same project without conflicts.

### 2. GIT VS GITHUB
| Git | GitHub |
|---|---|
| A version control system (software) | A cloud platform that hosts Git repositories |
| Runs locally on your machine | Runs on the web (github.com) |
| Tracks changes, manages branches, etc. | Adds collaboration tools (Pull Requests, Issues, Actions) |

---

## SECTION 1: GIT BASICS (LOCAL WORKFLOW)

### 3. INSTALLING GIT
- **Windows**: Download from [git-scm.com](https://git-scm.com) (Git Bash recommended).
- **Mac**: `brew install git` or download from the website.
- **Linux**: `sudo apt install git` (Debian/Ubuntu) or equivalent.

After installation, configure your identity (required for commits):
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

### 4. INITIALIZING A REPOSITORY
Navigate to your project folder and turn it into a Git repository:
```bash
git init
```
This creates a hidden `.git` folder that stores all version history.

### 5. CHECKING THE STATUS
```bash
git status
```
Shows which files are:
- Untracked (new, not yet added)
- Modified (changed since last commit)
- Staged (ready to be committed)

### 6. THE THREE STAGES OF GIT
| Working Directory | Staging Area | Repository (History) |
|---|---|---|
| Your actual files | Files marked to be committed | Committed snapshots |

### 7. ADDING FILES TO STAGING AREA
```bash
git add <filename>        # add a single file
git add .                 # add all changed/new files in current directory
```

### 8. COMMITTING CHANGES
```bash
git commit -m "Your message describing the change"
```
- A commit is a permanent snapshot of the staged files.
- Write meaningful commit messages (present tense, short, descriptive).

### 9. VIEWING COMMIT HISTORY
```bash
git log                   # full log
git log --oneline         # compact, one line per commit
git log --graph --all --oneline   # visual branch graph
```

### 10. UNDOING CHANGES (LOCAL)
- **Unstage a file**: `git reset <file>`
- **Discard changes in working directory**: `git checkout -- <file>` (or `git restore <file>`)
- **Amend the last commit**: `git commit --amend -m "New message"` (only if you haven't pushed yet)

---

## SECTION 2: BRANCHING & MERGING (LOCAL)

### 11. WHAT IS A BRANCH?
A branch is a parallel version of your code. You create a branch to work on a feature without affecting the main codebase.

### 12. BRANCH COMMANDS
```bash
git branch                # list all local branches
git branch feature-xyz    # create a new branch named feature-xyz
git checkout feature-xyz  # switch to that branch
# Or both in one step:
git checkout -b feature-xyz
```

### 13. MERGING BRANCHES
After finishing work on a branch, merge it back:
```bash
git checkout main          # switch to the branch you want to merge INTO
git merge feature-xyz      # merge feature-xyz into current branch
```
- **Fast-forward merge**: if there are no divergent changes, Git just moves the pointer.
- **Three-way merge**: when both branches have new commits, Git creates a merge commit.

### 14. RESOLVING MERGE CONFLICTS
- Occur when the same part of a file was changed differently in two branches.
- Git marks conflicts with `<<<<<<<`, `=======`, `>>>>>>>`.
- Manually edit the file, choose the correct code, then:
```bash
git add <resolved-file>
git commit -m "Merge branch feature-xyz (resolved conflicts)"
```

### 15. DELETING A BRANCH
```bash
git branch -d feature-xyz   # safe delete (only if merged)
git branch -D feature-xyz   # force delete (even if not merged)
```

---

## SECTION 3: WORKING WITH REMOTE REPOSITORIES (GITHUB)

### 16. CREATING A REPOSITORY ON GITHUB
- Log in to github.com → New repository.
- Give it a name (e.g., `my-todo-app`).
- Do **not** initialize with README if you already have a local repo (to avoid conflicts).

### 17. LINKING LOCAL REPO TO GITHUB (REMOTE)
```bash
git remote add origin https://github.com/your-username/your-repo.git
```
- `origin` is the default name for the remote.
- You can verify with `git remote -v`.

### 18. PUSHING YOUR CODE TO GITHUB (FIRST TIME)
```bash
git push -u origin main
```
- `-u` sets the upstream branch, so next time you can just `git push`.
- `main` is the branch name (older repos may use `master`).

### 19. PULLING CHANGES FROM GITHUB
```bash
git pull origin main
```
- Fetches and merges remote changes into your local branch.
- If you just want to download without merging: `git fetch origin`.

### 20. CLONING AN EXISTING REPOSITORY
```bash
git clone https://github.com/someone/repo.git
```
- Copies the entire repository to your local machine.
- Automatically creates a remote called `origin`.

---

## SECTION 4: COLLABORATION WORKFLOW (BASIC)

### 21. FORKING A REPOSITORY
- On GitHub, click "Fork" to create a personal copy of someone else's repo.
- Then clone your forked repo and work on it.
- When ready, open a **Pull Request** from your fork to the original repo.

### 22. PULL REQUESTS (PR)
- A request to merge your branch into another (usually the original project's main branch).
- Steps:
  1. Push your branch to your remote repo.
  2. On GitHub, click "Compare & pull request".
  3. Add a title and description, then create the PR.
  4. The project maintainer reviews and merges (or requests changes).

### 23. KEEPING YOUR FORK IN SYNC
```bash
git remote add upstream https://github.com/original-owner/repo.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

---

## SECTION 5: ADVANCED GIT TECHNIQUES

### 24. GIT STASH – SAVE WORK WITHOUT COMMITTING
Temporarily save changes that are not ready for a commit:
```bash
git stash                 # save current modifications
git stash list            # view all stashes
git stash pop             # reapply the most recent stash
git stash apply stash@{0} # reapply a specific stash
git stash drop stash@{0}  # delete a stash
```

### 25. REBASE – A CLEANER HISTORY
Instead of merging, you can rebase your feature branch onto main. This replays your commits one by one on top of the latest main.
```bash
git checkout feature-xyz
git rebase main
```
**Caution**: Never rebase commits that have already been pushed to a shared remote, unless you're the only one working on that branch.

### 26. INTERACTIVE REBASE – REWRITE COMMIT HISTORY
```bash
git rebase -i HEAD~3   # modify the last 3 commits
```
Allows you to:
- **pick** (keep)
- **squash** (combine with previous)
- **reword** (change message)
- **drop** (delete)
- **fixup** (combine discarding the message)

### 27. CHERRY-PICK – COPY A SPECIFIC COMMIT
Apply a single commit from another branch to your current branch:
```bash
git cherry-pick <commit-hash>
```

### 28. TAGS – MARK IMPORTANT COMMITS (e.g., releases)
```bash
git tag v1.0.0                   # lightweight tag
git tag -a v1.0.0 -m "Release version 1.0.0"   # annotated tag
git push origin --tags           # push tags to remote
```

### 29. GITIGNORE
Create a `.gitignore` file to exclude files/folders from being tracked:
```
node_modules/
.env
*.log
dist/
```
- Add, commit, and push the `.gitignore` file to share with the team.

### 30. REVERT – UNDO A COMMITTED CHANGE (SAFELY)
Unlike reset, revert creates a new commit that undoes the changes:
```bash
git revert <commit-hash>
```

### 31. RESET – MOVE BRANCH POINTER (CAREFUL!)
- `git reset --soft <commit>` : keeps changes staged.
- `git reset --mixed <commit>` : keeps changes in working directory (default).
- `git reset --hard <commit>` : **discards all changes** – use with caution.

### 32. GIT BISECT – FIND A BUGGY COMMIT
Binary search through commit history to locate the commit that introduced a bug:
```bash
git bisect start
git bisect bad   # current commit is bad
git bisect good <known-good-commit>
# Git checks out a middle commit, test it, then run:
git bisect good  # or git bisect bad
# Repeat until the faulty commit is found
git bisect reset
```

### 33. SUBMODULES – INCLUDE OTHER REPOS
```bash
git submodule add https://github.com/user/library.git libs/
```
The main repo tracks a specific commit of the submodule.

### 34. GIT HOOKS – AUTOMATE TASKS
Scripts in `.git/hooks/` that trigger before/after certain Git actions (pre-commit, post-commit, pre-push). Example: run linting before each commit.

### 35. WORKTREES – MULTIPLE WORKING DIRECTORIES
Checkout multiple branches simultaneously in different directories:
```bash
git worktree add ../project-hotfix hotfix-branch
```

---

## SECTION 6: COMMON WORKFLOWS

### 36. FEATURE BRANCH WORKFLOW
- `main` branch is always deployable.
- Each new feature gets its own branch: `feature/signup-form`.
- Open a PR from feature branch → `main`.
- After merge, delete the feature branch.

### 37. GIT FLOW (LEGACY, STILL USED)
- `main` – production releases.
- `develop` – integration branch.
- `feature/*` – new features.
- `release/*` – preparation for a new production release.
- `hotfix/*` – urgent fixes on `main` that get merged into both `main` and `develop`.

### 38. TRUNK-BASED DEVELOPMENT
- Developers commit directly to a single `main` branch (or short-lived branches).
- Use feature flags to hide unfinished features.

---

## SECTION 7: TIPS & BEST PRACTICES

- **Commit often**, with clear messages.
- **Pull before you push** to avoid conflicts.
- **Use `.gitignore`** from the start.
- **Never commit secrets** (API keys, passwords).
- **Review your own code** before opening a PR.
- **Keep branches short-lived** to ease merging.
- **Learn to use `git status` and `git diff` frequently**.
- **Backup**: push regularly to a remote.

---

## SECTION 8: CHEAT SHEET OF MOST COMMON COMMANDS

```bash
git init                     # start a repo
git status                   # see current state
git add .                    # stage all changes
git commit -m "msg"          # commit staged
git log --oneline            # see history
git branch                   # list branches
git checkout -b new-branch   # create and switch
git merge branch-name        # merge branch
git remote add origin URL    # connect to GitHub
git push -u origin main      # first push
git push                     # subsequent pushes
git pull                     # fetch + merge
git clone URL                # download repo
git stash                    # temporary save
git stash pop                # reapply stash
git rebase main              # rebase current branch
git tag v1.0.0               # create tag
git reset --hard HEAD~1      # undo last commit (destructive)
```

---

This document covers everything from installing Git to advanced topics like rebase, hooks, and submodules. Use it as a reference while you build projects and collaborate on GitHub. Practice each command in a test repository to really understand how they work.
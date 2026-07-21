What is Git?
  Git is a Version Control System (VCS). It helps track changes,
  collaborate with teams, and restore previous versions of files.

Why Git?
  -   Tracks file history
  -   Supports teamwork
  -   Enables branching and merging
  -   Helps recover previous versions

Git Workflow
  Working Directory -> Staging Area -> Local Repository -> Remote
  Repository (GitHub)

Basic Commands
  git –version - Check installed Git version.
  git config –global user.name “Your Name” - Configure your Git username.
  git config –global user.email “you@example.com” - Configure your Git
  email.
  git config –list - View Git configuration.
  git init - Initialize a new Git repository.
  git status - Show repository status.
  git add  - Stage one file.
  git add . - Stage all changes.
  git commit -m “message” - Save staged changes.
  git log - View detailed commit history.
  git log –oneline - View short commit history.
  git diff - Show unstaged changes.
  git diff –cached - Show staged changes.

Branching
  git branch - List branches.
  git branch feature - Create a branch.
  git switch feature - Switch to a branch.
  git checkout -b feature - Create and switch to a branch.
  git merge feature - Merge feature into current branch.

Remote Repository
  git remote add origin  - Connect local repo to GitHub.
  git remote -v - View remote repositories.
  git push -u origin main - push to GitHub (update the branch accordingly).
  git push - Push latest commits.
  git clone  - Download a repository.
  git fetch - Download remote changes only.
  git pull - Fetch and merge remote changes.

Undo Changes
  git restore  - Discard local file changes.
  git restore –staged  - Unstage a file.
  git reset –soft HEAD~1 - Undo last commit but keep staged changes.
  git reset HEAD~1 - Undo last commit and unstage changes.
  git reset –hard HEAD~1 - Remove last commit and discard changes.
  git revert  - Create a new commit that reverses an older commit.

Stash
  git stash - Temporarily save work.
  git stash list - View stashes.
  git stash pop - Restore latest stash.

Tags
  git tag v1.0 - Create a tag.
  git push origin v1.0 - Push tag.

Best Practices:
  -   Commit frequently with meaningful messages.
  -   Pull before pushing.
  -   Never commit passwords or secrets.
  -   Use .gitignore for temporary/generated files.
  -   Work in feature branches.
  -   Review code before merging.

Daily Commands: most common commands we use in our daily life 
  git status 
  git add . 
  git commit -m “message” 
  git pull 
  git push 
  git log –oneline 
  git branch 
  git switch 
  git merge 
  git stash 
  git diff

one liner

```bash
git remote remove origin && git checkout --orphan new_branch && git add -A && git commit -m "Initial commit" && git branch -D master && git branch -m master
```

```bash
# Create a new orphan branch with no history
git checkout --orphan new_branch

# Stage all files (they'll be in unstaged state initially)
git add -A
git commit -m "Initial commit"

# Delete the old main/master branch
git branch -D master

# Rename current branch to main/master
git branch -m master

# Force push to remote (if needed)
git push -f origin main
```
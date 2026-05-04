- Delete Branch
```bash
git push -d origin <branchname>   # Delete remote
git branch -d <branchname>        # Delete local
```

- Rename Branch
```bash
git branch -m <new_branchname> # current branch
# or
git branch -m <old_branchname> <new_branchname>
```

- Revert to a previous commit
```bash
# staging vs change vs discard
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1

# if reset to specific commit
git reset --hard 9c6f19b4905cbc749bebdfefd46ec40e18a8c3c9

git push --force
```
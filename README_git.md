# Git How To

## Initialise repository

Initialise repo per the following link:

[Publishing a new repo to GitHub from VS Code](https://losol.io/publishing-a-new-repository-to-github-from-vs-code/)

### Set up Git repo on local machine:

1. Create your new repository on GitHub. Do not add README, license or gitignore for now. Note the “remote repository URL”, which you will need in step 7 instead of **URL**.
2. Open terminal
3. *Initialize* a new Git repository: `git init`
4. *Stage* all your files before first commit: `git add .`
5. *Commit* the files: `git commit -m “Project started”`
6. *Add* remote repository: `git remote add origin {**URL**}`
7. *Verify* the remote repository: `git remote -v`
8. *Push* the first changes: `git push -u origin master`

Action (8) basically says push to origin (remote repo) the diff from master (local repo).

### And to update after a change to .gitignore:

1. run *Add*, *Commit*, *Push*
2. *Remove* cache from index (staging area): `git rm -r --cached .`
3. run *Add*, *Commit*, *Push*

### Additional valuable commands

[Visit learngitbranching.js.org to learn how to git](https://learngitbranching.js.org/)

* View *reflog* and history *log*, such as: `git log -5` and `git reflog -5`
* *Branches* are essentially *pointers* to a specific commit, and can be created by: `git checkout -b "branchName"` or doing both the following: `git branch "branchName"`, `git checkout branchName`
* *Merging* branches to master: merge commits and changes onto target branch, preserves history, better merge conflicts, easy to undo, can be messy (graphically): `git checkout master`, `git merge branchName`
* *Rebasing* branches to master: moves the commits and changes onto the target branch, a clean history, readable graph, harder to undo: in one command - `git rebase <CommitTo> <CommitFrom>`, or in two commands - `git checkout <CommitFrom>`, `git rebase <CommitTo>`
* View the *diff* between branches: `git diff <<branch1>> <<branch2>>`
* *Graphically* depict branch history with: `git show-branch -a`
* *HEAD* represents the commit that git is working off, which is moved using the `git checkout <<pointer>>` command.  To work off a specific commit (like a branch name commit pointer): `git checkout <<commit_tag>>`
* We can use the git branch pointer using `~n` to move n number commits upstream: `git checkout HEAD~4`, `git checkout master~3`, `git checkout branchName~1` etc...
* To *force-move a pointer* to a different commit: `git branch -f <<branchName>> <<pointer>>`, ie: `git branch -f master HEAD~3` will force the master commit pointer upstream 3 levels relative to HEAD
* A *reset* on a branch will work *locally* to move upstream of the commit we want removed: `git reset HEAD~1`.  However, these changes are not pushed / shared with remote streams.
* A *revert* on a branch will work *remotely* to move upstream of the commit we want removed, which it does by creating a new commit that completely reverses all preceding changes, thus, preserving history: `git revert HEAD`
* We can *cherry-pick* to apply the selected commits to the currently checked-out branch: `git cherry-pick <Commit1> <Commit2> <...>`
* We can also do some crazy shit by using *interactive rebase* to pick and squash and do other stuff: `git rebase -i <Commit1>`
* Using *tag* we can create a permanent pointer to a commit, like a version release: `git tag AlphaVer <Commit1>`
* We can determine where we are relative to tags by using: `git describe --tags <CommitName>`; output might be like: `alphaDemo-4-g2e087f6` (<tagName>-<# Commits upstream>-g<CurrentCommitHash>)
* Both git *pull* and git *merge* download data from a remote repo.  A `git pull` is roughly the equivalent of doing a `git fetch`, followed by a `git merge`.  Fetch downloads remote repo data only.  Pull downloads remote repo data, then integrates it into local HEAD branch current working copy files

### More additional valuable commands

[Compliments dev.to article](https://dev.to/jacobherrington/4-useful-patterns-in-git-19ac)

* *amend* last commit with a new file / file change, eg: `git add README.md` and `git commit --amend`.  You will be prompted to modify the commit message, then the staged changes will be pushed
* *split commit* into several commit chunks, by resetting the HEAD and adding the chunks: `git reset HEAD~1` and cycle the following: `git add --patch`, `git commit -m "some message 1"`; `git add --patch`, `git commit -m "some message 1"`...
* *stash* changes using `git stash`, do things / checkout another branch, then recover using `git stash apply` (which will leave the accessible for later) or `git stash pop`
* *squash commits* by either (1): moving up the tree (x commits) with `git reset HEAD~x` and squash by `git commit -am "commit message"`; or, (2): `git rebase -i master` (where master == branch name), and using *pick* or *squash* to choose what commits to select / squash

## Git Comments

Will follow the recommendations proposed in [Contributing to Pandas](https://pandas.pydata.org/pandas-docs/stable/development/contributing.html#committing-your-code)

* ENH: Enhancement, new functionality
* BUG: Bug fix
* DOC: Additions/updates to documentation
* TST: Additions/updates to tests
* BLD: Updates to the build process/scripts
* PERF: Performance improvement
* CLN: Code cleanup
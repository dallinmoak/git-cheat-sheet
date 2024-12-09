## Basic editing
|Name|Command|Definition
|:---|:---|:---
| __add__ |`git add [arg]`| stages changes to a directory or file specified by [arg]. `.` specifies all changes in cwd.
| __commit__ | `git commit [arg]` | creates a commit based on staged changes to the file or directory specified by [arg]. git will prompt for a message or one can be added after the `-m` flag. `.` specifies all changes in cwd.
| __push__ | `git push [optional...]` | pushes current local commits to the upstream remote.

## intermediate editing
|Name|Command|Definition
|:---|:---|:---
| __fetch__ | `git fetch [optional...]` | update all remote-tracking branches with changes from the actual remote
| __pull__ | `git pull` | do everything that fetch does *and* attempt to merge changes from the remote tracking branch asociated with the current branch into the current local branch. Often can be done pretty automatically
| __merge__ | `git merge [optional]` | merges changes from `[optional]` refs into the current local branch, or the asociated remote tracking branch if no arg is given. useful to manually manage a merge that can't be fast forwarded.

## branching
|Name|Command|Definition
|:---|:---|:---
| __checkout branch__ | `git switch [branch-name]` | check out the branch identified by `[branch-name]`. also switch is a thing
| __new branch__ | `git switch -c [branch-name]` | create and checkout a new branch identified by `[branch-name]`.
| __delete branch__ | `git branch -d [branch-name]` | delete the branch locally. also nice is to delete on the remote with `git push origin --delete [branch-name]`. if the remote is already deleted, `git fetch -p` will prune the remote tracking branch from your client. 
 
## other
|Name|Command|Definition
|:---|:---|:---
| __stash__ | `git stash [optional...]` | stashes all tracked changes and staged changes. `--staged` targets only staged changes, and `--keep-index` targets everything else
| __pop__ | `git stash pop` | removes the most recently added set of changes from the stash and applies them
| __apply__ | `git stash apply` | applies the most recent set from the stash, but keeps them in the stash.
| __cherry pick__ | `git cherry pick [commit id]` | applies the changes in the commit specified by `[commit id]` to the current branch. 

### notes on merge
 - `git pull` usually attempts a fast-forward merge that doesn't actually add a merge commit. this is the default behavior on most git setups. there's a config to change that.
 - merging that can't be fast-forwarded must be reconsiled manually. git will put up all the conflicting files in your cwd with those <<<<<< and >>>>>> signs to indicate incoming and outgoing changed lines. you stage all the merge candidate files and then commit the merge and it creates a merge commit.
 - fast forward is when the incomming changes can just be applied on top of the existing stuff by just tacking it on to the existing history. really nice and convenient for a sense of continuity across multiple remotes and clients.

 ### notes on remote
 - local git repos have a remote origin repo with a set of branches that may or may not match up with local branches. `fetch`, `push` and `pull` are the way to keep the remote and local in sync.
- each local branch can have a remote tracking branch that's on my local machine, but is separate from my actual current branch. this separation is good for comparing / inspecting change before actually applying them. `git status` is good for this. also `git diff [branch]..origin/[branch]` prints those out

### notes on branches
- each branch can have its own history and can interact with the remote indepentently of the others. but the cool thing is branches can be merged into other branches so that their histories are reconciled. 
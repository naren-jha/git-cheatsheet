# git-cheatsheet
List of most frequently used git commands

## add git branch to iterm
* https://stackoverflow.com/a/20309062/4210068 + https://stackoverflow.com/a/58528709/4210068
* https://stackoverflow.com/a/58375763/4210068
* https://www.mfitzp.com/tutorials/add-git-branch-name-to-terminal-prompt-mac/
* [UPDATE] Use "oh my zsh" instead

## setup
* `git init`
* `echo "/bin/" >> .gitignore`
* `git clone [url]`
* `git config --global user.name "[firstname lastname]"`
* `git config --global user.email "[valid-email]"`
* `git config --global color.ui auto`

## checkout
* `git checkout origin/[remote-branch-name] -b [local-branch-name]`
* `git checkout [file-or-folder]`
* `git checkout .`
* `git checkout [branch-name] -- [file-or-folder]` Get file/folder from another branch

## switch - newer way of doing checkout
* `git switch [branchname]` - Switch to a different branch
* `git switch -c [branchname]` - Create a new local branch (from current one) and then switch to it

## status, add, commit, push, pull
* `git status`
* `git add [file-or-folder1] [file-or-folder2] [file-or-folder3]`
* `git add .`
* `git commit -m “[commit message]”`
* `git push`
* `git push origin [local-branch-name]:[remote-branch-name]` 
  - use `-u` to associate to a remote
  - use `-f` to force the push
* `git pull`
* `git fetch` - fetch down all the branches from remote
* `git merge [alias]/[branch]` - merge a remote branch into your current branch to bring it up to date
* `git commit -am "[commit message]"` - add (all local change) and commit in one command

## alias
* `git config --global alias.ALIAS "WHAT"`
  - example: `git config --global alias.st "status"`

## branch
* `git branch` list local branches
* `git branch [branch_name]` create a new local branch form the current local
* `git branch --sort=-committerdate` list local branches in descending order of commit date
* `git branch --sort=committerdate` list local branches in ascending order of commit date
* `git branch -a | grep -i “[branch-name]”` search for a branch name across local and remote
* `git branch -r | grep -i “[branch-name]”` search for a branch name in all remote branches
* `git config --global alias.br "for-each-ref --sort=-committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))'"` 
create alias for colored branch listing in descending order of commit date and then use git br 
* `git branch -D [branch-name]` delete a local branch
* `git push origin :[remote-branch-name]` delete a remote branch

## clean, remove
* `git clean -f`
* `git clean -df`
* `git clean -fdx`
* `git clean -f [untracked-file-or-folder]` remove untracked [file/path]
* `git rm [file]`
* `git rm --cached [file-name]` remove already added file

## reset
* `git reset HEAD`
* `git reset --hard HEAD`
* `git reset --hard origin/[remote_branch]`
* `git reset [commit_hash]`
* `git reset HEAD [file_name]` To remove a file from staging after 'git add'

## log
* `git log` - Show the commit history for the currently active branch
* `git log -[n]` - Show 'n' most recent commit on the current branch
* `git log --oneline` OR `git log --pretty=oneline` - Show one liner pretty log
* `git log [file_name]` - See commit log of a file
* `git log --follow [file]` - Show the commits that changed file, even across renames
* `git log -p <file_name>` - See diffs of a file
* `git log -p [commit_hash] -- [file_name]` - See diff of a file from a particular commit
* `git log branchB..branchA` - Show the commits on branchA that are not on branchB
* `git reflog`
* `gitk [file_name]`
* See beautified log
  - create alias like this: `git config --global alias.lg "log --all --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'\n--abbrev-commit --date=relative"`
  - then use `git lg` instead of `git log`, like
  - `git lg`
  - `git lg [file_name]`
* See beautified log - one line
  - create alias like this: `git config --global alias.lpr "log --pretty=oneline"`
  - then use `git lpr`

 
## diff
* `git diff [local_file_fully_qualified_name]` - see local changes made in a particular file
* `git diff [commit_id]~ [commit_id]` - see changes added as part of a particular commit:
* list all files in a commit
  - `git diff-tree --no-commit-id --name-only -r [commit_id]`
  - or create alias: 
  - `git config --global alias.files "diff-tree --no-commit-id --name-only -r"`
  - and then use: `git files [commit_id]`
* `git diff branchB...branchA` - show the diff of what is in branchA that is not in branchB
* `git show [SHA]` - show any object in Git in human-readable format

## stash
* `git stash` - stash all changes in local and get a clean repository
* `git stash list` - show list of all stash
* `git stash apply` - apply top of stash stack without removing it
* `git stash pop` - apply top of stash stack and remove it
* apply stash by index-number / stash-id
  - `git stash apply [stash_number_or_stash_id]`
  - `git stash pop [stash_number_or_stash_id]`
* `git stash push -m “message” [file_or_folder1] [file_or_folder2] [file_or_folder3]` - stash selected file or folder
* `git stash drop stash@{n}` - to delete specific stash
* `git stash clear` - to delete all stash

## rebase
### interactive rebasing and squashing commits into one
* https://docs.gitlab.com/ee/topics/git/git_rebase.html
* https://stackoverflow.com/a/41464876
* squash last n commits into one
  - `git rebase -i HEAD~3` OR `git rebase -i [commit-hash]`
  - press i to edit
  - 'pick' and 'squash' the commits as you like (most of the time, you would want to keep the first commit as 'pick' and change remaining commits to 'squash')
  - press ESC
  - `:wq!` [w - save/write, q - exit/quit, ! - don't ask for confirmation]
  - in the next screen, edit the commit message as you like
  - then again `:wq!`
  - If you haven’t pushed your commits to the remote branch before rebasing, push your changes normally. 
  - If you had pushed these commits already, force-push instead by using following commands
  - `git push --force` OR 
  - `git push --force-with-lease` (use this command when collaborating with other developers, why? - https://stackoverflow.com/a/37460330)
  - https://youtu.be/RwvTrSm7zEY

#### squashing while merging into another branch (using git merge)
* `git merge --squash [origin/feature]` - this will bring all the changes that's been done in origin/feature into your local but it will not commit it. you'll have to commit and push yourself. 
* so `git commit -m "mergin feature-xyz into master"` and `git push`
* this change is already staged so you don't have to do `git add`


### rebase vs merge [ff (fast-forward) merge commit vs rebase merge]
* https://youtu.be/7Mh259hfxJg
* first update your local master `git switch master` and then `git pull` Then
* go to your feature branch `git switch [feature_branch]` And then 
* `git rebase master` - rebase feature_branch on the tip of current master. be aware that 'rebase' rewrites history; so never rebase commits that's been shared with other people, that means if you've alraedy pushed your commits to remote, most likely others will be using it, so DON'T rebase if your work is already on remote.

## cherry-pick
* `git cherry-pick [commit_hash]`
* `git cherry-pick [fromCommit]^..[toCommit]`
  - carrot (^) is used to point to immediate previous commit. use carrot (^) in fromCommit to include fromCommit, without ^ cherry-pick excludes fromCommit.
* `git push` - to push the changes to remote
* `git cherry-pick --quit` - to conclude the cherry-pick (end the cherry-pick sequence)

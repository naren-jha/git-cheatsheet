# git-cheatsheet
List of most frequently used git commands

## setup
* git init
* echo "/bin/" >> .gitignore
* git clone [url]
* git config --global user.name "[firstname lastname]"
* git config --global user.email "[valid-email]"
* git config --global color.ui auto

## checkout
* git checkout origin/[remote-branch-name] -b [local-branch-name]
* git checkout [file-or-folder]
* git checkout .
* get file/folder from another branch
  - git checkout [branch-name] -- [file-or-folder]

## status, add, commit, push
* git status
* git add [file-or-folder1] [file-or-folder2] [file-or-folder3]
* git add .
* git commit -m “[commit message]”
* git push
* git push origin [local-branch-name]:[remote-branch-name]

## alias
* git config --global alias.ALIAS "WHAT"
  - example: git config --global alias.st "status"

## branch
* git branch
* list local branches in descending order of commit date
  - git branch --sort=-committerdate
* list local branches in ascending order of commit date
  - git branch --sort=committerdate
* search for a branch name
  - git branch -a | grep -i “[branch-name]”
* create alias for colored branch listing in descending order of commit date
  - git config --global alias.br "for-each-ref --sort=-committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))'" 
  - and then use git br
* delete a local branch
  - git branch -D [branch-name]
* delete a remote branch
  - git push origin :[remote-branch-name]

## clean, remove
* git clean -f
* git clean -df
* git clean -fdx
* remove untracked [file/path]
  - git clean -f [untracked-file-or-folder]
* git rm [file]
* remove already added file
  - git rm --cached [file-name]

## reset
* git reset HEAD
* git reset HEAD --hard
* git reset [commit_hash]
* To remove a file from staging after 'git add'
  - git reset HEAD [file_name]

## log
* Show the commit history for the currently active branch
  - git log
* See commit log of a file
  - git log [file_name]
* Show the commits that changed file, even across renames
  - git log --follow [file]
* See diffs of a file
  - git log -p <file_name>
* See diff of a file from a particular commit
  - git log -p [commit_hash] -- [file_name]
* Show the commits on branchA that are not on branchB
  - git log branchB..branchA
* git reflog
* gitk [file_name]
* See beautified log
  - create alias like this: git config --global alias.lg "log --all --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'\n--abbrev-commit --date=relative"
  - then use 'git lg' instead of 'git log':
  - examples: 
    - git lg
    - git lg [file_name]
 
## diff
* to see local changes made in a particular file
  - git diff [local_file_fully_qualified_name]
* to see changes added as part of a particular commit:
  - git diff [commit_id]~ [commit_id]
* list all files in a commit
  - git diff-tree --no-commit-id --name-only -r [commit_id]
  - or create alias: 
  - git config --global alias.files "diff-tree --no-commit-id --name-only -r"
  - and then use: git files [commit_id]
* Show the diff of what is in branchA that is not in branchB
  - git diff branchB...branchA
* show any object in Git in human-readable format
  - git show [SHA]

## stash
* stash all changes in local and get a clean repository
  - git stash
* show list of all stash
  - git stash list
* apply top of stash stack without removing it
  - git stash apply 
* apply top of stash stack and remove it
  - git stash pop 
* apply stash by [index-number / stash-id]
  - git stash apply [stash_number_or_stash_id]
  - git stash pop [stash_number_or_stash_id]
* stash selected file or folder
  - git stash push -m “message” [file_or_folder1] [file_or_folder2] [file_or_folder3]
* to delete specific stash
  - git stash drop stash@{n}
* to delete all stash
  - git stash clear



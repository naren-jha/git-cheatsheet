# git-cheatsheet
List of most frequently used git commands

## checkout
* git checkout origin/remoteBranchName -b localBranchName
* git checkout .
* get file/folder from another branch
  - git checkout <branch> -- <file_or_folder_path>

## status, add, commit, push
* git status
* git add <file_or_folder1> <file_or_folder2> <file_or_folder3>
* git commit -m “commit message”
* git push
* git push origin localBranchName:remoteBranchName

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
  - git branch -a | grep -i “branchName”
* create alias for colored branch listing in descending order of commit date
  - git config --global alias.br "for-each-ref --sort=-committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))'" 
  - and then use git br
* delete a local branch
  - git branch -D <branch_name>
* delete a remote branch
  - git push origin :<remote_branch_name>

## clean
* git clean -df
* remove untracked file/path
  - git clean -f <untracked_file_or_folder>

## diff
* to see local changes made in a particular file
  - git diff <local_file_fully_qualified_name>
* to see changes added as part of a particular commit:
  - git diff <commit_id>~ <commit_id>

## reset
* git reset HEAD
* git reset HEAD --hard
* git reset <commit_hash>

## log
* git log
* To see commit log of a file:
  - git log <file_name>
* To see diffs of a file:
  - git log -p <file_name>
* To see diff of a file from a particular commit
  - git log -p <commit_hash> -- <file_name>
* git reflog
* gitk <file_name>
* beautified log
  - crate alias like this: git config --global alias.lg "log --all --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'\n--abbrev-commit --date=relative"
  - then use 'git lg' instead of 'git log':
    * git lg
    * git lg <file_name>
    * etc

## stash
* stash all changes in local and get a clean repository
  - git stash
* show list of all stash
  - git stash list
* apply top of stash stack without removing it
  - git stash apply 
* apply top of stash stack and remove it
  - git stash pop 
* apply stash by index number / stash_id
  - git stash apply <stash_number_or_stash_id>
  - git stash pop <stash_number_or_stash_id>
* stash selected file or folder
  - git stash push -m “message” <file_or_folder1> <file_or_folder2> <file_or_folder3>


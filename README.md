# git-cheatsheet
List of most frequently used git commands

## git checkout
* git checkout origin/remoteBranchName -b localBranchName
* git checkout .

## status, add, commit, push
* git status
* git add <file_or_folder1> <file_or_folder2> <file_or_folder3>
* git commit -m “commit message”
* git push
* git push origin localBranchName:remoteBranchName

# alias
* git config --global alias.ALIAS "WHAT"
  - example: git config --global alias.st "status"

## git branch
* git branch
* git branch --sort=-committerdate  # DESC
* git branch --sort=committerdate  # ASC
* git branch -a | grep -i “branchName”
* create alias for colored branch listing in descending order of commit date
  - git config --global alias.br "for-each-ref --sort=-committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))'" 
  - and then use git br

## remove untracked file/path:
* git clean -df
* git clean -f <untracked_file_or_folder>

## diff
* to see local changes made in a particular file
  - git diff <local_file_fully_qualified_name>
* to see changes added as part of a particular commit:
  - git diff <commitId>~ <commitId>

## get file/folder from another branch
* git checkout <branch> -- <file_or_folder_path>

## reset
* git reset HEAD
* git reset <commit_hash>

## log
* git log
* git reflog

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


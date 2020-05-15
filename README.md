# git-cheatsheet
List of most frequently used git commands

## search for branch name
* git branch -a | grep -i “branchName”

## git checkout
* git checkout -f origin/remoteBranchName -b localBranchName
* git checkout .

## add, commit, push
* git add <file_or_folder1> <file_or_folder2> <file_or_folder3>
* git commit -m “commit message”
* git push origin -u localBranchName:remoteBranchName

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


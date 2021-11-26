# Cheatsheet for git
## Table of contents 
TODO
## Setup
### config
To show configs list:
```
git config --list
```
To config user's email:
```
git config --global user.email "<your-email>"
```
To config user's name:
```
git config --global user.name "<your-name>"
```
To config text-editor used for writting commit messages:
```
git config core.editor "<text-editor>"
```
## Commands

### init
To init a respo in a directory, move to that directory and use:
```
git init
```
### status
Show information about changes since last commit:
```
git status
```
### add
To stage files/folders:
```
git add <{multiples} files/folders path>
``` 

To stage all files in current directory:
```
git add .
```
To stage all changes made for both `TRACKED` and `UNTRACKED` files:
```
git add -A
```
To stage all changes made for only `TRACKED` files:
```
git add -u
```

### commit
Commit by open some text editor to type message:
```
git commit
```
To commit with message:
```
git commit -m "<your-message>"
```

### reset
To revert staged changes of a file, better use `restore` though:
```
git reset <file> # copy state of a file of last commit to current staging area
git checkout <file> # now file changes is unstaged, we can use commands related to revert unstaged changes.
```
To undo x commit, remove changes from staging area but keep the changes in working directory:
```
git reset HEAD~<x>
```
To undo x commit but keep the changes in staging area and keep the changes working directory:
```
git reset --soft HEAD~<x>
```
To undo x commit, remove changes from staging area and also remove changes in working directory:
```
git reset --hard HEAD~<x>
```
### restore
Should be used for revert staged/unstaged instead of `checkout/reset`.

To revert unstaged changes of files since last commit:
```
git restore <files>
```
To revert staged changes of files since last commit:
```
git restore --staged <file>
git restore <files>
```

### log
To view commit history:
```
git log
```
View commit history with oneliner message:
```
git log --oneline
```
### ls-files
To checkout which files currently in staging area:
```
git ls-files
```
### checkout
Should be used to checkout commits only, for branches, it is better to use `switch`.

To checkout a commit in commit history and enter `DETACHED HEAD` state:
```
git checkout <commit-hash>
```
To switch to a branch:
```
git checkout <branch-name>
```
To create a branch and switch to it:
```
git checkout -b <new-branch-name>
```
To revert changes of `unstaged` files, though `restore` should be used here:
```
git checkout <files>
``` 
### branch
To view all available branches and current branch:
```
git branch
```
To create a branch, but not switch to it
```
git branch <new-branch-name>
```
To delete a branch which has been merged to another:
```
git branch -d <{multiples} branch-name>
```
To delete a branch whether it's been merged or not:
```
git branch -D <{multiple} branch-name>
```
To create a new branch contain a commit and all commits before it, this is typically used to deal with `detached-head` state, after this we can merge this new branch as needed:
```
git branch <new-branch-name> <commit-hash>
```
To rename current branch:
```
git branch -M <new-branch-name>
```

### switch
Better use this to working with branches than `checkout`.

To switch to a branch:
```
git switch <branch-name>
```
To create a branch and switch to it:
```
git switch -c <new-branch-name>
```

### merge
First switch to your main branch, that mean the branch you want changes from other branch to merge into.

To merge changes from other branch into current branch:
```
git merge <branch-name>
```
### clean
To see which files will be removed when running `-df`, this should be run first:
```
git clean -dn
```
To remove untracked files:
```
git clean -df
```
### stash
Quite useful when dealing with unstaged changes, when get a stash, the basic flow maybe as follow:
- git stash apply
- git restore .

Or
- git stash pop
- git stash

To list all stash available in the stash's stack:
```
git stash list
```
To stash current unstaged changes and push it on top of the stash's stack:
```
git stash
```
To push the current stash to the top of the stash's stack, but with some message/comment:
```
git stash push -m "<stash-message>"
```

To apply the stash at the x'th position of the stash's stack, if not specified, x will default to 0, which is the top element, notice that this will not remove the stash:
```
git stash apply <x>
```
Similar to `stash apply`, but will pop the specified stash, if not specified, x will be 0:
```
git stash pop <x>
```
To remove some specific stash x:
```
git stash drop <x>
```
To clear the whole stash's stack:
```
git stash clear
```
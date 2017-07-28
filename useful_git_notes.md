1. Git Tutorial: Commands [link](https://www.siteground.com/tutorials/git/commands.htm)





2. Learn Git: [link](https://www.atlassian.com/git/tutorials/setting-up-a-repository)

## Setting up a repository
* Initializing a new Git repo    // git init 'project directory'
* Cloning an existing Git repo   // git clone 'repo url'
* Committing a modified version of file to the repo 
   -git add '--all' // add file to staging area
   -git commit -m 'msg' // commit file to the repo
* Configuration & set up: git config
   -git remote add < remote_name >  < remote_repo_url >   // map remote repo at 'remote_repo_url' to a ref in local repo 'name'
   -git push -u < remote_name orgin> < local_branch_name master>  //once mapped the remote repo, you can  push local branches to it
   
   -git config --global user.name 'name'  | git config --global user.email 'email'  // tell git who you are.
   
 ___
 
## Saving changes
* git add  < file | directory >  // changes are not actually recorded until you run < git commit > 
* git stash  // takes your uncommitted changes (both staged and unstaged), saves them away for later use.[git-stash](https://www.atlassian.com/git/tutorials/git-stash) 
>git add : add modified file to the queue to be committed later. (in staging area)

>git commit: commit the added file to **local** repo and creates a new version with log

>git push: push the commit file to **remote** repo

[git_remote|git_pull|git_push](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)

## staging area: a container where git collects all changes which will be part of next commit
To stage a file is simply to prepare it finely for a commit. Git, with its index allows you to commit only certain parts of the changes you've done since the last commit.

[stage area](https://git-scm.com/book/zh-tw/v1/Git-%E5%9F%BA%E7%A4%8E-%E6%8F%90%E4%BA%A4%E6%9B%B4%E6%96%B0%E5%88%B0%E5%84%B2%E5%AD%98%E5%BA%AB)
LOCAL:
file in working directory --> (git add file) **-->** file in 'staging area' --> (git commit) **-->** file in local repo 

## Undoing Changes [undo](https://www.atlassian.com/git/tutorials/undoing-changes)
1. git checkout: checking out files, checking out commits, and checking out branches.
   git checkout is an easy way to “load” any of these saved snapshots onto your development machine.
   
   **git checkout serves as a way to revert back to an old version of an individual file**
   git checkout <commit>  //turn the 'files' from <commit> to the staging area. (undo commit)
   
2. git revert
   Instead of removing the commit from the project history, it figures out how to undo the changes introduced by the commit and appends a new commit with the resulting content.
   
   git revert <commit> // Generate a **new commit** that undoes all of the changes introduced in <commit>
   
3. git reset (a dangerous way)
   it reverts back to the previous state of a project by **removing** all subsequent commits
   git reset <commit> //commits are no longer referenced by any ref or the reflog
   
4. git clean
   The git clean command removes untracked files from your working directory.




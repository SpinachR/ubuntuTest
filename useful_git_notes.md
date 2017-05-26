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



#VeePiO Git Style Guide

* [Branching](#branching)  
* [Merging](#merging)
* [Distribution](#distribution)
* [Commits](#commits)
* [Commit messages](#commit-messages)
* [Useful git commands](#useful-git-commands)
* [Useful git tools](#useful-git-tools)


_inspired by..._  
* [Vincent Driessen's ultimate branching model](http://nvie.com/posts/a-successful-git-branching-model/)  
* [git flow](https://github.com/nvie/gitflow/tree/master)


##Branching    
The only two REQUIRED branches on github:    
- `develop`  
- `master`  
 
#### `develop`   
This is our working branch from which releases will be built. No feature or fix should be committed to develop that is not complete, working and tested on another branch. Develop should be treated as releasable at all times.

#### `master`  
Commits to `master` are released builds. The commit name and tag should reflect the build number and version number of the release.

#### other branches
All other branches should have a clearly-labelled function. Start new features using a `feature/feature_name` branch. Try to isolate discrete features to separate branches.

	
None of these branches _needs_ to be pushed to github, but any of them _may_ be pushed up. Owner is responsible for deleting completed branches from github.

##Merging

merging - especially to develop - should be a two-way process to minimise conflicts. First merge FROM develop TO your branch, then merge the result BACK to develop.

example: I have just finished a feature on an experimental branch `feature/thing`. It's good and I want to merge it.  

  
First `git fetch` to update your local copy of remote indexes:

	git fetch -a  
	
(This is not necessary but good practice: updates all local copies of remote indexes. `fetch` ensures `git status` will accurately report when a local branch is out of sync with a remote.)
	
Ensure your local version of `develop ` is in sync with remote (on github):

	git checkout develop  
	git pull

switch back to the branch we want to merge, then update it with latest master:

    git checkout feature/thing
    git merge develop
    
now merge back in the other direction..

    git checkout develop
    git merge feature/thing
 
    


##Commits

Make commits little and often. 

One commit should relate to one meaningful unit of work. 

_Never commit code that does not compile_ 

##Commit messages

A commit message should provide a short description of the commit content. 
     
Fine-grained commits with meaningful messages greatly facilitate tracking of regression bugs either manually or using [git bisect](https://git-scm.com/docs/git-bisect). 

Do not use the same commit message repeatedly -  no _cont_  _cont_ _cont_

##Useful git commands
_reporting_  
`git status` - shows status of current branch - modified/staged files, comparision with remote  
`git log` - history of commits  
`git log --oneline` - abbreviated history (useful for changelogs) 

_undo_   
`git reset --soft HEAD^` - undo the most recent commit, retaining file modifications since last commit  
`git reset --hard HEAD^` - undo the most recent commit, losing file modifications since last commit (state is rewound to previous commit)  
_cf stackoverflow: [How do you undo the last commit?](http://stackoverflow.com/q/927358/1375695) ...  
 if you've already pushed to a remote, too late mate._
 
 _back out of a conflicted merge_  
`git merge --abort`  
cf [Dealing with merge conflicts](https://www.git-tower.com/learn/git/ebook/command-line/advanced-topics/merge-conflicts)

_filesystem_   
`git mv <oldname> <newname>` rename/move a file whilst retaining git history  
`git rm --cached <file>` remove a file from the git repository without removing it from the filesystem  
_cf stackoverflow: [How to remove a file from the index in git?](http://stackoverflow.com/a/2223340/1375695)_


##Useful git tools
2. XCode git management is not to be trusted. Don't use.
3. For simple git tasks, use the commandline.
4. For GUI tasks (like resolving merge commits, browsing commit history):  
    - [SmartGit](http://www.syntevo.com/smartgit/)
    - [SourceTree](https://www.sourcetreeapp.com)
    



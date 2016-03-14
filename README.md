
#VeePiO Git Style Guide

* [Branching](#branching)  
* [Merging](#merging)
* [Distribution](#distribution)
* [Commits](#commits)
* [Commit messages](#commit-messages)

_inspired by..._  
* [Vincent Driessen's ultimate branching model](http://nvie.com/posts/a-successful-git-branching-model/)  
* [git flow](https://github.com/nvie/gitflow/tree/master)


##Branching    
The only two REQUIRED branches on github:    
- `master`  (aka 'release' in VD's branching model)  
- `archive`  ('master' in VD's branching model)  
 
#### `master`   
This is our working branch from which archives will be built. No feature or fix should be committed to master that is not complete, working and tested on another branch. Master should be treated as publishable at all times.

#### `archive`  
Commits to ARCHIVE are actual XCode archive builds intended for distribution. The commit name and tag should reflect the build number and version number of the build.

#### other branches
All other branches should have a clearly-labelled owner and only that owner should commit to that branch. 

One 'master' per named developer
eg   
`mr_lucas`  
`rick`  
`foundry`    
_'jonathan' is a reserved keyword!_

Sub-branches can be created and 'owned' by using a slash-naming convention

l's branches  

	l/feature  
	l/tryout  
	l/whatever  
	
ricks  

	r/thing
	r/other
	
jm's (foundry)

	f/this
	f/that 
	f/theother
	
None of these branches _needs_ to be pushed to github, but any of them _may_ be pushed up. Owner is responsible for deleting completed branches from github.

##Merging

merging - especially to master - should be a two-way process to minimise conflicts. First merge FROM master TO your branch, then merge the result BACK to master.

example: I have just finished a feature on an experimental branch `f/thing`. It's good and I want to merge it.  

    git checkout foundry
    git merge f/thing
    
when I am satsfied with the result, I want to merge `foundry` with `master`.   

First `git fetch` to update your local copy of remote indexes:

	git fetch -a  
	
(This is not necessary but good practice: updates all local copies of remote indexes. `fetch` ensures `git status` will accurately report when a local branch is out of sync with a remote.)
	
Ensure your local version of `master` is in synch with remote (on github):

	git checkout master  
	git pull

switch back to the branch we want to merge, then update it with latest master:

    git checkout -b foundry
    git merge master
    
now merge back in the other direction..

    git checkout master
    git merge foundry
 
    
##Distribution

When creating an archive for distribution, build from the master branch. When archive is complete, commit with archive build number and merge `master` to `archive`. The commit and tag names should include version number and build. 

No other commits or merges should be made to `archive`.



##Commits

Make commits little and often. 

One commit should relate to one meaningful unit of work. 

_Never commit code that does not compile_ 

##Commit messages

A commit message should provide a short description of the commit content. 
     
Fine-grained commits with meaningful messages greatly facilitate tracking of regression bugs either manually or using [git bisect](https://git-scm.com/docs/git-bisect).



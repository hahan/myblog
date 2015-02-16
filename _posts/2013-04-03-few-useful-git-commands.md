---
layout: post
title: Few useful Git commands
date: 2013-04-03 00:50:00.000000000 -07:00
categories:
- git
- git commands
tags: []
status: publish
type: post
published: true

---
I have been using [Git](http://git-scm.com/) at work for last couple of years now and I must say it has helped me a lot to be more productive and pushing out more and more features instead of either waiting for code reviews or waiting for the expensive branches (as in Perforce) to get created.

I won't go into details on how Git has helped me and why I love this tool but rather will post some very useful commands that helps to get around some very tricky situations. I found these commands from various posts while looking for solutions to these problems I encountered while at work. So yes, these are not 'my' solutions but they do work.

####How to get a list of un-pushed commits in git?
Assuming your remote repository is named origin and you’re dealing with the master branch:
  
	$ git log master ^origin/master
	
This shows what commits are in master but not in origin/master (which is the remote branch).

This same syntax can be used to see the difference between two local branches, but will show cherry-picked commits as differences which can be confusing:
   
	$ git log master ^production

####Delete last commit
To soft delete the commit before head. Alternatively you can refer to the SHA-1 of the hash you want to reset to.


--soft option will delete the commit but it will leave all your changed files "Changes to be committed", as git status would put it.

	$ git reset --soft HEAD~1
	
If you want to get rid of any changes to tracked files in the working tree since the commit before head use --hard instead.

Now if you already pushed and someone pulled which is usually my case, you can't use git reset. You can however do a git revert,
  
	$ git revert HEAD
	
This will create a new commit that reverses everything introduced by the accidental commit.

####Make an existing git branch track a remote branch?
Given a branch foo and a remote upstream, as of Git 1.7.0:
	
	$ git branch --set-upstream foo upstream/foo

That will cause Git to make local branch foo track remote branch foo from upstream.

####How to undo "git commit --amend"?
Move the current head so that it's pointing at the old commit. Leave the index intact for redoing the commit

	$ git reset --soft HEAD@{1}
	
commit the current tree using the commit details of the previous HEAD commit. 

(Note that HEAD@{1} is pointing somewhere different from the previous command. It's now pointing at the erroneously amended commit.)

	$ git commit -C HEAD@{1}
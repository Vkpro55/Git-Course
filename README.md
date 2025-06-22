# Git & GitHub Course

These commands **identify who you are** when you make Git commits and become part of every commit’s metadata - 

```
git config --global user.name "Vinod Kumar"
git config --global user.email "vinod@gmail.com"
```
So to create new file in git bash - 

```
nano f1.txt /*== creates new file ==*/ 
ctrl + X /*== Save the file ==*/
Yes
Enter /*== Move out of the nano editor ==*/
```
To track the file locally on the system - 

```
git intit /*== Initializes a new Git repository in your current directory ==*/
```
 If you run this command in wrong folder -

```
rm -rf .git /*== Delete the .git folder ==*/
```
Git will not automatically tracks the file in the current directory, you need to tell them manually to what files do you want to track. By executing following command you will check the files which git not aware about and it allow fine control to review your changes before commit.

```
git status /*== Show current status - commits, tracked file, untracked file ==*/
git add filename /*== Git will aware about your file and it's content. It brings the file from non-stagin area to stagin area. ==*/ 
```
To unstage the file you don't want to track -

```
git rm --cached filename
```
To track the file in the git repository -

```
git commit 
```
To check whether the files are tracked or not you can see commit history -

```
git log
```
The default branch that will created when you do git init is -

```
master
```
To initialize with another branch - 

```
git init --initial-branch=main
```
> Note: Remember this when you makes your first commit then only branch will creates.

To see the permission of the file or directory -

```
drwxr-xr-x
│││ │ │ │
│││ │ │ └── Others: execute (x)
│││ │ └──── Others: read (r)
│││ └────── Group: execute (x)
││└──────── Group: read (r)
│└───────── Owner: write (w)
└────────── Directory (d)
```
Git will never track the empty folder. And to see the all files that tracked or not inside folder -

```
git status --untracked=all
```
To see detailed ans sort info about files tracked or not tracked - 

```
git status -v /*== Verbose : detailed info ==*/
git status -s /*== Sort : sort info ==*/
```
> Note : Avoid adding all the files in the stagin area, double check it and add only those files with no code error or compilation error.

If you modifies the already tracked file, you can directly commit them from NSA -

```
git commit -a -m "Modified : f2.txt"
```
If you want to do changes in already existed commit - 

```
git add . /*== Put the new changes in statging area ==*/
git commit --amend
git commit --amend --no-edit /*== If dont want to change commit msg ==*/
```
To signed-off the commit that signifies that commit comes from the person who owns who they are - 

```
git commit -s -m "msg"
```
To create a empty commit - 

```
git commit --allow-empty -m "msg"
```
"An empty commit is a trick to get Netlify/Vercel to rebuild and redeploy your site — without needing to modify your actual code."

To see latest n=2 commits not all - 

```
git log -n 2
```
To see all the commits id only without author info -

```
git log --pretty=oneline
```
To see the detailed about commit what change made during that commit -

```
git log -p
```
To see the commits from particular time - 

```
git log --since="1 week ago"
git log --since="2025-06-20" --until="2025-06-22"
git log --author="Vinod" /*== Only shows the commits made by Vinod ==*/
```
Git commit important commnads - 

```
git reset --soft 674dab3e6bc22a8c6f167bc3ca30e3930882e288 
/*== This command will put all the changes in the staging area after 
this commit_id mentioned in the command 
Note : it will not delete the changes you made after this commit_id ==*/
```
This shows the changes that are staged (i.e., added with `git add`) and ready to be committed, compared to the previous commit - 

```
git diff --staged
```
```
git reset --mixed 674dab3e6bc22a8c6f167bc3ca30e3930882e288
/*== This will brings the changes in Non-statging area : it will not
delete the changes ==*/
```
```
git reset --hard 674dab3e6bc22a8c6f167bc3ca30e3930882e288
/*== It will delete all the changes after this commit_id, also your 
working tree remain clean ==*/
```
This commit undoes a specific commit by creating a new commit that reverses the changes made by the original one — without modifying history -

```
git revert commit_id /*== Creates the new commit that undo the changes ==*/
git checkout commit_id /*== You can see the content at this commit ==*/
git checkout master
```
To see all the local branches -

```
git branch
```
To create a new local branch, it will take current branch head as the reference -

```
git branch branch_name
```
To go to already created branch

```
git checkout branch_name /*== If branch is not present that give you error ==*/
```
To delete a branch -

```
git branch -d branch_name
```
To get the changes of the branches that not in the current branch -

```
git checkout master 
git merge feature01 /*== master branch want the commits that present in 
master branch as compared to feature01 branch ==*/
```
If you want to merge changes of specif commit only - 

```
/* == branched - master , f1 ==*/
f1-c1 = erii899...
f1-c2 = hghuhio...
f1-c3 = hujkk79...

git switch master
git cherry-pick hghuhio
/*== Only changed happened from f1-c1 to f1-c2 are merged in master ==*/
```
To push into the remote repository -

```
git push -u origin master
/*== It will create a new master branch at the remote url and push changes
inside that==*/
```
To see all the remote branches -

```
git branch -r
```
> Note: Remember this origin/master is the last updated state of the remote branch. 
master → your local branch
origin/master → points to GitHub’s state _at the time of cloning_

Until you run `git fetch` or `git pull`, your local `origin/master` still points to the old commit — it does not automatically update.

So, whenever there is new changed `﻿git fetch` will downloaded those commits into your local remote branch. Ex- local orogin/master -> sync with remote master branch.

```
git switch master
git fetch 
/*== It will brings all the changes or latest update from remote master
branch to remote tracking branch -> origin/master ==*/
```
If the remote branch is deleted then there si no sense to have remote tracking branch for that -

```
/*== In the remote repo you delete this branch : feature01-v3 ==*/

/*== But when you do in the local system ==*/
git branch -r 
 - origin/master
 - origin/feature01-v1
 - origin/feature01-v2
 - origin/feature01-v3 -> no way you are tracking this branch

/*== Run this command : it will automatically delete the remote tracking branch 
if the remote repo doesn't have that branch ==*/
git fetch --prune
 
```
Rather than doing `﻿git pull`  always do `﻿git pull origin master`  -

```
git fetch 
/*== Fetch the changes or updates of all the remote branches to you local 
remote tracking branched : that I don't need. My concern with specific 
branch only which will I need to updated. ==*/

git fetch origin master
/*== Now I'm only say if there is changes in remote master that please
download those changed to remote tracking branch origin/master. I don't
care about the other branches. ==*/
```
So let's say you are working on current branch and you modified or create new chnanges and in the meantime you have to go to other branch and do development. Git will not allow this - i) do stash ii) do commit.

So changes about you are not confident that this is incomplete and you don't have to commit them. Instead use `﻿git stash` to put this temporarily chnages in safe place.

```
git stash list /*== List of all the stash ==*/
git stash apply stash@{0} /*== Now start work on temporarily changes ==*/
```



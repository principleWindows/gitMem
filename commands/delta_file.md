# Understanding delta file changes and merge conflicts in Git pull requests

<https://devblogs.microsoft.com/devops/understanding-delta-file-changes-and-merge-conflicts-in-git-pull-requests/>

*******************

## Index

1.  [Delta file changes for a Git pull request](#delta-file-changes-for-a-git-pull-request) \
    [1.1 How to get the source branch and the target branch](#how-to-get-the-source-branch-and-the-target-branch)
2.  [Merge conflicts in Git pull requests](#merge-conflicts-in-git-pull-requests)


## Preface

A while ago I worked on a support request with a user reporting unexpected behavior 
from Git when completing a big and long-living pull request using 
[Azure Repos](https://azure.microsoft.com/en-us/products/devops/repos/). This pull 
request had known conflicts but also some missing changes on files and paths where 
there were no merge conflicts detected at all. This made me think Git was indeed, 
as user was reporting, ignoring some changes on its own. Long story short, it was not.

Let’s dig into this and hopefully help anyone using Git to understand the key processes 
of a Git pull request and the whys of the resulting changes of the merge operation 
to happen at the end of it.

[Back to index](#index)


## 1 Delta file changes for a Git pull request

The changes to be applied at completion of a pull request are the result of merging 
the head of the source branch against the head of the target branch. To refer to these 
changes we use the term delta file changes (Δchanges). The method Git uses to determine 
these changes is by comparing the heads of both branches from the merge-base commit.

![](pix/merge-base-fullres.png)

Any commit before the merge-base commit will not be considered because it is part of 
both branches. When the source branch has grown so big that it is difficult to find 
the merge-base commit in the history you can run:
```batch
git merge-base refs/heads/master refs/heads/dev
```

For this example, the target branch is named *master* and the source branch is named *dev*. 
The result of this command will be the `SHA` value for the merge-base commit.

This will allow you to identify which is the merge-base commit. All the commits made on 
the source branch after the merge-base commit will be considered as Δchanges. These are 
the commits that will be listed in the commits tab for your pull request.



[Back to index](#index)


### 1.1 How to get the source branch and the target branch

First we clone the source branch from the remote repo.
```batch
git clone https://gitee.com/principlewin/win-principle-2022.git
```

Using the following command to create a new branch and checkout to this new branch:
```batch
git checkout -b <new-branch> [<start-point>]
```

Specifying `-b` causes a new branch to be created as if git-branch were called and then 
checked out. In this case you can use the `--track` or `--no-track` options, which will 
be passed to git branch. As a convenience, `--track` without `-b` implies branch 
creation.

Now pull the target remote branch to the new-branch created above.
```batch
git pull https://gitee.com/someone/targetRepo.git master
```

[Back to index](#index)


## 2 Merge conflicts in Git pull requests

There will be conflicts in the pull request when both the source branch and the target 
branch contain matching changes after the merge-base commit. This means both branches 
grew in parallel after the source branch was cut-off from the target branch and at some 
point, both branches made changes to the same file.

Git is especially good at tracking changes for text/code files. If the file is not a 
text/code file (such as images, videos etc), then Git will consider any change as a new 
version of the file.

![](pix/merge-conflicts-fullres.png)

In this diagram we show an example of a merge conflict, both branches received a commit 
on the file abstracted in the shape of a square. If we attempt to merge these branches 
Git won’t know which version of the file you intend to keep as final; we call these 
competing files.

For competing files you’ll have to mimic a sync between the branches by committing the 
version you want to keep on either branch. Git makes this easy by adding some conflict 
markers to the lines of the file in both branches after the conflict has been detected, see 
[Resolving a merge conflict using the command line](https://help.github.com/en/articles/resolving-a-merge-conflict-using-the-command-line).

[Back to index](#index)


## 3 Git ignoring file changes after a pull request completion with no conflicts

Remember we said Git would determine which changes to apply based on the merge-base 
commit? Let’s elaborate a more complicated scenario to demonstrate this.

![](pix/unexpected-fullres.png)

Which is the final version for file abstracted as a square?

In this example a user modified the file in the source branch and then rolled it back 
to the way it was at the merge-base commit expecting Git to set this version as the 
final one for the merge operation.

However, Git compared the version of the file from the merge-base commit against the 
HEAD of the source branch and determined there were no changes on it and therefore 
it ignored it. At the same time the target branch received a change on the same file 
and since there was no input on this file from Git on the source branch, it remained 
untouched and with no conflicts after the merge operation was completed. Keep in mind 
this behavior applies not only at a file level but at a line level for text/code files.

From the perspective of a support engineer, my suggestion to developers experiencing 
unexpected results from a merge operation is to identify the head of the source branch 
at the moment of a pull request completion and compare it to the merge-base commit by 
running the git merge-base command. After all this being said we can narrow down the 
possible scenarios to merge conflicts and unexpected resulting changes applied.

[Back to index](#index)






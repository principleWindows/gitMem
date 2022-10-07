# How to Create and Apply a Patch in Git

- [How to Create and Apply a Patch in Git](https://www.git-tower.com/learn/git/faq/create-and-apply-patch)
- [定位和解决git am冲突的方法](https://blog.csdn.net/Qidi_Huang/article/details/61920472)

************************************

Patches are an alternative way to exchange code changes. Although today - 
with the widespread use of remote repositories, forks, and Pull Requests - 
exchanging code via patches isn't very common anymore, it can be a valuable 
tool in special situations.

By creating a patch, you can essentially "export" one or more commits into 
plain text files, which you can then easily send to someone else for 
integration.

In this article, we'll look at how to both create and apply patches.


## Index

1. [Using git format-patch to Create a Patch](#using-git-format-patch-to-create-a-patch)
2. [Using git am to Apply a Patch](#using-git-am-to-apply-a-patch)
3. [How to resolve merge conflicts in git am](#fixing-git-am-conflicts)
4. [References](#refs)


## 1 Using git format-patch to Create a Patch

To create a patch, we will use the git format-patch command. Most 
importantly, we must tell Git which commits exactly we want to be 
included in the patch. Let's take the following scenario as an example:

- we are currently on a bugfix branch named "bugfix/broken-navigation"
- we had based the branch on our local "master" branch
- after some work, we have created two new commits on the bugfix branch
- we now want to create a patch that contains these two new commits so we 
can send them to a colleague that wants to integrate them

We can achieve this with the following commands:
```batch
# Switch to the base branch that is missing the new changes
git checkout master

# Create patch files for all new commits in our bugfix branch
git format-patch bugfix/broken-navigation
```

The git format-patch command will include all of the commits that are 
contained in the specified branch ("bugfix/broken-navigation"), but not 
in the currently checked out branch ("master").

This will leave us with two patch files, which contents look approximately 
like this:
```batch
From 7173808e55679215179217cec8aac1ca0a213bb5 Mon Sep 17 00:00:00 2001
From: example 
Date: Tue, 7 July 2020 10:05:28 +0200
Subject: [PATCH 2/2] Change page structure

---
 about.html   | 2 +-
 index.html   | 4 ++--
 product.html | 0
 3 files changed, 3 insertions(+), 3 deletions(-)
 create mode 100644 product.html

diff --git a/about.html b/about.html
index 0c20c33..ee7cc3d 100644
--- a/about.html
+++ b/about.html
@@ -13,7 +13,7 @@
       <div id="navigation">
         <ul>
           <li><a href="index.html">Home</a></li>
-          <li><a href="about.html">About</a></li>
+          <li><a href="about.html">About Us</a></li>
           <li><a href="imprint.html">Imprint</a></li>
         </ul>
       </div>
```

In case you'd prefer to have just a single file containing all of the 
commits, you can use the --stdout option:
```batch
git format-patch bugfix/broken-navigation --stdout > bugfix.patch
```

In any case, you'll be left with one or multiple .patch files which you 
can send to a colleague for review and integration.


[Back to index](#index)


## 2 Using git am to Apply a Patch

The receiver of the patch file(s) can then apply the changes using the git am command:
```batch
# Switch to the branch where the changes should be applied
git checkout master

# Apply the patch
git am bugfix.patch

# Check what has happened in the commit log
git log
```

In the commit history, you should now find that the new commit(s) have been 
added!


[Back to index](#index)


## 3 Fixing git am conflicts

伴随着主线代码的不断更新，我们在早期保存出来 的patch 中有部分内容可能已经不能再直接
打入现在的代码里了。这种情况下可以使用下面的方法解决冲突：

1、执行命令 `git am xxxx.patch` 尝试直接打入补丁。因为我们使用的 patch 已经过时了，
所以这一步肯定会报错并中断（注意，虽然命令停止执行了，但我们依然处于 git am 
命令的运行环境中，可以通过git status命令查看到当前的状态）。
此时应该执行 `git am --abort` 来放弃当期打补丁操作。

2、执行命令 git apply --reject xxxx.patch 自动合入 patch 中不冲突的代码改动，
同时保留冲突的部分。这些存在冲突的改动内容会被单独存储到目标源文件的相应目录下，
以后缀为 .rej 的文件进行保存。比如对 ./test/someDeviceDriver.c 文件中的某些行
合入代码改动失败，则会将这些发生冲突的行数及内容都保存在 
./test/someDeviceDriver.c.rej 文件中。我们可以在执行 git am 命令的目录下执行 
find -name *.rej 命令以查看所有存在冲突的源文件位置。

3、依据 步骤2 中生成的 *.rej 文件内容逐个手动解决冲突，然后删除这些 *.rej 文件。
完成这一步骤的操作后，我们就可以继续执行 git am 的过程了。

4、执行命令 git status 查看当前改动过的以及新增的文件，确保没有多添加或少添加文件。

5、执行命令 git add . 将所有改动都添加到暂存区（注意，关键字add后有一个小数点 . 
作为参数，表示当前路径）。

6、执行命令 git am --resolved 继续步骤 1 中被中断的 patch 合入操作。合入完成后，
会有提示信息输出。

7、执行命令 git log 确认合入状态。

至此，带有冲突代码的 patch 合入就操作完成了。如果要修改 commit 信息，执行 git 
commit --amend 命令即可。


[Back to index](#index)


## refs

- Check out the official documentation for 
[git format-patch](https://git-scm.com/docs/git-format-patch) 
and 
[git am](https://git-scm.com/docs/git-am)
- More 
[frequently asked questions](https://www.git-tower.com/learn/git/faq)
about Git & version control
- [《Git am 合并 patch 时的冲突处理》](http://blog.csdn.net/chaihuasong/article/details/50517519)


[Back to index](#index)

# How to Create and Apply a Patch in Git

- [How to Create and Apply a Patch in Git](https://www.git-tower.com/learn/git/faq/create-and-apply-patch)
- [��λ�ͽ��git am��ͻ�ķ���](https://blog.csdn.net/Qidi_Huang/article/details/61920472)

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

���������ߴ���Ĳ��ϸ��£����������ڱ������ ��patch ���в������ݿ����Ѿ�������ֱ��
�������ڵĴ������ˡ���������¿���ʹ������ķ��������ͻ��

1��ִ������ `git am xxxx.patch` ����ֱ�Ӵ��벹������Ϊ����ʹ�õ� patch �Ѿ���ʱ�ˣ�
������һ���϶��ᱨ���жϣ�ע�⣬��Ȼ����ִֹͣ���ˣ���������Ȼ���� git am 
��������л����У�����ͨ��git status����鿴����ǰ��״̬����
��ʱӦ��ִ�� `git am --abort` ���������ڴ򲹶�������

2��ִ������ git apply --reject xxxx.patch �Զ����� patch �в���ͻ�Ĵ���Ķ���
ͬʱ������ͻ�Ĳ��֡���Щ���ڳ�ͻ�ĸĶ����ݻᱻ�����洢��Ŀ��Դ�ļ�����ӦĿ¼�£�
�Ժ�׺Ϊ .rej ���ļ����б��档����� ./test/someDeviceDriver.c �ļ��е�ĳЩ��
�������Ķ�ʧ�ܣ���Ὣ��Щ������ͻ�����������ݶ������� 
./test/someDeviceDriver.c.rej �ļ��С����ǿ�����ִ�� git am �����Ŀ¼��ִ�� 
find -name *.rej �����Բ鿴���д��ڳ�ͻ��Դ�ļ�λ�á�

3������ ����2 �����ɵ� *.rej �ļ���������ֶ������ͻ��Ȼ��ɾ����Щ *.rej �ļ���
�����һ����Ĳ��������ǾͿ��Լ���ִ�� git am �Ĺ����ˡ�

4��ִ������ git status �鿴��ǰ�Ķ������Լ��������ļ���ȷ��û�ж���ӻ�������ļ���

5��ִ������ git add . �����иĶ�����ӵ��ݴ�����ע�⣬�ؼ���add����һ��С���� . 
��Ϊ��������ʾ��ǰ·������

6��ִ������ git am --resolved �������� 1 �б��жϵ� patch ���������������ɺ�
������ʾ��Ϣ�����

7��ִ������ git log ȷ�Ϻ���״̬��

���ˣ����г�ͻ����� patch ����Ͳ�������ˡ����Ҫ�޸� commit ��Ϣ��ִ�� git 
commit --amend ����ɡ�


[Back to index](#index)


## refs

- Check out the official documentation for 
[git format-patch](https://git-scm.com/docs/git-format-patch) 
and 
[git am](https://git-scm.com/docs/git-am)
- More 
[frequently asked questions](https://www.git-tower.com/learn/git/faq)
about Git & version control
- [��Git am �ϲ� patch ʱ�ĳ�ͻ����](http://blog.csdn.net/chaihuasong/article/details/50517519)


[Back to index](#index)

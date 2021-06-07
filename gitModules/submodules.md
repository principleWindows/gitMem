# ��ģ��

[7.11 Git ���� - ��ģ��](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97)

***************************

����������Ǿ�����������ĳ�������е���Ŀ��Ҫ������ʹ����һ����Ŀ�� Ҳ���ǵ������⣬��������������ģ�
���ڶ������Ŀ�Ŀ⡣ �����������ˣ�����Ҫ�����ǵ���������������Ŀ��ͬʱ������һ����Ŀ��ʹ����һ����

���Ǿ�һ�����ӡ� ���������ڿ���һ����վȻ�󴴽��� Atom ���ġ� �����ʹ��һ���⣬������д�Լ��� Atom 
���ɴ��롣 ����ܲ��ò�ͨ�� CPAN ��װ�� Ruby gem ������������еĴ��룬
���߽�Դ����ֱ�ӿ������Լ�����Ŀ�С� ���������������������ô�����ú��ַ�ʽ�����Ѷ�������
������������ѣ���Ϊ�����ȷ��ÿһ���ͻ��˶������ÿ⡣ ��������븴�Ƶ��Լ�����Ŀ�У�
��ô�������κ��Զ����޸Ķ���ʹ�ϲ����εĸĶ�������ѡ�

Git ͨ����ģ�������������⡣ ��ģ�������㽫һ�� Git �ֿ���Ϊ��һ�� Git �ֿ����Ŀ¼�� 
�������㽫��һ���ֿ��¡���Լ�����Ŀ�У�ͬʱ�������ύ�Ķ�����

## 1 ��ʼʹ����ģ��

���ǽ�Ҫ��ʾ�����һ�����ֳ�һ������Ŀ�뼸������Ŀ����Ŀ�Ͽ�����

�������Ƚ�һ���Ѵ��ڵ� Git �ֿ����Ϊ���ڹ����Ĳֿ����ģ�顣 �����ͨ���� git submodule add 
������������Ҫ���ٵ���Ŀ����Ի���� URL ������µ���ģ�顣 �ڱ����У�
���ǽ������һ����Ϊ ��DbConnector�� �Ŀ⡣

```shell
$ git submodule add https://github.com/chaconinc/DbConnector
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
```

Ĭ������£���ģ��Ὣ����Ŀ�ŵ�һ����ֿ�ͬ����Ŀ¼�У��������� ��DbConnector���� 
�������Ҫ�ŵ������ط�����ô�����������β���һ����ͬ��·����

�����ʱ���� git status�����ע�⵽�����¡�

```shell
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   .gitmodules
	new file:   DbConnector
```
����Ӧ��ע�⵽�µ� .gitmodules �ļ��� �������ļ���������Ŀ URL ���Ѿ���ȡ�ı���Ŀ¼֮���ӳ�䣺

[submodule "DbConnector"]
	path = DbConnector
	url = https://github.com/chaconinc/DbConnector
����ж����ģ�飬���ļ��оͻ��ж�����¼�� Ҫ�ص�ע����ǣ����ļ�Ҳ�� .gitignore 
�ļ�һ���ܵ���ͨ�����汾���ơ� ����͸���Ŀ����������һͬ����ȡ���͡� 
����ǿ�¡����Ŀ����֪��ȥ�Ļ����ģ���ԭ��

> **Note**
>
> ���� .gitmodules �ļ��е� URL ���������ȳ��Կ�¡/��ȡ�ĵط�������뾡����ȷ����ʹ�õ� URL 
> ��Ҷ��ܷ��ʡ� ���磬����Ҫʹ�õ����� URL �����˵���ȡ URL ��ͬ����ô��ʹ�������ܷ��ʵ��� URL�� 
> ��Ҳ���Ը����Լ�����Ҫ��ͨ���ڱ���ִ�� git config submodule.DbConnector.url <˽��URL> 
> ���������ѡ���ֵ�� ������еĻ���һ�����·������а�����

�� git status ������г�����һ������Ŀ�ļ��м�¼�� ��������� git diff���ῴ�������������Ϣ��

```shell
$ git diff --cached DbConnector
diff --git a/DbConnector b/DbConnector
new file mode 160000
index 0000000..c3f01dc
--- /dev/null
+++ b/DbConnector
@@ -0,0 +1 @@
+Subproject commit c3f01dc8862123d317dd46284b05b6892c7b29bc
```
��Ȼ DbConnector �ǹ���Ŀ¼�е�һ����Ŀ¼���� Git ���ǻὫ������һ����ģ�顣���㲻���Ǹ�Ŀ¼��ʱ��
Git ����������������ݣ� ���ǽ���������ģ��ֿ��е�ĳ��������ύ��

������뿴����Ư���Ĳ�����������Ը� git diff ���� --submodule ѡ�

```shell
$ git diff --cached --submodule
diff --git a/.gitmodules b/.gitmodules
new file mode 100644
index 0000000..71fc376
--- /dev/null
+++ b/.gitmodules
@@ -0,0 +1,3 @@
+[submodule "DbConnector"]
+       path = DbConnector
+       url = https://github.com/chaconinc/DbConnector
Submodule DbConnector 0000000...c3f01dc (new submodule)
```
�����ύʱ���ῴ�������������Ϣ��

```shell
$ git commit -am 'added DbConnector module'
[master fb9093c] added DbConnector module
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 DbConnector
```
ע�� DbConnector ��¼�� 160000 ģʽ�� ���� Git �е�һ������ģʽ��
����������ζ�����ǽ�һ���ύ����һ��Ŀ¼��¼�ģ����ǽ�����¼��һ����Ŀ¼����һ���ļ���

���������Щ���ģ�

```shell
$ git push origin master
```

## 2 ��¡������ģ�����Ŀ

���������ǽ����¡һ��������ģ�����Ŀ�� �����ڿ�¡��������Ŀʱ��Ĭ�ϻ��������ģ��Ŀ¼�������л�û���κ��ļ���

```shell
$ git clone https://github.com/chaconinc/MainProject
Cloning into 'MainProject'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 1), reused 13 (delta 0)
Unpacking objects: 100% (14/14), done.
Checking connectivity... done.
$ cd MainProject
$ ls -la
total 16
drwxr-xr-x   9 schacon  staff  306 Sep 17 15:21 .
drwxr-xr-x   7 schacon  staff  238 Sep 17 15:21 ..
drwxr-xr-x  13 schacon  staff  442 Sep 17 15:21 .git
-rw-r--r--   1 schacon  staff   92 Sep 17 15:21 .gitmodules
drwxr-xr-x   2 schacon  staff   68 Sep 17 15:21 DbConnector
-rw-r--r--   1 schacon  staff  756 Sep 17 15:21 Makefile
drwxr-xr-x   3 schacon  staff  102 Sep 17 15:21 includes
drwxr-xr-x   4 schacon  staff  136 Sep 17 15:21 scripts
drwxr-xr-x   4 schacon  staff  136 Sep 17 15:21 src
$ cd DbConnector/
$ ls
$
```

������ DbConnector Ŀ¼�������ǿյġ� ����������������git submodule init ������ʼ�����������ļ����� git submodule update ��Ӹ���Ŀ��ץȡ�������ݲ��������Ŀ���г��ĺ��ʵ��ύ��

```shell
$ git submodule init
Submodule 'DbConnector' (https://github.com/chaconinc/DbConnector) registered for path 'DbConnector'
$ git submodule update
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
Submodule path 'DbConnector': checked out 'c3f01dc8862123d317dd46284b05b6892c7b29bc'
```
���� DbConnector ��Ŀ¼�Ǵ��ں�֮ǰ�ύʱ��ͬ��״̬�ˡ�

�������и���һ��ķ�ʽ�� ����� git clone ����� --recurse-submodules ѡ�
���ͻ��Զ���ʼ�������²ֿ��е�ÿһ����ģ�飬 �������ܴ��ڵ�Ƕ����ģ�顣

```shell
$ git clone --recurse-submodules https://github.com/chaconinc/MainProject
Cloning into 'MainProject'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 1), reused 13 (delta 0)
Unpacking objects: 100% (14/14), done.
Checking connectivity... done.
Submodule 'DbConnector' (https://github.com/chaconinc/DbConnector) registered for path 'DbConnector'
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
Submodule path 'DbConnector': checked out 'c3f01dc8862123d317dd46284b05b6892c7b29bc'
```
������Ѿ���¡����Ŀ�������� --recurse-submodules����ô�������� git submodule update --init 
�� git submodule init �� git submodule update �ϲ���һ���������Ҫ��ʼ����ץȡ������κ�Ƕ�׵���ģ�飬 
��ʹ�ü����� git submodule update --init --recursive��


## 3 �ڰ�����ģ�����Ŀ�Ϲ���

����������һ�ݰ�����ģ�����Ŀ���������ǽ���ͬʱ������Ŀ����ģ����Ŀ�����Ŷӳ�ԱЭ����

### 3.1 ����ģ���Զ����ȡ�����޸�

����Ŀ��ʹ����ģ������ģ�ͣ�����ֻʹ������Ŀ����ʱ�ػ�ȡ���£�����������ļ���н����κθ��ġ�
��������һ���򵥵����ӡ�

�����Ҫ����ģ���в鿴�¹��������Խ��뵽Ŀ¼������ git fetch �� git merge���ϲ����η�֧�����±��ش��롣

```shell
$ git fetch
From https://github.com/chaconinc/DbConnector
   c3f01dc..d0354fc  master     -> origin/master
$ git merge origin/master
Updating c3f01dc..d0354fc
Fast-forward
 scripts/connect.sh | 1 +
 src/db.c           | 1 +
 2 files changed, 2 insertions(+)
```
��������ڷ��ص�����Ŀ������ git diff --submodule���ͻῴ����ģ�鱻���µ�ͬʱ�����һ������������ύ���б�
����㲻��ÿ������ git diff ʱ������ --submodle����ô���Խ� diff.submodule 
����Ϊ ��log�� ��������ΪĬ����Ϊ��

```shell
$ git config --global diff.submodule log
$ git diff
Submodule DbConnector c3f01dc..d0354fc:
  > more efficient db routine
  > better connection routine
```
����ڴ�ʱ�ύ����ô��Ὣ��ģ������Ϊ�����˸���ʱ���´��롣

����㲻������Ŀ¼���ֶ�ץȡ��ϲ�����ô�����ָ����׵ķ�ʽ�� ���� git submodule update --remote��
Git ���������ģ��Ȼ��ץȡ�����¡�

```shell
$ git submodule update --remote DbConnector
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 2), reused 4 (delta 2)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   3f19983..d0354fc  master     -> origin/master
Submodule path 'DbConnector': checked out 'd0354fc054692d3906c85c3af05ddce39a1c0644'
```

������Ĭ�ϻ�ٶ�����Ҫ���²������ģ��ֿ�� master ��֧�� ������Ҳ��������Ϊ��Ҫ��������֧�� 
���磬����Ҫ DbConnector ��ģ����ٲֿ�� ��stable�� ��֧����ô�ȿ����� .gitmodules 
�ļ������ã�����������Ҳ���Ը���������Ҳ����ֻ�ڱ��ص� .git/config �ļ������á� 
�������� .gitmodules �ļ�����������

```shell
$ git config -f .gitmodules submodule.DbConnector.branch stable

$ git submodule update --remote
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 2), reused 4 (delta 2)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   27cf5d3..c87d55d  stable -> origin/stable
Submodule path 'DbConnector': checked out 'c87d55d4c6d4b05ee34fbc8cb6f7bf4585ae6687'
```
������� `-f .gitmodules` ѡ���ô��ֻ��Ϊ�����޸ġ������ڲֿ��б���������Ϣ��������һЩ��
��Ϊ������Ҳ���Եõ�ͬ����Ч����

��ʱ�������� `git status`��Git ����ʾ��ģ�����С����ύ����

```shell
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   .gitmodules
  modified:   DbConnector (new commits)

no changes added to commit (use "git add" and/or "git commit -a")
```
���������������ѡ�� status.submodulesummary��Git Ҳ����ʾ�����ģ��ĸ���ժҪ��

```shell
$ git config status.submodulesummary 1

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   .gitmodules
	modified:   DbConnector (new commits)

Submodules changed but not updated:

* DbConnector c3f01dc...c87d55d (4):
  > catch non-null terminated lines
```
��ʱ������� `git diff`�����Կ��������޸��� .gitmodules �ļ���
ͬʱ���м�������ȡ���ύ��Ҫ�ύ�������Լ�����ģ����Ŀ�С�

```shell
$ git diff
diff --git a/.gitmodules b/.gitmodules
index 6fc0b3d..fd1cc29 100644
--- a/.gitmodules
+++ b/.gitmodules
@@ -1,3 +1,4 @@
 [submodule "DbConnector"]
        path = DbConnector
        url = https://github.com/chaconinc/DbConnector
+       branch = stable
 Submodule DbConnector c3f01dc..c87d55d:
  > catch non-null terminated lines
  > more robust error handling
  > more efficient db routine
  > better connection routine
```
��ǳ���Ȥ����Ϊ���ǿ���ֱ�ӿ�����Ҫ�ύ����ģ���е��ύ��־�� �ύ֮��
��Ҳ�������� `git log -p` �鿴�����Ϣ��

```shell
$ git log -p --submodule
commit 0a24cfc121a8a3c118e0105ae4ae4c00281cf7ae
Author: Scott Chacon <schacon@gmail.com>
Date:   Wed Sep 17 16:37:02 2014 +0200

    updating DbConnector for bug fixes

diff --git a/.gitmodules b/.gitmodules
index 6fc0b3d..fd1cc29 100644
--- a/.gitmodules
+++ b/.gitmodules
@@ -1,3 +1,4 @@
 [submodule "DbConnector"]
        path = DbConnector
        url = https://github.com/chaconinc/DbConnector
+       branch = stable
Submodule DbConnector c3f01dc..c87d55d:
  > catch non-null terminated lines
  > more robust error handling
  > more efficient db routine
  > better connection routine
```
������ `git submodule update --remote` ʱ��Git Ĭ�ϻ᳢�Ը���**����**��ģ�飬
��������кܶ���ģ��Ļ�������Դ�����Ҫ���µ���ģ������֡�

### 3.2 ����ĿԶ����ȡ���θ���

���ڣ�������վ��Э���ߵ��ӽǣ������Լ��� MainProject �ֿ�ı��ؿ�¡�� ֻ��ִ�� git pull ��ȡ�����ύ�ĸ��Ļ�������

```shell
$ git pull
From https://github.com/chaconinc/MainProject
   fb9093c..0a24cfc  master     -> origin/master
Fetching submodule DbConnector
From https://github.com/chaconinc/DbConnector
   c3f01dc..c87d55d  stable     -> origin/stable
Updating fb9093c..0a24cfc
Fast-forward
 .gitmodules         | 2 +-
 DbConnector         | 2 +-
 2 files changed, 2 insertions(+), 2 deletions(-)

$ git status
 On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   DbConnector (new commits)

Submodules changed but not updated:

* DbConnector c87d55d...c3f01dc (4):
  < catch non-null terminated lines
  < more robust error handling
  < more efficient db routine
  < better connection routine

no changes added to commit (use "git add" and/or "git commit -a")
```
Ĭ������£�`git pull`�����ݹ��ץȡ��ģ��ĸ��ģ��������һ������������ʾ��
Ȼ����������**����**��ģ�顣����ͨ�� `git status` �������������ʾ��ģ�顰���޸ġ����ҡ����µ��ύ���� 
���⣬��ߵļ����ţ�<��ָ�����µ��ύ����ʾ��Щ�ύ���� MainProject �м�¼��
����δ�ڱ��ص� `DbConnector` �м���� Ϊ����ɸ��£�����Ҫ���� `git submodule update`��

```shell
$ git submodule update --init --recursive
Submodule path 'vendor/plugins/demo': checked out '48679c6302815f6c76f1fe30625d795d9e55fc56'

$ git status
 On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```

��ע�⣬Ϊ��ȫ�������� MainProject �ύ�������ȡ������ģ�飬��ôӦ���� `git submodule update` 
������� `--init` ѡ������ģ����Ƕ�׵���ģ�飬��Ӧʹ�� `--recursive` ѡ�

��������Զ����˹��̣���ô����Ϊ `git pull` ������� `--recurse-submodules` ѡ��� Git 2.14 ��ʼ����
����� Git ����ȡ������ `git submodule update`������ģ����Ϊ��ȷ��״̬�� ���⣬��������� Git ������ 
`--recurse-submodules` ��ȡ�����Խ�����ѡ�� `submodule.recurse` ����Ϊ `true`���� Git 2.15 
��ʼ������ `git pull`������ѡ����� Git Ϊ����֧�� `--recurse-submodules`
������ʹ�ø�ѡ��� `clone` ���⣩��

��Ϊ������Ŀ��ȡ����ʱ���������һ������������������ȡ���ύ�У� ���� `.gitmodules` 
�ļ��м�¼����ģ��� URL �����˸ı䡣 ���磬����ģ����Ŀ�ı��������й�ƽ̨���ͻᷢ����������� 
��ʱ����������Ŀ���õ���ģ���ύ���ڲֿ��б������õ���ģ��Զ���ϣ���ôִ�� 
`git pull --recurse-submodules` �� `git submodule update` �ͻ�ʧ�ܡ� Ϊ�˲��ȣ�
`git submodule sync` ������Ҫ��

```shell
# ���µ� URL ���Ƶ�����������
$ git submodule sync --recursive
# ���� URL ������ģ��
$ git submodule update --init --recursive
```

### 3.3 ����ģ���Ϲ���

����п�������ʹ����ģ�飬��Ϊ��ȷʵ������ģ���б�д�����ͬʱ������������Ŀ�ϱ�д���루���߿���ģ�鹤������
��������ֻ���ü򵥵���������ϵͳ���� Maven �� Rubygems��������ˡ�

�������ǽ�ͨ��һ����������ʾ�������ģ��������Ŀ��ͬʱ���޸ģ��Լ����ͬʱ�ύ�뷢����Щ�޸ġ�

��ĿǰΪֹ������������ `git submodule update` ����ģ��ֿ���ץȡ�޸�ʱ��Git 
��������Щ�Ķ���������Ŀ¼�е��ļ������ǻὫ�Ӳֿ�����һ������������� HEAD����״̬��
����ζ��û�б��ع�����֧������ ��master�� �����ٸĶ��� ���û�й�����֧���ٸ��ģ�
Ҳ����ζ�ż����㽫�����ύ������ģ�飬��Щ����Ҳ�ܿ��ܻ����´�����  `git submodule update` 
ʱ��ʧ���������Ҫ����ģ���и�����Щ�޸ģ�����ҪһЩ����Ĳ��衣

Ϊ�˽���ģ�����õø����׽��벢�޸ģ�����Ҫ�������¡� ���ȣ�����ÿ����ģ�鲢�������Ӧ�Ĺ�����֧�� 
���ţ��������˸��ľ���Ҫ���� Git ������ʲô��Ȼ������ `git submodule update --remote` 
����������ȡ�¹����� �����ѡ�����Ǻϲ�����ı��ع����У�Ҳ���Գ��Խ���Ĺ���������µĸ����ϡ�

���ȣ������ǽ�����ģ��Ŀ¼Ȼ����һ����֧��

```shell
$ cd DbConnector/
$ git checkout stable
Switched to branch 'stable'
```

Ȼ������ ��merge�� ѡ����������ģ�顣 Ϊ���ֶ�ָ����������ֻ��� `update` ��� `--merge` ѡ��ɡ�
��ʱ���ǽ��ῴ���������ϵ������ģ����һ���Ķ����������ϲ��˽�����

```shell
$ cd ..
$ git submodule update --remote --merge
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 2), reused 4 (delta 2)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   c87d55d..92c7337  stable     -> origin/stable
Updating c87d55d..92c7337
Fast-forward
 src/main.c | 1 +
 1 file changed, 1 insertion(+)
Submodule path 'DbConnector': merged in '92c7337b30ef9e0893e758dac2459d07362ab5ea'
```

������ǽ��� DbConnector Ŀ¼�����Է����µĸĶ��Ѿ��ϲ��뱾�� `stable` ��֧��
���������ǿ��������ǶԿ���һЩ���صĸĶ���ͬʱ��������������һ���޸ĵ�����ʱ�ᷢ��ʲô��

```shell
$ cd DbConnector/
$ vim src/db.c
$ git commit -am 'unicode support'
[stable f906e16] unicode support
 1 file changed, 1 insertion(+)
```
����������ڸ�����ģ�飬�ͻῴ���������ڱ������˸���ʱ����Ҳ��һ���Ķ���������Ҫ�������뱾�ء�

```shell
$ cd ..
$ git submodule update --remote --rebase
First, rewinding head to replay your work on top of it...
Applying: unicode support
Submodule path 'DbConnector': rebased into '5d60ef9bbebf5a0c1c1050f242ceeb54ad58da94'
```
��������� `--rebase` �� `--merge`��Git �Ὣ��ģ�����Ϊ�������ϵ�״̬��
���һὫ��Ŀ����Ϊһ������� HEAD ״̬��

```shell
$ git submodule update --remote
Submodule path 'DbConnector': checked out '5d60ef9bbebf5a0c1c1050f242ceeb54ad58da94'
```
��������ķ�����Ҳ��Ҫ������ֻ��ص�Ŀ¼���ٴμ����ķ�֧��������������Ĺ����ķ�֧��
Ȼ���ֶ��غϲ����� origin/stable�����κ�һ������Ҫ��Զ�̷�֧�������ˡ�

�����û���ύ��ģ��ĸĶ�����ô����һ����ģ�����Ҳ����������⣬
��ʱ Git ��ֻץȡ���Ķ������Ḳ����ģ��Ŀ¼��δ����Ĺ�����

```shell
$ git submodule update --remote
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 4 (delta 0)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   5d60ef9..c75e92a  stable     -> origin/stable
error: Your local changes to the following files would be overwritten by checkout:
	scripts/setup.sh
Please, commit your changes or stash them before you can switch branches.
Aborting
Unable to checkout 'c75e92a2b3855c9e5b66f915308390d9db204aca' in submodule path 'DbConnector'
```
���������һЩ�����θĶ���ͻ�ĸĶ��������и���ʱ Git ������֪����

```shell
$ git submodule update --remote --merge
Auto-merging scripts/setup.sh
CONFLICT (content): Merge conflict in scripts/setup.sh
Recorded preimage for 'scripts/setup.sh'
Automatic merge failed; fix conflicts and then commit the result.
Unable to merge 'c75e92a2b3855c9e5b66f915308390d9db204aca' in submodule path 'DbConnector'
```
����Խ�����ģ��Ŀ¼��Ȼ�����ƽʱ�����޸���ͻ��

### 3.4 ������ģ��Ķ�

�������ǵ���ģ��Ŀ¼����һЩ�Ķ��� ������һЩ������ͨ�����´���������ģ�����һЩ�Ǳ������ɵģ�
�������ǻ�û���������ǣ����Զ��κ������˶������á�

```shell
$ git diff
Submodule DbConnector c87d55d..82d2ad3:
  > Merge from origin/stable
  > updated setup script
  > unicode support
  > remove unnecessary method
  > add new option for conn pooling
```
�������������Ŀ���ύ�����͵�����������ģ���ϵĸĶ����������Լ�������޸ĵ��˻������鷳�� 
��Ϊ�����޷��õ���������ģ��Ķ�����Щ�Ķ�ֻ���������Ǳ��صĿ����С�

Ϊ��ȷ���ⲻ�ᷢ����������� Git �����͵�����Ŀǰ���������ģ���Ƿ������͡�
`git push` ������ܿ�������Ϊ ��check�� �� ��on-demand�� �� `--recurse-submodules` ������ 
����κ��ύ����ģ��Ķ�û��������ô ��check�� ѡ���ֱ��ʹ `push` ����ʧ�ܡ�

```shell
$ git push --recurse-submodules=check
The following submodule paths contain changes that can
not be found on any remote:
  DbConnector

Please try

	git push --recurse-submodules=on-demand

or cd to the path and use

	git push

to push them to a remote.
```
������������Ҳ��������һЩ���õĽ��飬ָ�����������������
��򵥵�ѡ���ǽ���ÿһ����ģ����Ȼ���ֶ����͵�Զ�ֿ̲⣬ȷ�������ܱ��ⲿ���ʵ���
֮���ٴγ���������͡� �������Ҫ���������Ͷ�ִ�м�飬��ô����ͨ������ 
`git config push.recurseSubmodules check` ������ΪĬ����Ϊ��

��һ��ѡ����ʹ�� ��on-demand�� ֵ�����᳢��Ϊ����������

```shell
$ git push --recurse-submodules=on-demand
Pushing submodule 'DbConnector'
Counting objects: 9, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (9/9), 917 bytes | 0 bytes/s, done.
Total 9 (delta 3), reused 0 (delta 0)
To https://github.com/chaconinc/DbConnector
   c75e92a..82d2ad3  stable -> stable
Counting objects: 2, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 266 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
To https://github.com/chaconinc/MainProject
   3d6d338..9a377d1  master -> master
```
����������Git ���뵽 DbConnector ģ����Ȼ������������Ŀǰ���������� 
����Ǹ���ģ����ΪĳЩԭ������ʧ�ܣ�����ĿҲ������ʧ�ܡ� 
��Ҳ����ͨ������ `git config push.recurseSubmodules on-demand` ������ΪĬ����Ϊ��

### 3.5 �ϲ���ģ��Ķ�
�����������ͬʱ�Ķ���һ����ģ�����ã���ô���ܻ�����һЩ���⡣
Ҳ����˵�������ģ�����ʷ�Ѿ��ֲ沢���ڸ���Ŀ�зֱ��ύ���˷ֲ�ķ�֧�ϣ���ô����Ҫ��һЩ�������޸�����

���һ���ύ����һ����ֱ�����ȣ�һ�����ʽ�ϲ�������ô Git ��򵥵�ѡ��֮����ύ���ϲ�������ûʲô���⡣

������Git �������᳢��ȥ����һ�μ򵥵ĺϲ��� �����ģ���ύ�Ѿ��ֲ�����Ҫ�ϲ��������õ������������Ϣ��

```shell
$ git pull
remote: Counting objects: 2, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 2 (delta 1), reused 2 (delta 1)
Unpacking objects: 100% (2/2), done.
From https://github.com/chaconinc/MainProject
   9a377d1..eb974f8  master     -> origin/master
Fetching submodule DbConnector
warning: Failed to merge submodule DbConnector (merge following commits not found)
Auto-merging DbConnector
CONFLICT (submodule): Merge conflict in DbConnector
Automatic merge failed; fix conflicts and then commit the result.
```
���Ա����� Git ������ָ������ģ����ʷ�е�������֧��¼���Ѿ��ֲ沢����Ҫ�ϲ���
���������Ϊ ��merge following commits not found�� ��δ�ҵ���������Ҫ�ϲ����ύ����
��Ȼ���е��������󣬲���֮�����ǻ����Ϊʲô��������

Ϊ�˽��������⣬����ҪŪ�����ģ��Ӧ�ô�������״̬�� ��ֵ��ǣ�Git �������������ܰ��������������Ϣ��
�����������ύ��ʷ�е� `SHA-1` ֵ��û�С� ���˵��ǣ�������׽���� ��������� git diff��
�ͻ�õ���ͼ�ϲ���������֧�м�¼���ύ�� SHA-1 ֵ��

```shell
$ git diff
diff --cc DbConnector
index eb41d76,c771610..0000000
--- a/DbConnector
+++ b/DbConnector
```
���ԣ��ڱ����У�`eb41d76` �����ǵ���ģ���д�ҹ��е��ύ���� `c771610` ������ӵ�е��ύ�� 
������ǽ�����ģ��Ŀ¼�У���Ӧ���Ѿ��� `eb41d76` ���ˣ���Ϊ�ϲ�û�ж������� ������ǵĻ�������ʲôԭ��
�㶼���Լ򵥵ش��������һ��ָ�����ķ�֧��

������һ�ߵ��ύ�� `SHA-1` ֵ�Ƚ���Ҫ�� ������Ҫ�����ϲ�����ġ� ����Գ���ֱ��ͨ�� SHA-1 �ϲ���
Ҳ����Ϊ������һ����֧Ȼ���Ժϲ��� ���ǽ�����ߣ�����ֻ��Ϊ��һ����Ư���ĺϲ��ύ��Ϣ��

���ԣ����ǽ��������ģ��Ŀ¼������ `git diff` �ĵڶ��� SHA-1 ����һ����֧Ȼ���ֶ��ϲ���

```shell
$ cd DbConnector

$ git rev-parse HEAD
eb41d764bccf88be77aced643c13a7fa86714135

$ git branch try-merge c771610
(DbConnector) $ git merge try-merge
Auto-merging src/main.c
CONFLICT (content): Merge conflict in src/main.c
Recorded preimage for 'src/main.c'
Automatic merge failed; fix conflicts and then commit the result.
```
����������õ���һ�������ĺϲ���ͻ�����������Ҫ������ύ������ôֻ��򵥵�ͨ���������������Ŀ��

```shell
$ vim src/main.c (1)
$ git add src/main.c
$ git commit -am 'merged our changes'
Recorded resolution for 'src/main.c'.
[master 9fd905e] merged our changes

$ cd .. (2)
$ git diff (3)
diff --cc DbConnector
index eb41d76,c771610..0000000
--- a/DbConnector
+++ b/DbConnector
@@@ -1,1 -1,1 +1,1 @@@
- Subproject commit eb41d764bccf88be77aced643c13a7fa86714135
 -Subproject commit c77161012afbbe1f58b5053316ead08f4b7e6d1d
++Subproject commit 9fd905e5d7f45a0d4cbc43d1ee550f16a30e825a
$ git add DbConnector (4)

$ git commit -m "Merge Tom's Changes" (5)
[master 10d2c60] Merge Tom's Changes
```

 1. ���Ƚ����ͻ
 2. Ȼ�󷵻ص�����ĿĿ¼��
 3. �ٴμ�� SHA-1 ֵ
 4. �����ͻ����ģ���¼
 5. �ύ���ǵĺϲ�

����ܻ������е�����󣬵���ȷʵ���ѡ�

��Ȥ���ǣ�Git ���ܴ�����һ������� �����ģ��Ŀ¼�д���������һ���ϲ��ύ��
������ʷ�а����˵�**����**���ύ����ô Git �Ὠ���㽫����Ϊһ�����еĽ�������� 
��������������ģ����Ŀ��ĳһ���Ϻϲ��˰����������ύ�ķ�֧�������������Ҫ�Ǹ���

�����Ϊʲôǰ��Ĵ�����Ϣ�� ��merge following commits not found������Ϊ������ **����** ����
��������������Ϊ˭���뵽���᳢����������

������ҵ���һ�����Խ��ܵĺϲ��ύ����ῴ�������������Ϣ��

```shell
$ git merge origin/master
warning: Failed to merge submodule DbConnector (not fast-forward)
Found a possible merge resolution for the submodule:
 9fd905e5d7f45a0d4cbc43d1ee550f16a30e825a: > merged our changes
If this is correct simply add it to the index for example
by using:

  git update-index --cacheinfo 160000 9fd905e5d7f45a0d4cbc43d1ee550f16a30e825a "DbConnector"

which will accept this suggestion.
Auto-merging DbConnector
CONFLICT (submodule): Merge conflict in DbConnector
Automatic merge failed; fix conflicts and then commit the result.
```
Git ����������Ǹ��������������������� `git add` �����������������ͻȻ���ύ�� ��������ܲ�Ӧ����������
��������ɵؽ�����ģ��Ŀ¼���鿴������ʲô�����������ύ��ǡ���ز��ԣ�Ȼ���ύ����

```shell
$ cd DbConnector/
$ git merge 9fd905e
Updating eb41d76..9fd905e
Fast-forward

$ cd ..
$ git add DbConnector
$ git commit -am 'Fast forwarded to a common submodule child'
```
��Щ���������ͬһ���£�����ͨ�����ַ�ʽ�����ٿ�����֤�����Ƿ���Ч��
�Լ����������ʱ����ȷ����ģ��Ŀ¼������Ĵ��롣

## 4 ��ģ�Ŀ鼼��
�����������������������ģ�鹤������һ�����

### 4.1 ��ģ�����
��һ�� `foreach` ��ģ�����������ÿһ����ģ��������������� �����Ŀ�а����˴�����ģ�飬���ǳ����á�

���磬����������Ҫ��ʼ����һ���¹��ܻ����޸�һЩ���󣬲�����Ҫ�ڼ�����ģ���ڹ����� 
���ǿ������ɵر���������ģ��Ĺ������ȡ�

```shell
$ git submodule foreach 'git stash'
Entering 'CryptoLibrary'
No local changes to save
Entering 'DbConnector'
Saved working directory and index state WIP on stable: 82d2ad3 Merge from origin/stable
HEAD is now at 82d2ad3 Merge from origin/stable
```
Ȼ�����ǿ��Դ���һ���·�֧������������ģ�鶼�л���ȥ��

```shell
$ git submodule foreach 'git checkout -b featureA'
Entering 'CryptoLibrary'
Switched to a new branch 'featureA'
Entering 'DbConnector'
Switched to a new branch 'featureA'
```
��Ӧ�����ס� �ܹ�����һ������Ŀ����������Ŀ�ĸĶ���ͳһ�����Ƿǳ����õġ�

```shell
$ git diff; git submodule foreach 'git diff'
Submodule DbConnector contains modified content
diff --git a/src/main.c b/src/main.c
index 210f1ae..1f0acdc 100644
--- a/src/main.c
+++ b/src/main.c
@@ -245,6 +245,8 @@ static int handle_alias(int *argcp, const char ***argv)

      commit_pager_choice();

+     url = url_decode(url_orig);
+
      /* build alias_argv */
      alias_argv = xmalloc(sizeof(*alias_argv) * (argc + 1));
      alias_argv[0] = alias_string + 1;
Entering 'DbConnector'
diff --git a/src/db.c b/src/db.c
index 1aaefb6..5297645 100644
--- a/src/db.c
+++ b/src/db.c
@@ -93,6 +93,11 @@ char *url_decode_mem(const char *url, int len)
        return url_decode_internal(&url, len, NULL, &out, 0);
 }

+char *url_decode(const char *url)
+{
+       return url_decode_mem(url, strlen(url));
+}
+
 char *url_decode_parameter_name(const char **query)
 {
        struct strbuf out = STRBUF_INIT;
```
��������ǿ�����ģ���ж�����һ��������������Ŀ�е��������� �������Ǹ����˵����ӣ�
����ϣ�����������������ַ������ô���

### 4.2 ���õı���
�������Ϊ����һЩ�������ñ�������Ϊ���ǿ��ܻ�ǳ��������ֲ�������ѡ����Ϊ���ǵ�Ĭ��ѡ�
������ [**Git ����**](https://git-scm.com/book/zh/v2/ch00/_git_aliases) ���������� Git ������ 
���������ƻ��� Git �д���ʹ����ģ��Ļ���������һЩ���ӡ�

```shell
$ git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'"
$ git config alias.spush 'push --recurse-submodules=on-demand'
$ git config alias.supdate 'submodule update --remote --merge'
```
����������Ҫ������ģ��ʱ���Լ򵥵����� git supdate���� git spush �����ģ�����������͡�

## 5 ��ģ�������
Ȼ��ʹ����ģ�黹����һЩС���⡣

### 5.1 �л���֧
���磬ʹ�� Git 2.13 ��ǰ�İ汾ʱ��������ģ�����Ŀ���л���֧���ܻ�����鷳�� ����㴴��һ���·�֧��
���������һ����ģ�飬֮���л���û�и���ģ��ķ�֧��ʱ������Ȼ����һ����δ���ٵ���ģ��Ŀ¼��

```shell
$ git --version
git version 2.12.2

$ git checkout -b add-crypto
Switched to a new branch 'add-crypto'

$ git submodule add https://github.com/chaconinc/CryptoLibrary
Cloning into 'CryptoLibrary'...
...

$ git commit -am 'adding crypto library'
[add-crypto 4445836] adding crypto library
 2 files changed, 4 insertions(+)
 create mode 160000 CryptoLibrary

$ git checkout master
warning: unable to rmdir CryptoLibrary: Directory not empty
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	CryptoLibrary/

nothing added to commit but untracked files present (use "git add" to track)
```
�Ƴ��Ǹ�Ŀ¼�������ѣ�������һ��Ŀ¼���Ƕ���������һ������ ������Ƴ���Ȼ���л������Ǹ���ģ��ķ�֧��
��Ҫ���� `submodule update --init` �����½�������䡣

```shell
$ git clean -fdx
Removing CryptoLibrary/

$ git checkout add-crypto
Switched to branch 'add-crypto'

$ ls CryptoLibrary/

$ git submodule update --init
Submodule path 'CryptoLibrary': checked out 'b8dda6aa182ea4464f3f3264b11e0268545172af'

$ ls CryptoLibrary/
Makefile	includes	scripts		src
```
��˵һ�飬����Ĳ��ѣ�ֻ�ǻ������е������

�°�� Git��>= 2.13��ͨ��Ϊ `git checkout` ������� `--recurse-submodules` ѡ�����������Щ���裬
����Ϊ������Ҫ�л����ķ�֧����ģ�鴦�ڵ���ȷ״̬��

```shell
$ git --version
git version 2.13.3

$ git checkout -b add-crypto
Switched to a new branch 'add-crypto'

$ git submodule add https://github.com/chaconinc/CryptoLibrary
Cloning into 'CryptoLibrary'...
...

$ git commit -am 'adding crypto library'
[add-crypto 4445836] adding crypto library
 2 files changed, 4 insertions(+)
 create mode 160000 CryptoLibrary

$ git checkout --recurse-submodules master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

nothing to commit, working tree clean
```
�����ڸ�����Ŀ�ļ�����֧�Ϲ���ʱ���� `git checkout` ʹ�� `--recurse-submodules` ѡ��Ҳ�����ã�
�����������ģ�鴦�ڲ�ͬ���ύ�ϡ�ȷʵ��������ڼ�¼����ģ��Ĳ�ͬ�ύ�ķ�֧���л���
��ô��ִ�� `git status` ����ģ�����ʾΪ�����޸ġ���ָ�����µ��ύ����
������Ϊ��ģ���״̬Ĭ�ϲ������л���֧ʱ������

���ǳ�����������˵������Ŀ��ӵ����ģ��ʱ����������ʹ�� `git checkout --recurse-submodules`�� 
������û�� `--recurse-submodules` ѡ��ľɰ� Git���ڼ��֮���ʹ�� 
`git submodule update --init --recursive` ������ģ�鴦����ȷ��״̬����

���˵��ǣ������ͨ�� `git config submodule.recurse true` ���� `submodule.recurse` ѡ� 
���� Git��>=2.14������ʹ�� `--recurse-submodules`�� ������������Ҳ���� Git Ϊÿ��ӵ�� 
`--recurse-submodules` ѡ���������� `git clone`�� ���ǵݹ������ģ����ִ�С�

### 5.2 ����Ŀ¼�л�����ģ��
��һ����Ҫ�ĸ��������������˽���Ŀ¼ת��Ϊ��ģ������⡣ ���������Ŀ���Ѿ�������һЩ�ļ���
Ȼ����Ҫ�������ƶ���һ����ģ���У���ô�����С�ģ����� Git ����㷢Ƣ���� ������Ŀ����һЩ�ļ�����Ŀ¼�У�
����Ҫ����ת��Ϊһ����ģ�顣 ���ɾ����Ŀ¼Ȼ������ `submodule add`��Git �ᳯ��󺰣�

```shell
$ rm -Rf CryptoLibrary/
$ git submodule add https://github.com/chaconinc/CryptoLibrary
'CryptoLibrary' already exists in the index
```
�����Ҫ��ȡ���ݴ� CryptoLibrary Ŀ¼�� Ȼ��ſ��������ģ�飺

```shell
$ git rm -r CryptoLibrary
$ git submodule add https://github.com/chaconinc/CryptoLibrary
Cloning into 'CryptoLibrary'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
```
���ڼ�������һ����֧�����������Ĺ�����
��������л��صķ�֧����Щ�ļ�������Ŀ¼������ģ����ʱ�������õ��������

```shell
$ git checkout master
error: The following untracked working tree files would be overwritten by checkout:
  CryptoLibrary/Makefile
  CryptoLibrary/includes/crypto.h
  ...
Please move or remove them before you can switch branches.
Aborting
```
�����ͨ�� `checkout -f` ��ǿ���л�������ҪС�ģ�������л���δ������޸ģ�������������Ǹ��ǵ���

```shell
$ git checkout -f master
warning: unable to rmdir CryptoLibrary: Directory not empty
Switched to branch 'master'
```
�����л�����֮����ΪĳЩԭ����õ���һ���յ� `CryptoLibrary` Ŀ¼������ 
`git submodule update` Ҳ�޷��޸����� ����Ҫ���뵽��ģ��Ŀ¼������ `git checkout` . 
���һ����е��ļ��� ��Ҳ����ͨ�� `submodule foreach` �ű���Ϊ�����ģ����������

Ҫ�ر�ע����ǣ�������ģ��Ὣ���ǵ����� Git ���ݱ����ڶ�����Ŀ�� `.git` Ŀ¼�У�
���Բ���ɰ汾�� Git���ݻ�һ����ģ��Ŀ¼�����ᶪʧ�κ��ύ���֧��

ӵ������Щ���ߣ�ʹ����ģ����Ϊ�����ڼ�����ص�ȴ�������Ŀ��ͬʱ�������൱����Ч�ķ�����
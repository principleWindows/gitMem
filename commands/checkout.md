# git checkout

- <https://zhuanlan.zhihu.com/p/465954849>

****************************

## Index

1. [git �ļ��](#git_checkout)
2. [detached HEAD](#detached-head) \
    [2.1 Introduction to git detached head](#introduction-to-git-detached-head) \
    [2.2 Git detached head workflow](#git-detached-head-workflow) \
    [2.3 Setting up the lab environment](#setting-up-the-lab-environment) \
    [2.4 How to work with git detached head](#how-to-work-with-git-detached-head) \
    [2.5 Summary](#summary)


## 1 git �ļ��<span id="git_checkout"></span>

�������л���֧�� 
```batch
    git checkout -b mybranch
```

![](pix/gitbranches.png)

�� `Git` �����У�`checkout` ����˼���Ƕ���һ��ʵ��Ĳ�ͬ�汾֮������л��Ĳ�����`git checkout` 
��������������ֲ�ͬ��ʵ�壺�ļ���`commit`���Լ���֧��

`checkout ��֧` �����ڼ��һ����֧�е�ĳ�ξɵ� `commit`��Ȼ�����µı���ᱻ�洢����Ŀ����ʷ�У�
��Ҳ����ζ���Ⲣ����һ��ֻ���Ĳ�����

`git checkout` ������ʱ���� `git clone` �����������������������Ϊ�����Ĳ�����ڣ�`git clone` 
���ڴ�Զ�ֿ̲��ȡ���룬�� `git checkout` �������ڱ���ϵͳ��ҵ�Ѵ��ڵĴ�������л���ͬ�İ汾��

`checkout` һ����֧������µ�ǰ�Ĺ����ռ��е��ļ���ʹ��������֧�� `commit` 
�汾״������һ�¡���֮�������е����б�����ᱻ��¼�� `checkout` 
�������Ǹ���֧�ϡ���� `checkout` ������ʵ����**��ѡ������֧**������Ϊ**�����֧**��

`checkout` һ�����ط�֧��Ȼ����Ӳ����ΪԶ�̷�֧������ `commit`:
```batch
git checkout -b ��branchname��
git reset --hard origin/��branchname��
```

[Back to index](#index)


## 2 detached HEAD

<https://www.golinuxcloud.com/git-detached-head-examples/>

����״̬�� HEAD

------

### 2.1 Introduction to git detached head

`HEAD` �� `Git` �������õ�ǰ���յ�ָ�롣`git checkout` ��� `HEAD` 
ָ�����Ϊָ���ض���֧���� `commit`������ָ��һ����֧ʱ��ûʲô���⣬���� 
`checkout` һ���ض��� `commit`���ͻὫ `HEAD` ָ����һ�������ָ��״̬��

��������������״̬ʱ��`Git` �ᾯ���㵱ǰ��������״̬�����������κθ���Ҳ����������������Ŀ�Ŀ������̡�
���ִ��Ҫ������״̬��չ�µ��޸ģ���Щ�޸Ľ����ᱻ�����ٺϲ����κη�֧��
Ȼ����û�а취ֻ���л���������֧ʱ���ⲿ���޸�Ҳ�޷������ص��µķ�֧��

![](pix/attached_detached.png)

��������Ӧ��ʼ�շ�����һ����֧�ϡ���������һ������״̬�� `HEAD` �ϡ�
�����ֻ��Ϊ��ȥ����ĳһ����ȥ���ύ��������ν�Ƿ�������״̬��

[Back to index](#index)


### 2.2 Git detached head workflow




[Back to index](#index)


### 2.3 Setting up the lab environment



[Back to index](#index)


### 2.4 How to work with git detached head



[Back to index](#index)


### 2.5 Summary


[Back to index](#index)



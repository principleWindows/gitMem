# Remove something


## �Ƴ�����

```batch
$ git rm -r --cached .vs        # ɾ�� .vs �ļ���
$ git commit -m 'remove .vs'    # �ύ,��Ӳ���˵��

$ git push -u origin master     # �����θ��ĸ��µ�Զ�ֿ̲���ȥ
```

�Ƴ����ļ��ĸ���
```batch
#ɾ��readme1.txt�ĸ��٣��������ڱ��ء�
git rm --cached readme1.txt

#ɾ��readme1.txt�ĸ��٣�����ɾ�������ļ���
git rm --f readme1.txt    
```

�Ƴ����ļ��еĸ���
```batch
#ɾ���� .gitee/ �ĸ��٣��������ڱ��ء�
git rm -r --cached .gitee/
rm '.gitee/ISSUE_TEMPLATE.zh-CN.md'
rm '.gitee/PULL_REQUEST_TEMPLATE.zh-CN.md'
```


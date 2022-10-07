# Remove something


## 移除跟踪

```batch
$ git rm -r --cached .vs        # 删除 .vs 文件夹
$ git commit -m 'remove .vs'    # 提交,添加操作说明

$ git push -u origin master     # 将本次更改更新到远程仓库上去
```

移除对文件的跟踪
```batch
#删除readme1.txt的跟踪，并保留在本地。
git rm --cached readme1.txt

#删除readme1.txt的跟踪，并且删除本地文件。
git rm --f readme1.txt    
```

移除对文件夹的跟踪
```batch
#删除对 .gitee/ 的跟踪，并保留在本地。
git rm -r --cached .gitee/
rm '.gitee/ISSUE_TEMPLATE.zh-CN.md'
rm '.gitee/PULL_REQUEST_TEMPLATE.zh-CN.md'
```


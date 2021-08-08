# git rebase -i HEAD~4 合并多个提交

[^_^]:
<https://www.cnblogs.com/zndxall/p/14087020.html>

****************************

```shell
git rebase -i HEAD~4
```

`git rebase` 操作实际上是将当前执行rebase分支的所有基于原分支提交点之后的commit打散成一个一个的patch，
并重新生成一个新的commit hash值，再次基于原分支目前最新的commit点上进行提交，
并不根据两个分支上实际的每次提交的时间点排序，rebase完成后，
切到基分支进行合并另一个分支时也不会生成一个新的commit点，可以保持整个分支树的完美线性



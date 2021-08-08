# Tips

https://www.cnblogs.com/zhuchenglin/p/7128383.html

******************

## 1 如何忽略跟踪已经纳入版本管理的文件

如果你在创建`.gitignore`文件之前就已经`push`项目了，那么即时你在`.gitignore`文件中写入新的规则，
这些规则也不会起作用。

有时候在项目开发过程中把某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，
原因是`.gitignore`只能忽略那些原来没有被`track`过的文件，如果某些文件已经被纳入了版本管理中，
则修改`.gitignore`是无效的。那么解决方法就是先把本地缓存删除（改变成未`track`状态），然后再提交：
```git
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

如果还是不行的话，先将想要取消追踪的文件移到项目目录外)，并提交，
然后提交后再将刚刚移出的文件再移入项目中即可。
 

**注意：**
不要误解了 `.gitignore` 文件的用途，该文件只能作用于 `Untracked Files`，
也就是那些从来没有被 `Git` 记录过的文件（自添加以后，从未 `add` 及 `commit` 过的文件）。
如果文件曾经被 `Git` 记录过，那么`.gitignore` 就对它们完全无效。


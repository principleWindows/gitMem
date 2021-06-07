# Set up Personal Webpage via GitHub Pages

[^_^]:
https://zhuanlan.zhihu.com/p/370549865

[^_^]:
https://pages.github.com/

[^_^]:
https://stackoverflow.com/questions/7212290/how-can-i-commit-specific-directory-to-a-different-than-a-working-branch-on-git

*****************************

GitHub Pages是一个静态站点托管服务，可直接从GitHub上的存储库获取HTML，
CSS和JavaScript文件，还可以选择在构建过程中运行这些文件并发布网站。

研究人员通常使用两种类型的个人网站模板：雨果（hugo）和杰基尔（jekyll）主题学术页面。
此处显示的示例使用基于“ minimum-mistakes-jekyll”主题的定制版本。

## 1 GitHub页面

创建一个GitHub账户，您的个人网站将在那里托管。

注意：如果您不想为任何域名地址付费，请仔细选择您的帐户名，因为它最终将成为您的网站链接地址。

在“代码”下从头下载相关学术页面的所有文件，或从研究人员现有的GitHub页面下载，例如，

* GitHub: zejiang-unsw的zejiang-unsw.github.io
* GitHub: oliviergimenez的oliviergimenez.github.io
* GitHub: samzipper的website-HEAL

## 2 GitHub Pages 使用不同的分支

### 2.1 How to commit a specific directory to a different than a working branch?

Reference Link：<https://blog.csdn.net/wu_xianqiang/article/details/107173240>

When you build a static website on github pages, based on Jekyll thems and the whole thing
will be in a github repository. The project structure is something like:
```shell
    _posts      # your documents of the website, usually in markdown format
    _pages      # other pages, such as About page, that need to be generated
    _layouts    # layout template for webpage
    _includes   # 被模板包含的HTML片段，可在_config.yml中修改位置
    assets      # other resouces, such as css layout,js scripts, pix etc
    _data       # dynamic data
    _sites      # the generated pages of the whole final static website
                # this directory is NOT in source control
    _config.yml # config info of the website
    index.html  # main web page of the website
```
When you run `jekyll build` command that jekyll compiles all the results into the `_sites`
directory, which is NOT in the git repository(at least not in the master brunch).

Note that the way GitHub pages work, is that you create a clean seperate branch 
named `gh-pages`, which will contain the final content. 
Now that if you want to make use of GitHub Pages and to use the `_sites` directory 
output as a GitHub page, the easiest way is to commit this whole subdirectory to the 
`gh-pages` branch.

Since `.gitignore` is versioned as well, just don't put the `_sites/` directory in the 
`gh-pages` branch's `.gitignore` file. Then, you can do something like this:
```shell
ORIG_HEAD="$(git name-rev --name-only HEAD)" git checkout gh-pages && mv publish/* . && git commit -am "automatic update" && git checkout "$ORIG_HEAD"
```

It does get triky if you're wanting to do things in the root directory rather than a 
subdirectory.

To use submodules in git, a detail description is in [submodules](../gitModules/submodules.md).

例如，某个git项目有三个平行的目录 `p1/`，`p2/`，`p3/`。随着开发进程的推移，
发现这三个目录的代码或文件的关联度很低，实际上是各自独立的。
例如最好用分支 `p1proj`，`p2proj`，`p3proj` 来进行管理，原来的master分支保留。
实际上我们可以通过 git subtree 来实现分支管理文件。

```shell
git subtree push --prefix p1 origin p1proj
git subtree push --prefix p2 origin p2proj
git subtree push --prefix p3 origin p3proj
```

最常见的是写 vuepress 文档，通常文档的位置在项目的 docs/.vuepress/dist 目录，
而且我们的文档部署的地方是 Github 中的 gh-pages 分支，所以可以执行下面命令把文档推到 gh-pages 分支。

```shell
git subtree push --prefix docs/.vuepress/dist origin gh-pages
```
当前我的项目有 master 分支和 gh-pages 分支，而且 gh-pages 分支使用的 master 分支中的文档中部分文件，
所以当你在 master 里面修改文档的时候，提交之后再推一下 gh-pages 分支就可以，两边代码就能保持一致了。




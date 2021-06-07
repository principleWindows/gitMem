# Set up Personal Webpage via GitHub Pages

[^_^]:
https://zhuanlan.zhihu.com/p/370549865

[^_^]:
https://pages.github.com/

[^_^]:
https://stackoverflow.com/questions/7212290/how-can-i-commit-specific-directory-to-a-different-than-a-working-branch-on-git

*****************************

GitHub Pages��һ����̬վ���йܷ��񣬿�ֱ�Ӵ�GitHub�ϵĴ洢���ȡHTML��
CSS��JavaScript�ļ���������ѡ���ڹ���������������Щ�ļ���������վ��

�о���Աͨ��ʹ���������͵ĸ�����վģ�壺�����hugo���ͽܻ�����jekyll������ѧ��ҳ�档
�˴���ʾ��ʾ��ʹ�û��ڡ� minimum-mistakes-jekyll������Ķ��ư汾��

## 1 GitHubҳ��

����һ��GitHub�˻������ĸ�����վ���������йܡ�

ע�⣺���������Ϊ�κ�������ַ���ѣ�����ϸѡ�������ʻ�������Ϊ�����ս���Ϊ������վ���ӵ�ַ��

�ڡ����롱�´�ͷ�������ѧ��ҳ��������ļ�������о���Ա���е�GitHubҳ�����أ����磬

* GitHub: zejiang-unsw��zejiang-unsw.github.io
* GitHub: oliviergimenez��oliviergimenez.github.io
* GitHub: samzipper��website-HEAL

## 2 GitHub Pages ʹ�ò�ͬ�ķ�֧

### 2.1 How to commit a specific directory to a different than a working branch?

Reference Link��<https://blog.csdn.net/wu_xianqiang/article/details/107173240>

When you build a static website on github pages, based on Jekyll thems and the whole thing
will be in a github repository. The project structure is something like:
```shell
    _posts      # your documents of the website, usually in markdown format
    _pages      # other pages, such as About page, that need to be generated
    _layouts    # layout template for webpage
    _includes   # ��ģ�������HTMLƬ�Σ�����_config.yml���޸�λ��
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

���磬ĳ��git��Ŀ������ƽ�е�Ŀ¼ `p1/`��`p2/`��`p3/`�����ſ������̵����ƣ�
����������Ŀ¼�Ĵ�����ļ��Ĺ����Ⱥܵͣ�ʵ�����Ǹ��Զ����ġ�
��������÷�֧ `p1proj`��`p2proj`��`p3proj` �����й���ԭ����master��֧������
ʵ�������ǿ���ͨ�� git subtree ��ʵ�ַ�֧�����ļ���

```shell
git subtree push --prefix p1 origin p1proj
git subtree push --prefix p2 origin p2proj
git subtree push --prefix p3 origin p3proj
```

�������д vuepress �ĵ���ͨ���ĵ���λ������Ŀ�� docs/.vuepress/dist Ŀ¼��
�������ǵ��ĵ�����ĵط��� Github �е� gh-pages ��֧�����Կ���ִ������������ĵ��Ƶ� gh-pages ��֧��

```shell
git subtree push --prefix docs/.vuepress/dist origin gh-pages
```
��ǰ�ҵ���Ŀ�� master ��֧�� gh-pages ��֧������ gh-pages ��֧ʹ�õ� master ��֧�е��ĵ��в����ļ���
���Ե����� master �����޸��ĵ���ʱ���ύ֮������һ�� gh-pages ��֧�Ϳ��ԣ����ߴ�����ܱ���һ���ˡ�




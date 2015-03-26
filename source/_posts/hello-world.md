title: Hello World
---
Welcome to [Hexo](http://hexo.io/)! This is your very first post. Check [documentation](http://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [trobuleshooting](http://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

<!--more-->

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](http://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](http://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](http://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](http://hexo.io/docs/deployment.html)


===
更新！
自己把自己坑了！之前的branch 没建好，还好自己最近没怎么写 blog...

方法应见：
[http://wuchong.me/blog/2014/01/17/use-github-to-manage-hexo-source/]()

---
---
填坑！

之前一次失误，直接把 Blog 的 hexo 源内容简单地加到了另一个 Branch 中，结果整个 Branch 都乱了！这次感觉好多了，肯定可以正常地把 blog 保存到 hexo branch 中！

参考上面的地址。

我们可以在 Github 上新建一个仓库，保存 Hexo 源内容，但是新开一个 repo 感觉怪怪的，所以我要改为加到 Blog 的 Hexo Branch 中。


---
步骤：

## 传上去

1. blog 先要搭好吧！这个没啥说的~
2. 把 blog 的 git 拉到本地来

	```
	git clone git@github.com:zwpaper/zwpaper.github.com.git
	#当然，后面的 git 地址要换成自己的
	```
3. 新建一个空 branch

	```
	git checkout --orphan hexo
	#这个选项真的会建一个很干净的分支！连 commit 内容都是新的
	```
4. 把之前存的东西在这个 branch 里都删了，没有用了

	```
	git rm -rf .
	#删 git 中内容
	如果文件夹内还有文件要话，也都删掉，但是 .git 不能删！
	rm -rf *
	#这个不会删隐藏文件，所以 .git 也不会被删，但是用 rm 命令还是自己仔细点好。。。
	```
5. 把之前的 hexo 源文件，也就是我们写 blog 的那些都复制到当前文件夹下面

	```
	cp ../blog/* .
	#路径自己确定，也是没有复制隐藏文件
	```
6. 加入 .gitignore

	```
	#.gitignore 内容
	public/
	.deploy/
	```
7. 上传到 github

	```
	git add .
	git commit -m "first commit"
	#注意下面这个一定要加上 origin hexo
	#要不就 push 到 master 里去了
	git push origin hexo
	```

好啦，这样就都放到 branch 里去啦，可以安心啦~

等明天试一下从别的电脑拉下来看看。

## 拉下来

```
git clone git@github.com:zwpaper/zwpaper.github.com.git -b hexo
```

## 可补充

其实应该把默认分支改一下，以后 push 的时候直接 push 给 hexo
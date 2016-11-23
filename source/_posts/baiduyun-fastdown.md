title: "百度云加速下载v2.0"
date: 2015-07-19 12:20:28
tags:
- Software
---

> 教程有点过时了！
> 教程有点过时了！
> 教程有点过时了！  
> 本想更新一下教程，结果发现度娘封这个插件封的好狠，简直是斗智斗勇。
> 2016.11.21 看到的情况是下不鸟，所以大家也不用向下看了。
> 有兴趣的旁朋，可以关注一下我的微博，如果哪天能用了，我更新了，会在微博说的

 [微博点我](http://weibo.com/zwpaper/)

> 自从百度云成为视频下载神器，百度云下载就广为人知，又从百度云无耻限速，百度云又被骂得广为人知，如果你还在因限速而惆怅，刚好你又在用 Chrome/Safari，来这里，就对了。
> 写了这个文章，结果还不少人问我怎么不能用，所以我又修改了一下，把教程做简单一点。

<!--more-->


# 准备工作：
## 下载文件
要用到的文件我都放在百度云了，直接下了就够了，强迫性也可以从下面主页下载

[http://pan.baidu.com/s/1kTZPgEF](http://pan.baidu.com/s/1kTZPgEF) 密码: 4966

1. 脚本文件 aria2baiduyun，见百度云
2. aria2 dmg文件，[https://github.com/tatsuhiro-t/aria2/releases](https://github.com/tatsuhiro-t/aria2/releases)
3. 浏览器插件（二选一）：主页：[https://github.com/acgotaku/BaiduExporter/releases](https://github.com/acgotaku/BaiduExporter/releases)
    * Chrome 插件 crx，--> [百度网盘助手](https://chrome.google.com/webstore/detail/baiduexporter/mjaenbjdjmgolhoafkohbhhbaiedbkno)
    * Safari 插件 BaiduExporter.safariextz，没有链接。
    
# 流程
## 安装 aria2
dmg 文件，直接打开，双击安装即可。

## 配置 aria2
找到之前下载的脚本文件，是一个压缩包 **aria2baiduyun.tar.gz** 使用常见解压文件就可以解压，有可能要解压两次。

解压后文件夹内有两个文件 **aria2.conf** 和 **aria2baiduyun.sh**

Mac 用户请打开 **Terminal**，也就是**终端**，打开程序菜单打 terminal 可以直接找到。

把 **aria2baiduyun.sh** 文件拖到终端的窗口里面，再按一下**回车**

输入下面命令后按**回车**。

```
source ~/.bash_profile
```

## 安装浏览器插件

### Chrome

* Chrome 市场直接安装，给能上的朋友：[百度网盘助手](https://chrome.google.com/webstore/detail/baiduexporter/mjaenbjdjmgolhoafkohbhhbaiedbkno)
* 不能打开 Chrome 市场的：
> 
    * 从上面提供的百度云里下载 BaiduExporter.crx
    * 打开 Chrome 菜单中的扩展程序
    * 勾选右上角 **开发者模式** 
    * 把 BaiduExporter.crx 拖到扩展程序页面


### Safari 
从上面提供的百度云里下载 BaiduExporter.safariextz

安装方式来自苹果官网：[https://support.apple.com/kb/PH21488?locale=zh_CN&viewlocale=zh_CN]()

> 安装来自开发者网站的扩展：下载，然后打开 .safariextz 文件。“Safari 扩展”偏好设置面板打开，并要求您确认扩展是否来自可信的来源。点按“信任”以安装扩展。


# 使用
准备工作完成，现在正式进入使用环节

## 运行 Aria2
这个操作**每次开机**时要执行一次：
打开一个 Terminal 界面，输入以下命令并回车。

```
aria2rpc
```

## 打开 YAAW
这是一个网站，你应该好好保存网址：
[http://binux.github.io/yaaw/demo/]()

第一次打开时会报一个错误：

```
Error: Internal server error
```

点右上角的扳手按钮，修改 `JSON-RPC Path` 内容，
把 `http://binux.github.io:6800/jsonrpc` 改为 `http://127.0.0.1:6800/jsonrpc`

保存，Save。

## 百度云

终于到激动人心的时候了，-> [点我打开百度云](http://pan.baidu.com/disk/home)

看到上面的图标了吗？

![导出下载](https://i.imgur.com/y4WqUym.png)

如果没有请重启一下 Chrome 或打开一个新 Chome 窗口，注意，不是新标签页。

选中要下载的文件，鼠标放到图标上，点击 `Aria2 RPC`

看看 YAAW 的页面？有没有惊喜？


---
再打个广告 -> [我是微博](http://weibo.com/zwpaper)



===
以下为旧文章
---
date: 2015-07-19 12:20:28
# 说明

文章没有干货，只是自己碰巧找到两个好用的软件，效果惊人，所以总结一下自己的使用情况。

因为要用到命令行，所以 Windows 没试过，Mac 和 Linux 用户应该是无压力的。


# 效果

扯别的都没用，先说一下我自己的速度情况。

以下都是同一个网络环境：

* Chrome 默认下载：200 - 300 KBps
* Axel：下不鸟.........
* Android ES 浏览器：500 - 1000 KBps
* 本文所用，Aria2：1 - 3 MBps

其中 Android 的 `ES 浏览器` 也很让我意外，基本可以稳定在 700 KBps。

# 软件

其实总共要用的软件就一个，`Aria2`，其它都是插件。

## Aria2

上面说到了要用命令行，就是因为 `Aria2` 是一个命令行软件，但是在用上相应插件后，完全不用担心自己不用全命令行。

[Aria2主页](http://sourceforge.net/projects/aria2/)

[Aria2 Github 主页](https://github.com/tatsuhiro-t/aria2)

然你要是和我一样喜欢命令行那就更无压力啦！

### 安装
以下内容要用到命令行，所以

* Mac 用户请打开 `Terminal`，也就是`终端`，打开程序菜单打 terminal 可以直接找到。
* Linux 用户我觉得不用我说了吧？也是 terminal，看发行版，自己解决。


#### Mac
Mac 推荐用 `Homebrew` 安装，只要一句

```
brew install aria2
```
> `Homebrew` 的安装要 `Xcode` 环境，所以如果没有安装 `Homebrew` 还得先安装 `Xcode`。

> 想安装 `Homebrew` 的用户请看这里 -> [我是Homebrew](http://brew.sh/index.html)

> 其实就是下面的命令就可以安装（也是 `Terminal` 中输入）：

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### Linux
发行版的差异真让我不知道应该怎么说明 Linux 安装。

举一个粟子吧，Ubuntu

```
sudo apt-get install aria2
```

这个是基本，但不是关键，所以安装完就好了。

#### 从源码安装
如果以上方式你都觉得不合适，也可以从源码安装，但我已经忘记 Mac 默认会缺哪几个软件了，所以如果你真要这么干双不会的话，欢迎点左边的微博图标骚扰我。

也可以点这里 -> [我是微博](http://weibo.com/zwpaper)

### Aria2 配置

Aria2 是一个命令行软件，所以配置是写在文件里的，你要把下面的内容放到一个能找到的地方，例如 `~/Documents/aria2.conf`
如果你不知道这是哪里，那你就打开 Mac 的 Finder，然后在侧边栏点 `文档（Documents）`，新建一个文件叫 `aria2.conf` 然后打开写下以下内容，注意修改两个地方：

* `用户名` 改为自己的用户名，不知道是什么的，请在命令行中输入 `pwd` 然后回车。
* 最后一行，如果是 `SSD` 即 `固态硬盘` 就不用改，如果是传统硬盘，就改成 `file-allocation=prealloc`

```
#允许rpc
enable-rpc=true
#允许非外部访问
rpc-listen-all=true
#RPC端口, 仅当默认端口被占用时修改
rpc-listen-port=6800

#最大同时下载数(任务数), 路由建议值: 3
max-concurrent-downloads=10
#断点续传
continue=true
#同服务器连接数
max-connection-per-server=10
#最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
min-split-size=10M
#单文件最大线程数, 路由建议值: 5
split=10
#下载速度限制
max-overall-download-limit=0
#单文件速度限制
max-download-limit=0
#上传速度限制
max-overall-upload-limit=0
#单文件速度限制
max-upload-limit=0

#文件保存路径, 默认为当前启动位置
dir=/Users/用户名/Downloads

#允许所有来源, web界面跨域权限需要
rpc-allow-origin-all=true

#文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
#所需时间 none < falloc ? trunc << prealloc, falloc和trunc需要文件系统和内核支持
# !!仅针对传统磁盘，SSD 降低文件碎片并不是什么好事。
file-allocation=none
```

### Aria2 命令快捷设置

在命令行中输入以后命令，`用户名` 还是一样改成上文那个。

```
echo "alias aria2rpc='aria2c --conf-path=/Users/用户名/Documents/aria2.conf -D'" >> ~/.bash_profile
```
然后

```
source ~/.bash_profile
```

相信我，你已经接近完成了。

---

## 插件

以下安装一个即可

* Chrome 插件，[百度网盘助手](https://chrome.google.com/webstore/detail/baiduexporter/mjaenbjdjmgolhoafkohbhhbaiedbkno)
* Firefox 插件，[百度网盘助手](https://raw.githubusercontent.com/acgotaku/BaiduExporter/master/firefox/baidu-exporter.xpi)

这个其实都可以不安装，就是一个网页，下面是它的主页

* [YAAW](http://binux.github.io/yaaw/)

# 使用

好了，现在装备齐全了，要怎么样才可以用的最舒服呢！

从现在开始，以后只用按以下步骤就可以高速下载

## 运行 Aria2

打开一个 `Terminal` 界面，输入以下并回车。

```
aria2rpc
```
好了，可以关闭 `Terminal`。
每次开机后运行一次即可。

## 打开 YAAW
还记得我说的 YAAW 其实就是一个页面吗？打开它：

[YAAW](http://binux.github.io/yaaw/demo/)

这真是个应该有一个错误

	Error: Internal server error
	
点右上角的扳手按钮，修改 `JSON-RPC Path` 内容，
把 `http://binux.github.io:6800/jsonrpc` 改为 `http://127.0.0.1:6800/jsonrpc`

保存，Save。

## 百度云

终于到激动人心的时候了，-> [点我打开百度云](http://pan.baidu.com/disk/home)

看到上面的图标了吗？

![导出下载](https://i.imgur.com/y4WqUym.png)

如果没有请重启一下 Chrome 或打开一个新 Chome 窗口，注意，不是新标签页。

选中要下载的文件，鼠标放到图标上，点击 `Aria2 RPC`

看看 YAAW 的页面？有没有惊喜？

# 后记

这个真的是一劳多逸，如果有命令行经验的话，连劳都不算。

后面没说 Linux 的东西了，不是我忘了，而是觉得大家应该都会。

如果能帮上忙就点个赞吧！XD

再打个广告 -> [我是微博](http://weibo.com/zwpaper)






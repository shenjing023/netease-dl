一个基于命令行的网易云音乐下载器。

<!-- vim-markdown-toc GFM -->
* [安装](#安装)
    * [Git clone最新版](#git-clone最新版)
    * [PyPi安装](#pypi安装)
* [功能特性](#功能特性)
* [使用](#使用)
    * [下载单首歌曲](#下载单首歌曲)
    * [下载一个歌手的50首热门歌曲](#下载一个歌手的50首热门歌曲)
    * [下载一张唱片的所有歌曲](#下载一张唱片的所有歌曲)
    * [下载一张歌单的所有歌曲](#下载一张歌单的所有歌曲)
    * [下载指定用户的公开歌单](#下载指定用户的公开歌单)
    * [下载个人收藏以及创建的歌单](#下载个人收藏以及创建的歌单)
* [更多选项](#更多选项)
    * [将歌曲下载到指定路径](#将歌曲下载到指定路径)
    * [设置代理](#设置代理)
* [更新日志](#更新日志)
* [Contact](#contact)

<!-- vim-markdown-toc -->


## 安装


### Git clone最新版

```bash
$ git clone https://github.com/ziwenxie/netease-dl
$ python3 setup.py install
```

### PyPi安装

```bash
$ pip3 install netease-dl
```

p.s: 目前仅支持Python3.x，Python2.x以后也会支持。


## 功能特性


通过`--help`可以查看到所有的功能特性，包括下载单首歌曲，一张唱片的所有歌曲，一个歌手的前50首热门歌曲，一张歌单的所有歌曲，一个用户的公开歌单以及登录后可下载个人的私有歌单。

```
$ netease-dl --help
Usage: netease-dl [OPTIONS] COMMAND [ARGS]...

  A command tool to download NetEase-Music's songs.

Options:
  -t, --timeout INTEGER  Time to wait before giving up, in seconds.
  -p, --proxy TEXT       Use the specified HTTP/HTTPS/SOCKS proxy.
  -o, --output PATH      Specify the storage path.
  -q, --quiet            Automatically select the best one.
  -l, --lyric            Download lyric.
  -a, --again            Login Again.
  --help                 Show this message and exit.

Commands:
  album     Download a album's songs by name or id.
  artist    Download a artist's hot songs by name or id.
  me        Download my playlists.
  playlist  Download a playlist's songs by id.
  song      Download a song by name or id.
  user      Download a user's playlists by id.
```


## 使用

### 下载单首歌曲

使用`song`命令，在后面通过`--name`或者`-n`选项来指定歌曲的名字：

```
$ netease-dl song --name 成都
...
Downlaoding 成都 12831kb  [####################################]  100%
```

上面会返回10条搜索结果，可以在`song`命令前面加一个`--quiet`，`netease-dl`会自动匹配第一个返回的结果：
```
$ netease-dl --quiet song --name 成都
Downlaoding 成都 12831kb  [####################################]  100%
```

如果知道歌曲id的话，也可以直接使用`--id`或者`-i`选项来指定：
```
$ netease-dl song --id 436514312
Downlaoding 成都 12831kb  [####################################]  100%
```

`netease-dl`的所有子命令所支持的特性都可以通过在子命令后面加一个`--help`选项来查看：
```
$ netease-dl song --help
Usage: netease-dl song [OPTIONS]

  Download a song by name or id.

Options:
  -n, --name TEXT   Song name.
  -i, --id INTEGER  Song id.
  --help            Show this message and exit.
```


### 下载一个歌手的50首热门歌曲

使用`artist`命令，并且在后面通过`--name`或者`-n`选项来指定歌手的姓名：

```
$ netease-dl artist --name 陈奕迅
Downlaoding 陪你度过漫长岁月 9471kb  [####################################]  100%
Downlaoding 不要说话 11149kb  [####################################]  100%
Downlaoding 红玫瑰 9376kb  [####################################]  100%
...
Cost 215s
```

和上面下载歌曲的时候一样，也可以使用`--quiet`和`--id`，下面也是一样的原理，接下来我就不重复了。


### 下载一张唱片的所有歌曲

使用`album`命令，后面接`--name`或者`-n`选项来指定唱片的名字：

```
$ netease-dl album --name 范特西
...
Downlaoding 爱在西元前 3661kb  [####################################]  100%
Downlaoding 爸我回来了 3682kb  [####################################]  100%
Downlaoding 简单爱 4235kb  [####################################]  100%
...
Cost 24s
```


### 下载一张歌单的所有歌曲

使用`playlist`命令，后面接`--name`或者`-n`选项来指定歌单的名字：
```
$ netease-dl playlist --name 美国Billboard周榜
...
Downlaoding Shape of You 3611kb  [####################################]  100%
Downlaoding Bad and Boujee 5227kb  [####################################]  100%
Downlaoding Thats What I Like 3230kb  [####################################]  100%
...
Cost 152s
```

### 下载指定用户的公开歌单

使用`user`命令，后面接`--name`或者`-n`选项来指定用户的名字：
```
$ netease-dl user --name 子文歇
...
Downlaoding Apologize 8131kb  [####################################]  100%
Downlaoding Thank You 8537kb  [####################################]  100%
Downlaoding Girl In The Mirror 8506kb  [####################################]  100%
Cost 16s
```


### 下载个人收藏以及创建的歌单

使用`me`命令登录之后可以下载自己的所有歌单包括私人的歌单，以后一段之间之内如果没有修改过密码就不需要重新登录了：
```
$ netease-dl me
Please enter your email or phone number: ziwenxiecat@163.com
Please enter your password:
...
```

如果要换一个帐号或者登录密码修改了，使用`--again`或者`-a`选项重新登录：
```
$ netease-dl --again me
```

## 更多选项

除了上面提到的`--quiet`选项，正如使用`netease-dl --help`选项看到的，`netease-dl`还支持设置代理，设置超时时间，指定下载目录，是否下载歌词等选项，这些都可以通过在子命令前面加上相关的选项来指定。

### 将歌曲下载到指定路径

将下载到的歌曲全部存储到当前路径下的music目录下面：
```
$ netease-dl -o music artist -n 周杰伦
```

### 设置代理

海外用户可能要设置相关的代理，`netease-dl`同时支持http和socks协议代理，注意要声明代理所使用的协议：
```
$ netease-dl -p 'http://127.0.0.1:8118' artist -n 周杰伦
$ netease-dl -p 'socks5://127.0.0.1:1080' artist -n 周杰伦
```

## 更新日志

2017-03-19 1.0.2 fix song may contains special character and won't download again if song exists(#2, #3)
2017-03-16 1.0.1 fix dependencies problem(#1)


## Contact

Email: ziwenxiecat@gmail.com
Blog: www.ziwenxie.site
WeChat: ziwenxie97

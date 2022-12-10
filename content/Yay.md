> yay是一个AUR Helper，他可以执行pacman的几乎所有操作，并在此基础上添加了很多额外用法。
> 
> 我没有在网络上查找到关于yay的、除了pacman基础用法和安装AUR包以外的中文教程，英文的也几乎没有看到，这也是我写这篇文章的原因所在。
> 
> 本文通篇详讲yay的每一个设置/选项（大概就是archwiki那种干涩的行文思路），最后会给出我自己的一些常用命令，但不会做解释。
> 
> 写作时参考了yay的英文使用手册，如果你的arch安装了yay，那么即可通过`man yay`命令随时查阅它。

**Tips1: 本文中出现的foo一般是指包名，标注*的表示该选项默认启用。**

**Tips2: 使用电脑端的访客可以在侧栏以获取目录。**

## [](https://zhul.in/2021/04/04/yay-more/#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95 "基本用法")基本用法[](https://zhul.in/2021/04/04/yay-more/#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)

yay的基本用法是`yay <operation> [options] [targets]`、`yay foo`和`yay`，`yay <operation> [options] [targets]`的用法可以讨论的点比较多，我会在后文中一一道来。

### [](https://zhul.in/2021/04/04/yay-more/#yay "yay")`yay`[](https://zhul.in/2021/04/04/yay-more/#yay)

当我们仅执行`yay`，后面不跟任何参数时，yay会执行操作`yay -Syu`，他会先调用pacman更新源的数据库、更新所有从源内安装的软件包，并检查你的AUR包有没有更新。

### [](https://zhul.in/2021/04/04/yay-more/#yay-foo "yay foo")`yay foo`[](https://zhul.in/2021/04/04/yay-more/#yay-foo)

通过yay后面直接跟包名的命令会让yay直接在源和AUR内搜索带有`foo`关键词的包（包名和简介中只要出现foo都会被一网打尽），以下是我执行`yay dingtalk`的输出

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  

```
5 aur/com.dingtalk.deepin 5.0.15deepin7-1 (+0 0.00)    Deepin Wine dingtalk4 aur/deepin.com.dingtalk.com 5.1.28.12-2 (+1 0.12)    DingTalk Client on Deepin Wine3 aur/dingtalk 2.1.3-1 (+3 0.00)    钉钉桌面版，基于electron和钉钉网页版开发，支持Windows、Linux和macOS2 aur/dingtalk-linux 3.5.5-1 (+6 0.12)    May be the official Linux experimental version1 aur/dingtalk-electron 2.1.9-1 (+9 0.15)    钉钉Linux版本==> Packages to install (eg: 1 2 3, 1-3 or ^4)==
```

输入每一项对应的序号即可进入相应的安装过程。

### [](https://zhul.in/2021/04/04/yay-more/#yay-lt-operation-gt-options-targets "yay <operation> [options] [targets]")`yay <operation> [options] [targets]`[](https://zhul.in/2021/04/04/yay-more/#yay-lt-operation-gt-options-targets)

在这里，<operation>每次只能有一个，[options]和[targets]可以有多个，且多个[options]可以合起来写在一起。比如`yay -P -s -f`可以直接写成`yay -Psf`，顺序也可以颠倒，`-Psf`和`-sPf`没区别。

#### [](https://zhul.in/2021/04/04/yay-more/#Y-yay "-Y (--yay)")`-Y (--yay)`[](https://zhul.in/2021/04/04/yay-more/#Y-yay)

-Y行为其实是yay的默认行为，当你没有加其他的行为参数时，yay就会执行-Y参数，可以跟`--gendb`和`-c`。

##### [](https://zhul.in/2021/04/04/yay-more/#gendb "--gendb")`--gendb`[](https://zhul.in/2021/04/04/yay-more/#gendb)

生成AUR数据库。**仅当从另一个AUR Helper迁移到yay时，才应使用此选项。**（根据我的个人理解，是根据你Arch内安装的源内找不到的包的包名去AUR里寻找对应的PKGBUILD，并且把能找到的PKGBUILD给clone到`~/.cache/yay/`目录下）

千玄子大佬说：“简单说来就是把在 AUR 的 PKGBUILD 下下来然后比对是否要更新。”

##### [](https://zhul.in/2021/04/04/yay-more/#c%EF%BC%88-clean%EF%BC%89 "-c（--clean）")`-c（--clean）`[](https://zhul.in/2021/04/04/yay-more/#c%EF%BC%88-clean%EF%BC%89)

清除不再需要的、没有被依赖的包。（相当于apt中的autoremove）

#### [](https://zhul.in/2021/04/04/yay-more/#P-show "-P(--show)")`-P(--show)`[](https://zhul.in/2021/04/04/yay-more/#P-show)

执行特定的Print操作。可以跟的[option]有`-c、-f、-d、-g、-n、-s、-u、-w、-q`

##### [](https://zhul.in/2021/04/04/yay-more/#c-complete "-c(--complete)")`-c(--complete)`[](https://zhul.in/2021/04/04/yay-more/#c-complete)

Print所有源内和AUR软件包的列表。这是给命令行操作提供的，并不打算由用户直接使用。（意思是启用了这个选项以后你的终端会出现一大串长常的列表来告诉你你的Arch到底可以从哪里安装哪些包，并不是直接给你用的，是作为数据留给别的命令来玩耍的）

##### [](https://zhul.in/2021/04/04/yay-more/#f-fish "-f(--fish)")`-f(--fish)`[](https://zhul.in/2021/04/04/yay-more/#f-fish)

在输出结果到终端时，会专门为fish用户做微调。（但是根据SamLukeYes大佬说他用fish体验下来并没有感知到加不加有什么区别，应该是属于感知不强的选项）

##### [](https://zhul.in/2021/04/04/yay-more/#d-defaultconfig "-d(--defaultconfig)")`-d(--defaultconfig)`[](https://zhul.in/2021/04/04/yay-more/#d-defaultconfig)

Print默认的yay配置。

##### [](https://zhul.in/2021/04/04/yay-more/#g-currentconfig "-g(--currentconfig)")`-g(--currentconfig)`[](https://zhul.in/2021/04/04/yay-more/#g-currentconfig)

Print当前的yay配置。

##### [](https://zhul.in/2021/04/04/yay-more/#n-numberupgrades "-n(--numberupgrades)")`-n(--numberupgrades)`[](https://zhul.in/2021/04/04/yay-more/#n-numberupgrades)

数一数你现在还有多少AUR包待更新。yay作者不推荐你使用呢，他推荐你用`yay -Qu`或者`wc -l`来代替它。

##### [](https://zhul.in/2021/04/04/yay-more/#s-stats "-s(--stats)")`-s(--stats)`[](https://zhul.in/2021/04/04/yay-more/#s-stats)

会展示一大堆信息，如下

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  

```
[zhullyb@Archlinux ~]$ yay -Ps==> Yay version v10.2.0							    #yay版本=============================================> Total installed packages: 1240				    #总共安装了多少包==> Total foreign installed packages: 24		    #多少包不是从源里安装的==> Explicitly installed packages: 271			    #有多少包是你自己主动安装的(而不是作为依赖安装的)==> Total Size occupied by packages: 14.3 GiB	    #安装的所有包合在一起一共占了你多少空间=============================================> Ten biggest packages:						    #十个体积最大的包wps-office-cn: 990.9 MiBttf-sarasa-gothic: 855.5 MiBlinux-firmware: 652.3 MiBbaidunetdisk-bin: 494.7 MiBcom.antutu.benchmark: 412.0 MiBwine: 402.2 MiBlinux-xanmod-cacule-uksm-cjktty: 324.4 MiBmicrosoft-edge-dev-bin: 316.4 MiBwine-mono: 316.2 MiBdeepin-wine5-i386: 259.5 MiB===========================================:: Querying AUR... -> Missing AUR Packages:  zhullyb-archlinux-git    #AUR里找不到的包 -> Flagged Out Of Date AUR Packages:  xml2		    #AUR中被人标注过期的包
```

##### [](https://zhul.in/2021/04/04/yay-more/#u-upgrades "-u(--upgrades)")`-u(--upgrades)`[](https://zhul.in/2021/04/04/yay-more/#u-upgrades)

展示你所有待更新的包。

##### [](https://zhul.in/2021/04/04/yay-more/#w-news "-w(--news)")`-w(--news)`[](https://zhul.in/2021/04/04/yay-more/#w-news)

展示来自archlinux.org的新闻。需要注意的是，这里的新闻是具有时效性的，只有在你的Arch最后一次更新以后发出来的新闻才会被显示出来。如果你不想要yay判断新闻时效性，你可以通过`yay -Pww`（即两个`w`）来获取所有能获得的新闻。

##### [](https://zhul.in/2021/04/04/yay-more/#q-quiet "-q(--quiet)")`-q(--quiet)`[](https://zhul.in/2021/04/04/yay-more/#q-quiet)

在输出新闻的时候，仅输出新闻的标题。该功能需要与`-w`连用，即`yay -Pwq`。

#### [](https://zhul.in/2021/04/04/yay-more/#G-getpkgbuild "-G(--getpkgbuild)")`-G(--getpkgbuild)`[](https://zhul.in/2021/04/04/yay-more/#G-getpkgbuild)

后跟包名。需要注意的是，如果指定的包不存在于官方源，则无法输出，后跟`-f、-p`参数。

_如果希望仅获取来自AUR（即排除第三方源的干扰）的PKGBUILD，后需跟`-a`参数。_

##### [](https://zhul.in/2021/04/04/yay-more/#f-force "-f(--force)")`-f(--force)`[](https://zhul.in/2021/04/04/yay-more/#f-force)

强制下载AUR中的PKGBUILD，如果它在yay缓存目录已经存在了，那就覆盖它！

##### [](https://zhul.in/2021/04/04/yay-more/#p-print "-p(--print)")`-p(--print)`[](https://zhul.in/2021/04/04/yay-more/#p-print)

Print指定包的PKGBUILD。

### [](https://zhul.in/2021/04/04/yay-more/#pacman-%E6%8B%93%E5%B1%95%E7%94%A8%E6%B3%95 "pacman 拓展用法")pacman 拓展用法[](https://zhul.in/2021/04/04/yay-more/#pacman-%E6%8B%93%E5%B1%95%E7%94%A8%E6%B3%95)

yay虽然可以使用pacman的所有<operation>，但是它远不仅于此。在这一段，我将向你介绍yay中包含的那些pacman不包括的pacman <operation

#### [](https://zhul.in/2021/04/04/yay-more/#S "-S")`-S`[](https://zhul.in/2021/04/04/yay-more/#S)

##### [](https://zhul.in/2021/04/04/yay-more/#S-Si-Sl-Ss-Su-Sc-Qu "-S, -Si, -Sl, -Ss, -Su, -Sc, -Qu")`-S, -Si, -Sl, -Ss, -Su, -Sc, -Qu`[](https://zhul.in/2021/04/04/yay-more/#S-Si-Sl-Ss-Su-Sc-Qu)

这些操作pacman都支持，而与pacman不同的是，yay的这些操作可以涵盖到**官方源/第三方源和AUR**中的所有包。

#### [](https://zhul.in/2021/04/04/yay-more/#Sc "-Sc")`-Sc`[](https://zhul.in/2021/04/04/yay-more/#Sc)

yay将会清除AUR包构建时的缓存和没有被track的文件。没有被track的文件在这里指AUR包构建时下载的sources或者构建完成的pkg包，但是vcs sources会被保留（比如.`git`文件夹）

#### [](https://zhul.in/2021/04/04/yay-more/#%E5%85%A8%E5%B1%80%E7%9A%84-options "全局的[options]")全局的[options][](https://zhul.in/2021/04/04/yay-more/#%E5%85%A8%E5%B1%80%E7%9A%84-options)

全局是指在所有<operation>下都可以加啦。

##### [](https://zhul.in/2021/04/04/yay-more/#repo "--repo")`--repo`[](https://zhul.in/2021/04/04/yay-more/#repo)

假定你给出的包名只存在源里（忽视AUR的存在）

##### [](https://zhul.in/2021/04/04/yay-more/#a-aur "-a(--aur)")`-a(--aur)`[](https://zhul.in/2021/04/04/yay-more/#a-aur)

假定你给出的包名只存在AUR中（忽视源的存在）

## [](https://zhul.in/2021/04/04/yay-more/#%E9%85%8D%E7%BD%AE%E8%AE%BE%E7%BD%AE "配置设置")配置设置[](https://zhul.in/2021/04/04/yay-more/#%E9%85%8D%E7%BD%AE%E8%AE%BE%E7%BD%AE)

原版的man手册排的比较混乱，我这里自己细分了几个类型，或许不是特别专业，但我希望能够帮助你们理解。

### [](https://zhul.in/2021/04/04/yay-more/#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B0%83%E7%94%A8%E5%91%BD%E4%BB%A4%E5%9E%8B "自定义调用命令型")自定义调用命令型[](https://zhul.in/2021/04/04/yay-more/#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B0%83%E7%94%A8%E5%91%BD%E4%BB%A4%E5%9E%8B)

##### [](https://zhul.in/2021/04/04/yay-more/#editor-lt-command-gt "--editor <command>")`--editor <command>`[](https://zhul.in/2021/04/04/yay-more/#editor-lt-command-gt)

设置编辑时调用的编辑器。

##### [](https://zhul.in/2021/04/04/yay-more/#makepkg-lt-command-gt "--makepkg <command>")`--makepkg <command>`[](https://zhul.in/2021/04/04/yay-more/#makepkg-lt-command-gt)

设置makepkg时需要调用makepkg命令（一般情况下用不到）

##### [](https://zhul.in/2021/04/04/yay-more/#pacman-lt-command-gt "--pacman <command>")`--pacman <command>`[](https://zhul.in/2021/04/04/yay-more/#pacman-lt-command-gt)

设置运行pacman时需要调用pacman命令（一般情况下用不到）

##### [](https://zhul.in/2021/04/04/yay-more/#tar-lt-command-gt "--tar <command>")`--tar <command>`[](https://zhul.in/2021/04/04/yay-more/#tar-lt-command-gt)

设置makepkg解压tar资源时调用的tar命令（一般情况下用不到）

##### [](https://zhul.in/2021/04/04/yay-more/#git-lt-command-gt "--git <command>")`--git <command>`[](https://zhul.in/2021/04/04/yay-more/#git-lt-command-gt)

设置makepkg clone git资源时调用的git命令（比如你可以安装AUR中的fgit-go，使用`--git fgit`参数来让fastgit代理clone的过程）

##### [](https://zhul.in/2021/04/04/yay-more/#gpg-lt-command-gt "--gpg <command>")`--gpg <command>`[](https://zhul.in/2021/04/04/yay-more/#gpg-lt-command-gt)

设置gpg验证资源时调用的gpg命令

##### [](https://zhul.in/2021/04/04/yay-more/#sudo-lt-command-gt "--sudo <command>")`--sudo <command>`[](https://zhul.in/2021/04/04/yay-more/#sudo-lt-command-gt)

设置调用sudo获取su权限安装pkg时所调用的sudo命令。

### [](https://zhul.in/2021/04/04/yay-more/#%E8%87%AA%E5%AE%9A%E4%B9%89%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%9E%8B "自定义配置文件型")自定义配置文件型[](https://zhul.in/2021/04/04/yay-more/#%E8%87%AA%E5%AE%9A%E4%B9%89%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%9E%8B)

##### [](https://zhul.in/2021/04/04/yay-more/#config-lt-file-gt "--config <file>")`--config <file>`[](https://zhul.in/2021/04/04/yay-more/#config-lt-file-gt)

设置读取的pacman配置文件。

##### [](https://zhul.in/2021/04/04/yay-more/#makepkgconf-lt-file-gt "--makepkgconf <file>")`--makepkgconf <file>`[](https://zhul.in/2021/04/04/yay-more/#makepkgconf-lt-file-gt)

设置读取的makepkg配置文件。

##### [](https://zhul.in/2021/04/04/yay-more/#nomakepkgconf "--nomakepkgconf")`--nomakepkgconf`[](https://zhul.in/2021/04/04/yay-more/#nomakepkgconf)

不读取系统中的makepkg.conf，仅使用Arch默认状态下的配置文件。

### [](https://zhul.in/2021/04/04/yay-more/#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E5%BE%84%E7%B1%BB%E5%9E%8B "自定义路径类型")自定义路径类型[](https://zhul.in/2021/04/04/yay-more/#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E5%BE%84%E7%B1%BB%E5%9E%8B)

##### [](https://zhul.in/2021/04/04/yay-more/#builddir-lt-dir-gt "--builddir <dir>")`--builddir <dir>`[](https://zhul.in/2021/04/04/yay-more/#builddir-lt-dir-gt)

设置build路径，默认路径为`~/.cache/yay/`

##### [](https://zhul.in/2021/04/04/yay-more/#absdir-lt-dir-gt "--absdir <dir>")`--absdir <dir>`[](https://zhul.in/2021/04/04/yay-more/#absdir-lt-dir-gt)

设置abs路径，默认路径为`~/.cache/yay/abs/`

### [](https://zhul.in/2021/04/04/yay-more/#%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92%E5%9E%8B "参数传递型")参数传递型[](https://zhul.in/2021/04/04/yay-more/#%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92%E5%9E%8B)

##### [](https://zhul.in/2021/04/04/yay-more/#editorflags-lt-flags-gt "--editorflags <flags>")`--editorflags <flags>`[](https://zhul.in/2021/04/04/yay-more/#editorflags-lt-flags-gt)

后跟需要跟随传递给编辑器的参数。如果需要传递多个参数，可以使用引号。

##### [](https://zhul.in/2021/04/04/yay-more/#mflags-lt-flags-gt "--mflags <flags>")`--mflags <flags>`[](https://zhul.in/2021/04/04/yay-more/#mflags-lt-flags-gt)

后跟需要跟随传递给makepkg的参数。如果需要传递多个参数，可以使用引号。

这个用的人不多，但其实是非常好用的一个功能。在我们安装`deepin-wine-tim`等包的时候，很可能会遇到文件明明完整但checksum不通过的情况，这时我们可以跟一个`--skipchecksums`参数传递给makepkg以跳过checksum的过程。

##### [](https://zhul.in/2021/04/04/yay-more/#gpgflags-lt-flags-gt "--gpgflags <flags>")`--gpgflags <flags>`[](https://zhul.in/2021/04/04/yay-more/#gpgflags-lt-flags-gt)

后跟需要跟随传递给pgp的参数。如果需要传递多个参数，可以使用引号。

##### [](https://zhul.in/2021/04/04/yay-more/#sudoflags-lt-flags-gt "--sudoflags <flags>")`--sudoflags <flags>`[](https://zhul.in/2021/04/04/yay-more/#sudoflags-lt-flags-gt)

后跟需要跟随传递给sudo的参数。如果需要传递多个参数，可以使用引号。

### [](https://zhul.in/2021/04/04/yay-more/#%E8%8F%9C%E5%8D%95%E9%85%8D%E7%BD%AE%E5%9E%8B "菜单配置型")菜单配置型[](https://zhul.in/2021/04/04/yay-more/#%E8%8F%9C%E5%8D%95%E9%85%8D%E7%BD%AE%E5%9E%8B)

#### [](https://zhul.in/2021/04/04/yay-more/#clean%E8%8F%9C%E5%8D%95 "clean菜单")clean菜单[](https://zhul.in/2021/04/04/yay-more/#clean%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#cleanmenu "*--cleanmenu")*`--cleanmenu`[](https://zhul.in/2021/04/04/yay-more/#cleanmenu)

启用清除询问菜单。（询问你是否需要清除已存在的文件）

##### [](https://zhul.in/2021/04/04/yay-more/#nocleanmenu "--nocleanmenu")`--nocleanmenu`[](https://zhul.in/2021/04/04/yay-more/#nocleanmenu)

禁用清除询问菜单。（不询问你是否需要清除已存在的文件）

##### [](https://zhul.in/2021/04/04/yay-more/#answerclean "--answerclean")`--answerclean`[](https://zhul.in/2021/04/04/yay-more/#answerclean)

自动回答cleanmenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](https://zhul.in/2021/04/04/yay-more/#noanswerclean "*--noanswerclean")*`--noanswerclean`[](https://zhul.in/2021/04/04/yay-more/#noanswerclean)

不设置自动回答。

#### [](https://zhul.in/2021/04/04/yay-more/#diff%E8%8F%9C%E5%8D%95 "diff菜单")diff菜单[](https://zhul.in/2021/04/04/yay-more/#diff%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#diffmenu "*--diffmenu")*`--diffmenu`[](https://zhul.in/2021/04/04/yay-more/#diffmenu)

启用对比询问菜单。（询问你是否需要对比本地文件和AUR文件）

##### [](https://zhul.in/2021/04/04/yay-more/#nodiffmenu "--nodiffmenu")`--nodiffmenu`[](https://zhul.in/2021/04/04/yay-more/#nodiffmenu)

禁用对比询问菜单。（不询问你是否需要对比本地文件和AUR文件）

##### [](https://zhul.in/2021/04/04/yay-more/#answerdiff "--answerdiff")`--answerdiff`[](https://zhul.in/2021/04/04/yay-more/#answerdiff)

自动回答cleanmenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](https://zhul.in/2021/04/04/yay-more/#noanswerdiff "*--noanswerdiff")*`--noanswerdiff`[](https://zhul.in/2021/04/04/yay-more/#noanswerdiff)

不设置自动回答。

#### [](https://zhul.in/2021/04/04/yay-more/#edit%E8%8F%9C%E5%8D%95 "edit菜单")edit菜单[](https://zhul.in/2021/04/04/yay-more/#edit%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#editmenu "--editmenu")`--editmenu`[](https://zhul.in/2021/04/04/yay-more/#editmenu)

启用修改询问菜单。（询问你是否需要修改PKGBUILD以及相关文件）

##### [](https://zhul.in/2021/04/04/yay-more/#noeditmenu "*--noeditmenu")*`--noeditmenu`[](https://zhul.in/2021/04/04/yay-more/#noeditmenu)

禁用修改询问菜单。（不询问你是否需要修改PKGBUILD以及相关文件）

##### [](https://zhul.in/2021/04/04/yay-more/#answeredit "--answeredit")`--answeredit`[](https://zhul.in/2021/04/04/yay-more/#answeredit)

自动回答editmenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](https://zhul.in/2021/04/04/yay-more/#noansweredit "*--noansweredit")*`--noansweredit`[](https://zhul.in/2021/04/04/yay-more/#noansweredit)

不设置自动回答。

#### [](https://zhul.in/2021/04/04/yay-more/#upgrade%E8%8F%9C%E5%8D%95 "upgrade菜单")upgrade菜单[](https://zhul.in/2021/04/04/yay-more/#upgrade%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#upgrademenu "*--upgrademenu")*`--upgrademenu`[](https://zhul.in/2021/04/04/yay-more/#upgrademenu)

启用更新询问菜单。（询问你是否需要更新AUR包）

##### [](https://zhul.in/2021/04/04/yay-more/#noupgrademenu "--noupgrademenu")`--noupgrademenu`[](https://zhul.in/2021/04/04/yay-more/#noupgrademenu)

禁用更新询问菜单。（不询问你是否需要更新AUR包）

##### [](https://zhul.in/2021/04/04/yay-more/#answerupgrade "--answerupgrade")`--answerupgrade`[](https://zhul.in/2021/04/04/yay-more/#answerupgrade)

自动回答upgrademenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](https://zhul.in/2021/04/04/yay-more/#noanswerupgrade "*--noanswerupgrade")*`--noanswerupgrade`[](https://zhul.in/2021/04/04/yay-more/#noanswerupgrade)

不设置自动回答。

#### [](https://zhul.in/2021/04/04/yay-more/#removemake%E8%8F%9C%E5%8D%95 "removemake菜单")removemake菜单[](https://zhul.in/2021/04/04/yay-more/#removemake%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#askremovemake "*--askremovemake")*`--askremovemake`[](https://zhul.in/2021/04/04/yay-more/#askremovemake)

在编译结束后，询问是否删除make depend。

##### [](https://zhul.in/2021/04/04/yay-more/#removemake "--removemake")`--removemake`[](https://zhul.in/2021/04/04/yay-more/#removemake)

在编译结束后，删除make depend。

##### [](https://zhul.in/2021/04/04/yay-more/#noremovemake "--noremovemake")`--noremovemake`[](https://zhul.in/2021/04/04/yay-more/#noremovemake)

在编译结束后，不删除make depend。

#### [](https://zhul.in/2021/04/04/yay-more/#provides%E8%8F%9C%E5%8D%95 "provides菜单")provides菜单[](https://zhul.in/2021/04/04/yay-more/#provides%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#provides "*--provides")*`--provides`[](https://zhul.in/2021/04/04/yay-more/#provides)

搜索AUR包时，一同寻找其在AUR上的依赖程序。 当找到多个提供该依赖的包时，将出现一个菜单，提示您选择一个。尽管这不会引起注意，但这会增加依赖项解决时间。

##### [](https://zhul.in/2021/04/04/yay-more/#noprovides "--noprovides")`--noprovides`[](https://zhul.in/2021/04/04/yay-more/#noprovides)

搜索AUR包时，不在AUR上寻找其依赖程序。尽管yay不会再次弹出依赖菜单供你选择，yay调用pacman时依然会出现pacman的选择菜单让你选择。

#### [](https://zhul.in/2021/04/04/yay-more/#pgpfetch%E8%8F%9C%E5%8D%95 "pgpfetch菜单")pgpfetch菜单[](https://zhul.in/2021/04/04/yay-more/#pgpfetch%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#pgpfetch "*--pgpfetch")*`--pgpfetch`[](https://zhul.in/2021/04/04/yay-more/#pgpfetch)

询问你是否从每个PKGBUILD的validpgpkeys字段导入未知的PGP密钥。

##### [](https://zhul.in/2021/04/04/yay-more/#nopgpfetch "--nopgpfetch")`--nopgpfetch`[](https://zhul.in/2021/04/04/yay-more/#nopgpfetch)

不自动导入陌生的PGP密钥。

#### [](https://zhul.in/2021/04/04/yay-more/#useask%E9%80%89%E9%A1%B9 "useask选项")useask选项[](https://zhul.in/2021/04/04/yay-more/#useask%E9%80%89%E9%A1%B9)

##### [](https://zhul.in/2021/04/04/yay-more/#useask "*--useask")*`--useask`[](https://zhul.in/2021/04/04/yay-more/#useask)

调用pacman的–ask询问用户是否删除系统中与当前包冲突的软件包。

##### [](https://zhul.in/2021/04/04/yay-more/#nouseask "--nouseask")`--nouseask`[](https://zhul.in/2021/04/04/yay-more/#nouseask)

不调用pacman的–ask询问用户是否删除系统中与当前包冲突的软件包，遇到冲突的软件包时直接报错，由用户来手动解决。

#### [](https://zhul.in/2021/04/04/yay-more/#combinedupgrade%E8%8F%9C%E5%8D%95 "combinedupgrade菜单")combinedupgrade菜单[](https://zhul.in/2021/04/04/yay-more/#combinedupgrade%E8%8F%9C%E5%8D%95)

##### [](https://zhul.in/2021/04/04/yay-more/#combinedupgrade "--combinedupgrade")`--combinedupgrade`[](https://zhul.in/2021/04/04/yay-more/#combinedupgrade)

在系统更新期间，将源内包和AUR包的更新菜单合并到一起。

##### [](https://zhul.in/2021/04/04/yay-more/#nocombinedupgrade "*--nocombinedupgrade")*`--nocombinedupgrade`[](https://zhul.in/2021/04/04/yay-more/#nocombinedupgrade)

在系统更新期间，先支持源内包的升级，完成后再进行AUR包的升级。

### [](https://zhul.in/2021/04/04/yay-more/#T-or-F-%E5%9E%8B "T or F 型")T or F 型[](https://zhul.in/2021/04/04/yay-more/#T-or-F-%E5%9E%8B)

#### [](https://zhul.in/2021/04/04/yay-more/#devel "devel")devel[](https://zhul.in/2021/04/04/yay-more/#devel)

##### [](https://zhul.in/2021/04/04/yay-more/#devel-1 "--devel")`--devel`[](https://zhul.in/2021/04/04/yay-more/#devel-1)

在系统更新期间，检查AUR的vcs包是否有更新，当前仅支持AUR的-git包。 devel查询是使用`git ls-remote`对比安装时和现在最新的commit_id完成的。

##### [](https://zhul.in/2021/04/04/yay-more/#nodevel "*--nodevel")*`--nodevel`[](https://zhul.in/2021/04/04/yay-more/#nodevel)

在系统更新期间， 不检查AUR的vcs包是否有更新。

#### [](https://zhul.in/2021/04/04/yay-more/#timeupdate "timeupdate")timeupdate[](https://zhul.in/2021/04/04/yay-more/#timeupdate)

##### [](https://zhul.in/2021/04/04/yay-more/#timeupdate-1 "--timeupdate")`--timeupdate`[](https://zhul.in/2021/04/04/yay-more/#timeupdate-1)

在系统更新期间，将已安装软件包的构建时间与每个软件包的AUR的最后修改时间进行比较。

##### [](https://zhul.in/2021/04/04/yay-more/#notimeupdate "*--notimeupdate")*`--notimeupdate`[](https://zhul.in/2021/04/04/yay-more/#notimeupdate)

在系统更新期间，不将已安装软件包的构建时间与每个软件包的AUR的最后修改时间进行比较。

#### [](https://zhul.in/2021/04/04/yay-more/#redownload "redownload")redownload[](https://zhul.in/2021/04/04/yay-more/#redownload)

##### [](https://zhul.in/2021/04/04/yay-more/#redownload-1 "--redownload")`--redownload`[](https://zhul.in/2021/04/04/yay-more/#redownload-1)

就算PKGBUILD已经存在，也要重新从AUR上获取一份新的PKGBUILD并覆盖原有PKGBUILD。

##### [](https://zhul.in/2021/04/04/yay-more/#redownloadall "--redownloadall")`--redownloadall`[](https://zhul.in/2021/04/04/yay-more/#redownloadall)

就算PKGBUILD已经存在，也要重新从AUR上获取所有AUR包的PKGBUILD并覆盖原有PKGBUILD。

##### [](https://zhul.in/2021/04/04/yay-more/#noredownload "*--noredownload")*`--noredownload`[](https://zhul.in/2021/04/04/yay-more/#noredownload)

当下载PKGBUILD时，，如果发现cache中的PKGBUILD版本＞＝AUR上的版本时，直接使用本地的PKGBUILD。

#### [](https://zhul.in/2021/04/04/yay-more/#rebuild "rebuild")rebuild[](https://zhul.in/2021/04/04/yay-more/#rebuild)

##### [](https://zhul.in/2021/04/04/yay-more/#rebuild-1 "--rebuild")`--rebuild`[](https://zhul.in/2021/04/04/yay-more/#rebuild-1)

即使在cache中有可用的二进制包的情况下，也始终要重新编译目标软件包。

##### [](https://zhul.in/2021/04/04/yay-more/#rebuildall "--rebuildall")`--rebuildall`[](https://zhul.in/2021/04/04/yay-more/#rebuildall)

即使在cache中有可用的二进制包的情况下，也始终要重新编译所有的AUR包。

##### [](https://zhul.in/2021/04/04/yay-more/#rebuildtree "--rebuildtree")`--rebuildtree`[](https://zhul.in/2021/04/04/yay-more/#rebuildtree)

安装AUR包时，以递归方式重新编译并重新安装其所有AUR依赖包，即使已安装的依赖项也是如此。 该选项使您可以轻松地针对当前系统的库重新构建软件包，如果它们变得不兼容。（比如python3.8->3.9）

##### [](https://zhul.in/2021/04/04/yay-more/#norebuild "*--norebuild")*`--norebuild`[](https://zhul.in/2021/04/04/yay-more/#norebuild)

构建软件包时，如果在缓存中找到该软件包并且该软件包与想要的软件包的版本相同，则跳过软件包的编译过程并使用现有的二进制程序。

#### [](https://zhul.in/2021/04/04/yay-more/#sudoloop "sudoloop")sudoloop[](https://zhul.in/2021/04/04/yay-more/#sudoloop)

##### [](https://zhul.in/2021/04/04/yay-more/#sudoloop-1 "--sudoloop")`--sudoloop`[](https://zhul.in/2021/04/04/yay-more/#sudoloop-1)

在后台循环调用sudo，以防止sudo授权在长时间构建期间超时。

##### [](https://zhul.in/2021/04/04/yay-more/#nosudoloop "*--nosudoloop")*`--nosudoloop`[](https://zhul.in/2021/04/04/yay-more/#nosudoloop)

不在后台循环调用sudo，可能会导致sudo授权在长时间构建期间超时。

#### "batchinstall")batchinstall

#####  "--batchinstall")`--batchinstall`

在构建和安装AUR包时，对每个软件包的安装进行排序，而并非在构建之后立刻安装每个软件包时。 需要注意的是，一旦构建了所有软件包，或者需要构建队列中的软件包作为构建另一个软件包的依赖项，应当在安装队列中安装所有软件包。

#####  "*--nobatchinstall")*`--nobatchinstall`

在构建AUR包成功后立即安装。

#### "clearafter")clearafter

#####  "--cleanafter")`--cleanafter`

在构建AUR包完成以后清除cache文件。

#####  "*--nocleanafter")*`--nocleanafter`

在构建AUR包完成以后不清除cache文件。

###  "其他型")其他型

##### "--save")`--save`

把你这一次执行yay后面跟的配置参数永久保存下来。

##### "--aururl")`--aururl`

更改aur源地址（默认为 [https://aur.archlinux.org](https://aur.archlinux.org/) ），适用于中国用户，可以使用此参数将AUR的地址设置成清华的反代，具体的配置命令为

```
yay --aururl "https://aur.tuna.tsinghua.edu.cn" --save
```

TUNA 的反代已经取消，可以使用如下命令设置回 AUR 官方源

```
yay --aururl "https://aur.archlinux.org" --save
```

#####  "--sortby")`--sortby`

在搜索过程中，按特定条件对AUR结果进行排序，后跟`<votes|popularity|id|baseid|name|base|submitted|modified`参数，默认为`votes`。

##### "--searchby")`--searchby`

通过指定查询类型来搜索AUR软件包，后跟`<name|name-desc|maintainer|depends|checkdepends|makedepends|optdepends`参数，默认为`name-desc`。

#####  "*--topdown")*`--topdown`

优先展示源内包，其次才是AUR包

#####  "--bottomup")`--bottomup`

优先展示AUR包，其次才是源内包

##### "--requestsplitn <number>")`--requestsplitn <number>`

设置在每次向AUR的请求的最大数值（默认150）。数值越高，请求时间越短，但是单次请求的数值过大会导致error。当这个数值＞500时你应当特别注意这一点。

##### "--completioninterval <days>")`--completioninterval <days>`

刷新完成高速缓存的时间（以天为单位,默认为7）。 将此值设置为0将导致每次刷新缓存，而将其设置为-1将导致永远不刷新缓存。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MzQ4MTgzMF19
-->
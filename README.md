### Git第一天

#### 今日目标

- 了解版本控制软件的作用
- 了解版本控制系统的分类
- Git的特性
- 初始化 Git 仓库的命令
- 查看文件状态的命令
- 一次性将文件加入暂存区的命令
- 将暂存区的文件提交到 Git 仓库的命令



#### 一、关于版本控制

##### 1、文件的版本

<img src="./images/文件的版本.png" style="width: 80%;">

思考：人和动物的本质区别是什么？

答：人会制造并使用工具！



##### 2、版本控制软件

<img src="./images/版本控制软件.png" style="width: 70%;">



##### 3、使用版本控制软件的好处

<img src="./images/使用版本控制软件的好处.png" style="width: 70%;">



##### 4、版本控制系统的分类  

<img src="./images/版本控制系统的分类.png" style="width: 80%;">



+ 本地版本控制系统（没人使用）

  <img src="./images/本地版本控制系统.png" style="width: 30%;">

  特点：使用软件来记录文件的不同版本，提高了工作效率，降低了手动维护版本的出错率

  缺点：1、**单机运行**，不支持多人协作开发

​				   2、版本数据库故障后，所有历史更新记录会丢失



+ 集中化的版本控制系统（很少使用）

  <img src="./images/集中化的版本控制系统.png" style="width: 40%;">

  特点：基于服务器、客户端的运行模式。① 服务器保存文件的所有更新记录。② 客户端**只保留最新的文件版本**

  优点：联网运行，支持多人协作开发

  缺点：1、不支持离线提交版本更新

  ​		   2、中心服务器崩溃后，所有人无法正常工作

  ​		   3、版本数据库故障后，所有历史更新记录会丢失

  

+ 分布式版本控制系统

  <img src="./images/分布式版本控制系统.png" style="width: 30%;">

  **典型代表：`Git`**

  特点：基于**服务器、客户端**的运行模式。① 服务器保存文件的所有更新版本。② **客户端是服务器的完整备份**，并不是只保留文件的最新版本

  优点：1、联网运行，支持多人协作开发

  ​           2、客户端**断网**后**支持离线本地提交**版本更新

  ​           3、服务器故障或损坏后，可使用任何一个客户端的备份进行恢复





#### 二、Git基础概念

##### 1、什么是 Git

**Git** 是一个**开源的分布式版本控制系统**，是目前世界上**最先进**、**最流行**的版本控制系统。可以快速高效地处理从很小到非常大的项目版本管理。

特点：项目越大越复杂，协同开发者越多，越能体现出 Git 的**高性能**和**高可用性**！



##### 2、Git 的特点

Git 之所以快速和高效，主要依赖于它的如下两个特性：

① 直接记录快照，而非差异比较

② 近乎所有操作都是本地执行



+ SVN 的差异比较

  传统的版本控制系统（例如 `SVN`）是**基于差异**的版本控制，它们存储的是**一组基本文件**和**每个文件随时间逐步累积的差异**

  <img src="./images/SVN 的差异比较.png" style="width: 70%;">

  好处：节省磁盘空间

  缺点：耗时、效率低。  在每次切换版本的时候，都需要在基本文件的基础上，应用每个差异，从而生成目标版本对应的文件

  

+ Git 的记录快照

  **Git 快照**是在原有文件版本的基础上重新生成一份新的文件，**类似于备份**。为了效率，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

  <img src="./images/Git 的记录快照.png" style="width: 70%;">

  **缺点：**占用磁盘空间较大

  **优点：** **版本切换时非常快**，因为每个版本都是完整的文件快照，切换版本时直接恢复目标版本的快照即可。

  **特点：** **空间换时间**



+ 近乎所有操作都是本地执行

  在 Git 中的绝大多数操作都**只需要访问本地文件和资源**，一般不需要来自网络上其它计算机的信息

  **特性：**① 断网后依旧可以在本地对项目进行版本管理

  ​		   ② 联网后，把本地修改的记录同步到云端服务器即可



##### 3、Git 中的三个区域

使用 Git 管理的项目，拥有三个区域，分别是**工作区**、**暂存区**、**Git 仓库**

<img src="./images/Git 中的三个区域.png" style="width: 70%;">



##### 4、Git 中的三种状态

<img src="./images/Git 中的三种状态.png" style="width: 70%;">

+ 已修改 `modified` ：表示修改了文件，但还没将修改的结果放到**暂存区**
+ 已暂存 `staged` ：表示对已修改文件的当前版本做了标记，使之包含在**下次提交的列表中**
+ 已提交 `committed` ：表示文件已经安全地保存在本地的 **Git 仓库中**

注意：1、工作区的文件被修改了，但还没有放到暂存区，就是**已修改**状态。

​			2、如果文件已修改并放入暂存区，就属于**已暂存**状态。

​			3、如果 Git 仓库中**保存着特定版本**的文件，就属于**已提交**状态。



##### 5、基本的 Git 工作流程

<img src="./images/基本的 Git 工作流程.png" style="width: 50%;">

基本的 Git 工作流程如下：

① 在工作区中修改文件

② 将你想要下次提交的更改进行暂存

③ 提交更新，找到暂存区的文件，将快照永久性存储到 Git 仓库



#### 三、安装并配置 Git

##### 1、安装 Git

+ 在 Windows 中下载并安装 Git

  在开始使用 `Git` 管理项目的版本之前，需要将它安装到计算机上。可以使用浏览器访问如下的网址，根据自己的操作系统，选择下载对应的 `Git` 安装包：

  链接地址：https://git-scm.com/downloads

  <img src="./images/安装git.png" style="width: 50%;">

+ 在 Mac 安装 Git

  通过 Homebrew 下载，如果没有 Homebrew ，参考以下链接进行安装：

  ```shell
  /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
  ```

  安装好在 **终端**  运行以下命令即可安装：

  ```shell
  brew install git
  ```

  

##### 2、配置用户信息

安装完 Git 之后，要做的第一件事就是设置自己的**用户名**和**邮件地址**。因为通过 Git 对项目进行版本管理的时候，Git 需要使用这些基本信息，来记录是谁对项目进行了操作：

```shell
git config --global user.name "itheima"
git config --global user.email "itheima@itcast.cn"
```

**注意：**如果使用了 --global 选项，那么该命令只需要运行一次，即可永久生效。



##### 3、Git 的全局配置文件

通过 `git config --global user.name` 和 `git config --global user.email` 配置的用户名和邮箱地址，会被写入到 `C:/Users/用户名文件夹/.gitconfig` 文件中(Windows)，`/Users/zhaohang/.gitconfig` (MacOS) 。这个文件是 `Git` 的**全局配置文件**，**配置一次即可永久生效**。

可以使用记事本打开此文件，从而查看自己曾经对 Git 做了哪些全局性的配置。

<img src="./images/Git全局配置文件.png" style="width: 30%;">

##### 4、检查配置信息

除了使用记事本查看全局的配置信息之外，还可以运行如下的终端命令，快速的查看 Git 的全局配置信息：

```shell
# 查看所有的全局配置项
git config --list --global
# 查看指定的全局配置项
git config user.name
git config user.email
```



##### 5、获取帮助信息

可以使用 `git help <verb>` 命令，无需联网即可在浏览器中打开帮助手册，例如：

```shell
# 打开 git config 命令的帮助手册
git help config
```

如果不想查看完整的手册，那么可以用 -h 选项获得更简明的“help”输出：

```shell
# 想要获取 git config 命令的快速参考
git config -h
```



#### 四、Git 的基本操作

##### 1、获取 Git 仓库的两种方式

① 将尚未进行版本控制的本地目录**转换**为 `Git` 仓库

② 从其它服务器**克隆**一个已存在的 `Git` 仓库

以上两种方式都能够在自己的电脑上得到一个可用的 Git 仓库



##### 2、在现有目录中初始化仓库（重要）

如果自己有一个尚未进行版本控制的项目目录，想要用 `Git` 来控制它，需要执行如下两个步骤：

① 在项目目录中，通过鼠标右键打开“`Git Bash`” 

② 执行 `git init` 命令将当前的目录转化为 `Git` 仓库

`git init` 命令会创建一个名为 .git 的隐藏目录，**这个 .git 目录就是当前项目的 Git 仓库**，里面包含了**初始的必要文件**，这些文件是 Git 仓库的**必要组成部分**



##### 3、工作区中文件的 4 种状态

工作区中的每一个文件可能有 4 种状态，这四种状态共分为两大类，如图所示：

<img src="./images/工作区中文件的 4 种状态.png" style="width: 80%;">

**Git 操作的终极结果：**让工作区中的文件都处于**“未修改”**的状态。



##### 4、检查文件的状态

可以使用 `git status` 命令查看文件处于什么状态，例如：

<img src="./images/检查文件的状态.png" style="width: 70%;">

在状态报告中可以看到新建的 `index.html` 文件出现在 `v files`（未跟踪的文件） 下面。

未跟踪的文件意味着 **`Git` 在之前的快照（提交）中没有这些文件**；`Git` 不会自动将之纳入跟踪范围，除非明确地告诉它“我需要使用 Git 跟踪管理该文件”。



##### 5、以精简的方式显示文件状态

使用 `git status` 输出的状态报告很详细，但有些繁琐。如果希望以精简的方式显示文件的状态，可以使用如下

两条完全等价的命令，其中 **-s** 是 **--short** 的简写形式：

```shell
# 以精简的方式显示文件状态
git status -s
git status --short
```

未跟踪文件前面有红色的 **??** 标记，例如：

<img src="./images/以精简的方式显示文件状态.png" style="width: 70%;">



##### 6、跟踪新文件

使用命令 `git add` 开始跟踪一个文件。 所以，要跟踪 `index.html` 文件，运行如下的命令即可：

```shell
git add index.html
# 如果文件过多，你项跟踪目录下所有文件
git add .
```

此时再运行 `git status` 命令，会看到 `index.html` 文件在 `Changes to be committed` 这行的下面，说明已被跟踪，并处于暂存状态：

<img src="./images/跟踪新文件.png" style="width: 100%;">



##### 7、提交更新

现在暂存区中有一个 `index.html` 文件等待被提交到 `Git` 仓库中进行保存。可以执行 `git commit` 命令进行提交，其中 `-m` 选项后面是本次的提交消息，用来对提交的内容做进一步的描述：

```shell
git commit -m "新建了index.html 文件"
```

提交成功之后，会显示如下的信息：

<img src="./images/提交更新.png" style="width: 60%;">

提交成功之后，再次检查文件的状态，得到提示如下：

<img src="./images/提交更新后状态.png" style="width: 60%;">

更新流程：

<img src="./images/提交更新流程.png" style="width: 60%;">



##### 8、对已提交的文件进行修改

目前，`index.html` 文件已经被 `Git` 跟踪，并且工作区和 `Git` 仓库中的 `index.html` 文件内容保持一致。当我们修改了工作区中 `index.html` 的内容之后，再次运行 `git status` 和 `git status -s` 命令，会看到如下的内容：

<img src="./images/对已提交的文件进行修改.png" style="width: 60%;">

文件 `index.html` 出现在 `Changes not staged for commit` 这行下面，说明**已跟踪文件的内容发生了变化，但还没有放到暂存区**。

**注意：**修改过的、没有放入暂存区的文件前面有红色的 **M** 标记。



##### 9、暂存已修改的文件

目前，工作区中的 `index.html` 文件已被修改，如果要暂存这次修改，需要再次运行 `git add` 命令，这个命令是个多功能的命令，主要有如下 3 个功效：

① 可以用它 **开始跟踪新文件**

② 把 **已跟踪的**、**且已修改** 的文件放到暂存区

③ 把有冲突的文件标记为已解决状态

<img src="./images/暂存已修改的文件.png" style="width: 60%;">



##### 10、提交已暂存的文件

再次运行 `git commit -m "提交消息"` 命令，即可将暂存区中记录的 `index.html` 的快照，提交到 `Git` 仓库中进行保存：

<img src="./images/提交已暂存的文件.png" style="width: 60%;">

提交修改后暂存文件流程：

<img src="./images/提交修改后暂存文件.png" style="width: 60%;">



##### 11、撤销对文件的修改（慎用）

**撤销对文件的修改指的是：**把对工作区中对应文件的修改，**还原**成 Git 仓库中所保存的版本。

**操作的结果：**所有的修改会丢失，且无法恢复！**危险性比较高，请慎重操作！**

```shell
# 撤销操作
git checkout -- 文件名
```

<img src="./images/撤销对文件的修改.png" style="width: 60%;">

**撤销操作的本质：**用 Git 仓库中保存的文件，覆盖工作区中指定的文件。



##### 12、向暂存区中一次性添加多个文件

如果需要被暂存的文件个数比较多，可以使用如下的命令，一次性将所有的新增和修改过的文件加入暂存区：

```shell
git add .
```

今后在项目开发中，会经常使用这个命令，将新增和修改过后的文件加入暂存区



##### 13、取消暂存的文件

如果需要从暂存区中移除对应的文件，可以使用如下的命令：

```shell
# 从暂存区移除单个文件
git reset HEAD 要移出的文件名称
# 从暂存区移除所有文件
git reset HEAD .
```



##### 14、跳过使用暂存区域

`Git` 标准的工作流程是`工作区 → 暂存区 → Git 仓库`，但有时候这么做略显繁琐，此时可以跳过暂存区，直接将工作区中的修改提交到 `Git` 仓库，这时候 `Git` 工作的流程简化为了`工作区 → Git 仓库`

`Git` 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 `git commit` 加上 `-a` 选项，`Git` 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤：

```shell
git commit -a -m "描述信息"
```



##### 15、移除文件

从 Git 仓库中移除文件的方式有两种：

① 从 Git 仓库和工作区中**同时移除**对应的文件

② 只从 Git 仓库中移除指定的文件，但保留工作区中对应的文件

```shell
# 从 Git仓库和工作区中同时移除 index.js 文件
git rm -f index.js
# 只从 Git 仓库中移除 index.css，但保留工作区中的 index.css 文件
git rm --cached index.css
```

绿色的 D 表示文件已经移除，下次提交时候删除



##### 16、忽略文件

一般我们总会有些文件无需纳入 `Git` 的管理，也不希望它们总出现在未跟踪文件列表。 在这种情况下，我们可以创建一个名为 `.gitignore` 的配置文件，列出要忽略的文件的匹配模式。

文件 `.gitignore` 的格式规范如下：

① 以 **# 开头**的是注释

② 以 **/ 结尾**的是目录

③ 以 **/ 开头**防止递归

④ 以 **! 开头**表示取反

⑤ 可以使用 **glob 模式**进行文件和文件夹的匹配（glob 指简化了的正则表达式）

- **星号 \*** 匹配**零个或多个任意字符**
- **`[abc]`** 匹配**任何一个列在方括号中的字符** （此案例匹配一个 a 或匹配一个 b 或匹配一个 c） 
- **问号 ?** 只匹配**一个任意字符**
- **两个星号 \**** 表示匹配**任意中间目录**（比如 a/**/z 可以匹配 a/z 、 a/b/z 或 a/b/c/z 等）
- 在方括号中使用**短划线**分隔两个字符， 表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）

 `.gitignore` 文件的例子

<img src="./images/忽略清单.png" style="width: 50%;">



##### 17、查看提交历史

如果希望回顾项目的提交历史，可以使用 `git log` 这个简单且有效的命令

```shell
# 按时间先后顺序列出所有的提交历史，最近的提交在最上面
git log

# 只展示最新的两条提交历史，数字可以按需进行填写
git log -2

# 在一行上展示最近两条提交历史的信息
git log -2 --pretty=oneline

# 在一行上展示最近两条提交历史信息，并自定义输出的格式
# &h 提交的简写哈希值  %an 作者名字  %ar 作者修订日志  %s 提交说明
git log -2 --pretty=format:"%h | %an | %ar | %s"
```



##### 18、回退到指定的版本

```shell
# 在一行上展示所有的提交历史
git log --pretty=oneline

# 使用 git reset --hard 命令，根据指定的提交 ID 回退到指定版本
git reset --hard <CommitID>

# 在旧版本中使用 git reflog --pretty=oneline 命令，查看命令操作的历史
git reflog --pretty=onelone

# 再次根据最新的提交 ID，跳转到最新的版本
git reset --hard <CommitID>
```





### GIt 第二天

#### 今日目标

- 能够使用 `Github` 创建和维护远程仓库
- 能够掌握 `Git` 分支的基本使用



#### 一、了解开源相关的概念

##### 1、什么是开源

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%BC%80%E6%BA%90.png" style="width: 70%;">

**通俗的理解**

- **开源** 是指不仅提供程序还提供程序的源代码
- **闭源** 是只提供程序，不提供源代码

<span style="color:red;"></span>

##### 2、什么是开源许可协议

开源并不意味着完全没有限制，为了**限制使用者的使用范围**和**保护作者的权利**，每个开源项目都应该遵守开源

许可协议（ `Open Source License` ）。

常见的 5 种开源许可协议：

- `BSD`（Berkeley Software Distribution） 
- `Apache Licence 2.0`
- <span style="color:red;">**`GPL`**</span>（GNU General Public License） (⭐⭐⭐)
  - 具有传染性的一种开源协议，不允许修改后和衍生的代码做为闭源的商业软件发布和销售
  - 使用 `GPL` 的最著名的软件项目是：Linux
- `LGPL`（GNU Lesser General Public License） 
- <span style="color:red;">**`MIT`**</span>（Massachusetts Institute of Technology, MIT）  (⭐⭐⭐)
  - 是目前限制最少的协议，唯一的条件：在修改后的代码或者发行包中，必须包含原作者的许可信息
  - 使用 MIT 的软件项目有：`jquery`、`Node.js `;



##### 3、为什么要拥抱开源

开源的核心思想是“**我为人人，人人为我**”，人们越来越喜欢开源大致是出于以下 3 个原因：

① 开源给使用者更多的控制权

② 开源让学习变得容易

③ 开源才有真正的安全

开源是软件开发领域的大趋势，**拥抱开源就像站在了巨人的肩膀上**，不用自己重复造轮子，让开发越来越容易



##### 4、开源项目托管平台

专门用于免费存放开源项目源代码的网站，叫做**开源项目托管平台**。目前世界上比较出名的开源项目托管平台

主要有以下 3 个：

- `Github`（全球最牛的开源项目托管平台，没有之一）
- `Gitlab`（对代码私有性支持较好，因此企业用户较多）
- `Gitee`（又叫做码云，是国产的开源项目托管平台。访问速度快、纯中文界面、使用友好）

**注意：**以上 3 个开源项目托管平台，只能托管以 `Git` 管理的项目源代码，因此，它们的名字都以 `Git` 开头



#### 二、GitHub

##### 1、什么是 GitHub

`Github` 是全球最大的**开源项目**托管平台。因为只支持 `Git` 作为唯一的版本控制工具，故名 `GitHub`。 

在 `Github` 中，你可以：

① 关注自己喜欢的开源项目，为其点赞打 `call` 

② 为自己喜欢的开源项目做贡献（`Pull Request`） 

③ 和开源项目的作者讨论 Bug 和提需求 （`Issues`） 

④ 把喜欢的项目复制一份作为自己的项目进行修改（`Fork`） 

⑤ 创建属于自己的开源项目

⑥ etc…

So，**`Github ≠ Git`**



##### 2、注册 GitHub 账号的流程

① 访问 `Github` 的官网首页 https://github.com/

② 点击“`Sign up`”按钮跳转到注册页面

③ 填写可用的用户名、邮箱、密码

④ 选出对应的图片

⑤ 点击“`Continue`”按钮注册新用户

⑥ 登录到第三步填写的邮箱中，点击激活链接，完成注册

最新的GitHub注册界面，界面为英文，右键进行翻译如下：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E6%B3%A8%E5%86%8CGitHub.png" style="width: 40%;">





##### 3、新建空白远程仓库

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%88%9B%E5%BB%BA%E4%BB%93%E5%BA%93.png" style="width: 80%;">

成功后显示：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E6%88%90%E5%8A%9F%E5%88%9B%E5%BB%BA%E4%BB%93%E5%BA%93.png" style="width: 80%;">



##### 4、远程仓库的两种访问方式

`Github` 上的远程仓库，有两种访问方式，分别是 `HTTPS` 和 `SSH`。它们的区别是：

① `HTTPS`：**零配置**；但是每次访问仓库时，需要重复输入 `Github` 的账号和密码才能访问成功

② `SSH`：**需要进行额外的配置**；但是配置成功后，每次访问仓库时，不需重复输入 `Github` 的账号和密码

**注意：**在实际开发中，**推荐使用 SSH 的方式访问远程仓库。**



##### 5、基于 HTTPS 将本地仓库上传到 Github

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/https%E6%8F%90%E4%BA%A4.png" style="zoom:90%;" />





##### 6、基于 SSH key

- SSH key

  `SSH key` 的**作用**：实现本地仓库和 `Github` 之间免登录的加密数据传输。

  `SSH key` 的**好处**：免登录身份认证、数据加密传输。

  `SSH key` 由**两部分组成**，分别是：

  ① `id_rsa`（私钥文件，存放于客户端的电脑中即可）

  ② `id_rsa.pub`（公钥文件，需要配置到 `Github` 中）



- 生成 SSH key

  ① 打开 Git Bash

  ② 粘贴如下的命令，并将 `your_email@example.com` 替换为注册 `Github` 账号时填写的邮箱：

  ```shell
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```

  ③ 连续敲击 3 次回车，即可在 `C:\Users\用户名文件夹\.ssh` 目录中生成 `id_rsa` 和 `id_rsa.pub` 两个文件



##### 7、配置 SSH key

① 使用记事本打开 `id_rsa.pub` 文件，复制里面的文本内容

② 在浏览器中登录 `Github`，点击头像 -> `Settings -> SSH and GPG Keys -> New SSH key`

③ 将 `id_rsa.pub` 文件中的内容，粘贴到 `Key` 对应的文本框中

④ 在 `Title` 文本框中任意填写一个名称，来标识这个 `Key` 从何而来



##### 8、检测 Github 的 SSH key 是否配置成功

打开 `Git Bash`，输入如下的命令并回车执行：

```shell
ssh -T git@gitee.com
```

上述的命令执行成功后，可能会看到如下的提示消息：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/ssh%E9%85%8D%E7%BD%AE%E6%A3%80%E6%9F%A5.png" style="zoom:100%;" />

输入 yes 之后，如果能看到类似于下面的提示消息，证明 SSH key 已经配置成功了：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/ssh%E9%85%8D%E7%BD%AE%E6%A3%80%E6%9F%A501.png" style="zoom:100%;" />



##### 9、基于 SSH 将本地仓库上传到 Github

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%9F%BA%E4%BA%8ESSH%E4%B8%8A%E4%BC%A0%E5%88%B0github.png" style="zoom:100%;" />

**注意：** `git push origin master` 也能进行提交，`git push origin -u` 的话可以提交代码，并且把`origin` 当作默认的主机，后续直接 `git push` 就可以提交到`origin`对应的主机



##### 10、将远程仓库克隆到本地

打开 `Git Bash`，输入如下的命令并回车执行：

```shell
git clone 远程仓库的地址
```



#### 三、Git 分支

##### 1、分支的概念

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习`SVN`。如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了`Git`又学会了`SVN`！

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%88%86%E6%94%AF%E7%9A%84%E6%A6%82%E5%BF%B5.png" style="zoom:100%;" />

##### 2、分支在实际开发中的作用

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%88%86%E6%94%AF%E7%9A%84%E4%BD%9C%E7%94%A8.png" style="zoom:100%;" />



##### 3、master 主分支（main）

在初始化本地 `Git` 仓库的时候，`Git` 默认已经帮我们创建了一个名字叫做 `master` 的分支。通常我们把这个`master` 分支叫做主分支。

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E4%B8%BB%E5%88%86%E6%94%AF.png" style="zoom:100%;" />

在实际工作中，`master` 主分支的作用是：**用来保存和记录整个项目已完成的功能代码**。

因此，**不允许程序员直接在 `master` 分支上修改代码**，因为这样做的风险太高，容易导致整个项目崩溃。



##### 4、功能分支

由于程序员不能直接在 `master` 分支上进行功能的开发，所以就有了功能分支的概念。

**功能分支**指的是专门用来开发新功能的分支，它是临时从 `master` 主分支上分叉出来的，当新功能开发且测试

完毕后，最终需要合并到 `master` 主分支上，如图所示：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%8A%9F%E8%83%BD%E5%88%86%E6%94%AF.png" style="zoom:100%;" />



##### 5、查看分支列表

使用如下的命令，可以查看当前 Git 仓库中所有的分支列表：

```shell
git branch
```

运行的结果如下所示：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E6%9F%A5%E7%9C%8B%E5%88%86%E6%94%AF.png" style="zoom:100%;" />

**注意：**分支名字前面的 ***** 号表示当前所处的分支。



##### 6、创建新分支

使用如下的命令，可以**基于当前分支**，**创建一个新的分支**，此时，新分支中的代码和当前分支完全一样：

```shell
git branch 分支名称
```

图示如下：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%88%9B%E5%BB%BA%E5%88%86%E6%94%AF.png" style="zoom:100%;" />



##### 7、切换分支

使用如下的命令，可以**切换到指定的分支上**进行开发：

```shell
git checkout login
```

图示如下：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF.png" style="zoom:100%;" />



##### 8、分支的快速创建和切换

使用如下的命令，可以**创建指定名称的新分支**，并**立即切换到新分支上**：

```shell
# -b 表示创建一个新分支
# checkout 表示切换到刚才新建的分支上
git checkout -b 分支名称
```

图示如下：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%BF%AB%E9%80%9F%E5%88%9B%E5%BB%BA%E5%B9%B6%E4%B8%94%E5%88%87%E6%8D%A2.png" style="zoom:100%;" />

**注意：**

"`git checkout -b 分支名称`" 是下面两条命令的简写形式：

① `git branch` 分支名称

② `git checkout` 分支名称



##### 9、合并分支

功能分支的代码开发测试完毕之后，可以使用如下的命令，将完成后的代码合并到 `master` 主分支上：

```shell
# 1. 切换到 master 分支
git checkout master
# 2. 在master 分支上运行 git merge 命令，将 login 分支的代码合班到 master 分支
git merge login
```

图示如下：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%90%88%E5%B9%B6%E5%88%86%E6%94%AF.png" style="zoom:100%;" />

**合并分支时的注意点**：

假设要把 C 分支的代码合并到 A 分支，则必须**先切换到 A 分支**上，**再运行 git merge 命令**，来合并 C 分支！



##### 10、删除分支

当把功能分支的代码合并到 `master` 主分支上以后，就可以使用如下的命令，删除对应的功能分支：

```shell
git branch -d 分支名称
```

图示如下：

<img src="F:/%E9%BB%91%E9%A9%AC%E8%AF%BE%E7%A8%8B/%E5%B0%B1%E4%B8%9A%E7%8F%AD/09git/git%E7%AC%94%E8%AE%B0/images/%E5%88%A0%E9%99%A4%E5%88%86%E6%94%AF.png" style="zoom:100%;" />

**注意：**想要删除分支，必须要先切换到主分支



##### 11、遇到冲突时的分支合并

如果**在两个不同的分支中**，对**同一个文件**进行了**不同的修改(commit)**，Git 就没法干净的合并它们。 此时，我们需要打开这些包含冲突的文件然后**手动解决冲突**。

```shell
# 假设：在把 reg 分支合并到 master 分支期间
git checkout master
git merge reg

# 打开包含冲突的文件，手动解决冲突之后，再执行如下命令
git add .
git commit -m "解决了分支合并冲突的问题"

```



##### 12、将本地分支推送到远程仓库

如果是**第一次**将本地分支推送到远程仓库，需要运行如下的命令：

```shell
# -u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例
git push -u origin payment:pay

# 如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化
git push -u origin payment
```

**注意：**第一次推送分支需要带 **-u 参数**，此后可以直接使用 `git push` 推送代码到远程分支。



##### 13、查看远程仓库中所有的分支列表

通过如下的命令，可以查看远程仓库中，所有的分支列表的信息：

```shell
git remote show 远程仓库名称
```



##### 14、跟踪分支

跟踪分支指的是：从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下：

```shell
# 示例
git checkout pay

# 从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
git checkout -b 本地分支名称 远程仓库名称/远程分支名称

# 示例
git checkout -b payment origin/pay
```



##### 15、拉取远程分支的最新的代码

可以使用如下的命令，把远程分支最新的代码下载到本地对应的分支中:

```shell
# 从远程仓库，拉取当前分支最新的代码，保持当前分支的代码和远程分支代码一致
git pull
```



##### 16、删除远程分支

可以使用如下的命令，删除远程仓库中指定的分支：

```shell
# 删除远程仓库中，制定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称

# 示例
git push origin --delete pay
```
































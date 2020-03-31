一、Git简介

### 1. 什么是Git

`Git`是一个开源的分布式的版本控制软件。

那什么是版本控制呢？

我们之前肯定做过类似这样的操作：

![1585370145247](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585370145247.png)

![1585370234875](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585370234875.png)

背后故事：

~~~

~~~

### 2. 集中式和分布式

集中式代表：SVN

集中式特点：

版本库是集中存放在中央服务器的。

必须实时联网才能工作。

分布式代表：Git

分布式特点：

个人电脑都可以作为版本库

速度快，使用简单

不必实时联网。









![1585297601286](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585297601286.png)



使用版本控制，可以保留之前所有的版本，以便回滚和修改。



安装Git，参考https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git





## 二、Git使用

安装成功后会在开始菜单出现3个相关程序：

![1585374289137](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585374289137.png)

**Git Bash：**`Linux`风格的命令行，使用最多，推荐使用。

![1585374417699](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585374417699.png)

**Git CMD：**`Windows`风格的命令行。

![1585374456353](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585374456353.png)

**Git GUI**：自带的图形界面的`Git`，不建议初学者使用，尽量先熟悉常用命令。

![1585374487351](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585374487351.png)

点击`Create New Repository`可以直接创建一个新的仓库。



我们用的最多的是`Git Bash`，在里面可以使用`linux`命令进行操作。





![1585297931809](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585297931809.png)



![1585298003591](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585298003591.png)



为什么有暂存区，避免一个个直接提交，先临时保存好多，然后再往上推。

1、安装好后，首次使用需要进行全局配置，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中。

~~~bash
git config --global user.name "用户名"  # 建议使用github上注册的
git config --global user.email "邮箱地址"

# 查看当前用户配置
git config --global --list
~~~

2、创建仓库
当我们需要让`Git`去管理某个新项目/已存在项目的时候，就需要创建仓库了。注意，创建仓库时使用的目录不一定要求是空目录，选择一个非空目录也是可以的，目录最好不要是中文，避免不必要的乱码，但是不建议在现有项目上来学习`Git`。
`Git`仓库初始化：

~~~bash
# 进入一个目录，新建空目录或者进入已有目录
$ mkdir demo

# 进入空目录
$ cd demo
# 初始化仓库
git init  # 让Git知道，它需要来管理这个目录
~~~

执行之后会在项目目录下创建`.git`的隐藏目录，这个目录是`Git`所创建的，不能删除，也不能随意更改其中的内容。

![1585380708886](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585380708886.png)

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

3、添加到暂存区
我们在目录`demo`下新建一个文件`index.html`。

![1585381406786](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585381406786.png)

内容如：

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>老P之娱</title>

</head>
<body>
    <ul>
		<li>推荐</li>
		<li>影视</li>
		<li>音乐</li>
	</ul>
</body>
</html>
~~~

我们提交到暂存区：

~~~bash
# git add指令，可以添加一个文件，也可以同时添加多个文件。
# git add 文件名
# git add 文件名1 文件名2 文件名3...
# git add .       # 添加当前目录到缓存区中
git add index.html
~~~

4、提交至本地仓库

~~~bash
# git commit -m "注释内容"
git commit -m "第一次提交"
~~~

![1585381783533](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585381783533.png)

`git status`查看状态，会提醒接下来可能要的操作。



现在我们要新增模块，增加一个“直播”

~~~html
...
<li>直播</li>
....
~~~

增加完毕进行提交。

~~~bash
git add index.html
git commit -m "增加直播模块"
~~~



目前应用功能的样子

![1585382357563](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585382357563.png)

随着市场的越来越好，应用需要不断的迭代升级，现在根据市场需求，我们又继续开发一个功能“附近”。

~~~bash
# 修改应用

# 2.提交
git add index.html
git commit -m "增加附近模块"
~~~

截至目前功能有：

![1585382579375](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585382579375.png)

投入市场，果不其然流量暴增，但是慢慢的被监管部门注意到，说打擦边球，被叫去喝茶，需要将其“附近”功能下线。

这个时候，我们只需要将版本回退到增加"附近"之前的版本。

5、版本回退

~~~bash
# 1. 查看版本，确定需要回到的时间点
git log
git log --pretty=oneline   # 美化

# 2. 回退操作
git reset --hard 版本号
~~~

![1585383067389](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585383067389.png)

这样就将“附近”下线了，也不用将新增的代码删除。

![1585383116982](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585383116982.png)





就这样砍掉了“附近”的功能，流量随之暴跌，经过后续内部审核调整，准备重新上线“附近”功能。

![1585383369721](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585383369721.png)

我们查看日志，只有前面提交记录，那我们是不是得重新再写代码呢？当然不是，我们换种方式：

~~~bash
git reflog
git reset --hard 51ca6e7
~~~

![1585383604114](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585383604114.png)

![1585383641651](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585383641651.png)

再一次回到市场。



怎么从本地仓库直接提交到远程仓库（远程仓库不存在此仓库）。



怎么下载别人仓库的代码，是直接git clone别人仓库的名字，还是先fork到自己仓库，用自己仓库名字下载。



## 三、Git分支

1、查看分支

~~~bash
git branch
~~~

2、创建分支

~~~bash
git branch 分支名称
~~~

3、切换分支

~~~bash
git checkout 分支名称
~~~

![1585390429099](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585390429099.png)



此时已切换到`dev`分支上，我们来开发“电商”模块：

![1585394070484](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585394070484.png)

然后进行提交：

~~~bash
git add .
git commit -m "分支dev开发商城ing"
~~~

![1585395777687](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585395777687.png)



那我们再切换到主线上`master`。

![1585395849329](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585395849329.png)

我们再来看`index.html`内容：
![1585395895584](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585395895584.png)



我们切换到主线上，我们可以看到“电商”不见了，所以从主线上分离出来得，不影响主线。



工作继续进行着。

忽然有一天，线上出现`bug`，需要紧急修复【直播】的`bug`，以免影响生产。这个时候我们需要创建新的分支来处理`bug`。

~~~bash
git branch bug
git checkout bug
~~~

![1585397812141](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585397812141.png)



当创建新的分支的时候，会将`master`内容拷贝一份，内容都一样。

![1585397986912](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585397986912.png)



然后我们开始修复`bug`：
![1585398219732](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585398219732.png)

修复完之后，我们再提交：

~~~bash
git add .
git commit -m "直播bug修复"
~~~

此时bug修复完了，但只是在bug分支上修改完的。我们还需要合并到`master`分支。

~~~bash
# 1. 首先切换到master分支
git checkout master

# 2. 合并到master分支
git merge bug   # 注意切换分支再合并
~~~

![1585400511940](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585400511940.png)

合并的时候，可能弹出

![1585467814400](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585467814400.png)

可以不管(直接下面3,4步)，如果要输入解释的话就需要:

1. 按键盘字母 i 进入insert模式；
2. 修改最上面那行黄色合并信息,可以不修改；  **// 黄色内容为默认的合并信息；**
3. 按键盘左上角"Esc"；
4. 输入`:wq`，进行修改后保存退出,然后按回车键即可。



我们再看看内容，合并到没：
![1585400548854](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585400548854.png)

这样`bug`修复上线使用了，稳稳当当的，`bug`分支已经没有用了，我们可以删除分支：

~~~bash
# git branch -d 分支名称
git branch -d bug
~~~

![1585400698695](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585400698695.png)



`bug`修复完了，那我们继续开发`商城`模块，切换到`dev`分支

~~~bash
git checkout dev
~~~

可以看到，上面在`bug`分支修改的以及后续合并到`master`分支的内容，并没有影响`dev`分支上的内容：

![1585400982602](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585400982602.png)

我们继续开发 商城功能，将其完成：

![1585401078480](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585401078480.png)



然后提交：

~~~bash
git add .
git commit -m "商城开发完成"
~~~

![1585401384385](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585401384385.png)



商城开发完后，我们要合并到主线`master`上。

~~~bash
# 1. 切换到主线
git checkout master

# 2. 合并到master分支
git merge dev   # 注意切换分支再合并
~~~

这里合并可能会产生冲突。



![1585316026167](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585316026167.png)







## 五、冲突产生与解决

场景模拟：

① 同事A在下班之后修改了线上仓库的代码。

此时我本地仓库的内容与线上不一致的。

② 第二天上班，我没有git pull 操作，而是直接修改本地对应文件。



③下班时，我将本地仓库代码git push。

提示我们要在push之前先git pull操作。

【解决冲突】

④先git pull

此时git已经将线上与本地仓库的冲突合并了。

⑤打开冲突文件，解决冲突

解决办法：需要和相关同事进行商量，看代码如何修改，在此提交即可。

⑥重新提交



## 三、使用远程仓库

### 3.1 介绍

随着业务不断的扩大，需要租个办公室像个正规公司一样上班了，但是经常敲代码不止是在公司，回家照样要敲代码，因为经常背着电脑上下班，地铁又挤，所以大出血，买了一台电脑放公司，这样就需要2个地方进行代码同步，我们可以使用U盘来回copy，但是这样已经过时了，我们也可以使用类似各种云盘也是可以，但是对于代码，有更好的选择，可以使用`GitHub`，码云，甚至`GitLab`自己搭建。这样我们可以将代码上传到远程仓库，到另外一个地方拉取进行修改，再上传同步。

![1585402732078](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585402732078.png)



我们这里使用`GitHub`。

### 3.2 远程仓库创建

首先，需要注册账号，并创建远程仓库。

![1585404699976](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585404699976.png)

填写相关信息：

![1585404788641](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585404788641.png)

点击【`Create repository`】

![1585405161727](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585405161727.png)

远程仓库已经创建完成，接下来，我们要将前期在出租屋完成的项目代码提交到远程仓库中。

~~~bash
git remote add origin https://github.com/juehuan182/demo.git  # 远程仓库取别名
git push -u origin master  # 提交到远程仓库， -u默认，可以省略
~~~

如果没有配置账号密码，则会弹出窗口需要输入账号密码。

![1585405424399](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585405424399.png)



![1585405542534](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585405542534.png)

这样我们就已经推到远程仓库了。

![1585405646332](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585405646332.png)

现在只推送了`master`分支，那我们也可以将分支推上来。

~~~bash
git push -u origin master  # 将分支dev提交到远程仓库
~~~

![1585405802124](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585405802124.png)



我们已经将出租屋开发的代码同步到远程仓库了，现在要去公司上班了，第一天斗志昂扬，打开新买的电脑，初次需要将远程仓库代码拉到本地开干，比如我们要将代码直接拉到D盘下。

~~~bash
# 1. 进入d盘
cd d:
# 2. 开始克隆远程仓库
git clone https://github.com/juehuan182/demo.git
~~~

![1585406451042](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585406451042.png)

拉取下来，我们可以看到：

![1585406587005](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585406587005.png)

我们查看分支：

![1585406690276](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585406690276.png)

显示的只有主分支，其实clone已经将分支也克隆下来了，我们可以切换当分支看看。

![1585406821544](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585406821544.png)



我们在公司下载完代码后，继续开发功能：

~~~bash
# 1. 切换到dev分支
git checkout dev

# 2. 将主线master合并到dev分支，只一次。
git merge master
~~~

![1585407219595](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585407219595.png)



准备下班了，提交代码

~~~bash
git add .
git commit -m "短视频--【公司1%】"
git push origin dev    # 之前在家里已经取别名了，公司拿来直接用就行了。
~~~

![1585407615843](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585407615843.png)

代码上传完，下班回家。



回到家，继续写代码，这个时候，首先需要更新代码，毕竟在公司下班的时候已经提交了代码，否则会导致家里的和远程仓库不一致出现冲突。

~~~bash
# 1. 切换到dev分支
git checkout dev
# 2. 拉取最新代码
git pull origin dev
~~~

![1585407959365](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585407959365.png)



在出租屋继续加班加点，拼命干。。。。

![1585462823517](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585462823517.png)

肝到凌晨了，狗命要紧，赶紧提交代码，睡觉

~~~bash
git add .
git commit -m "短视频--【出租屋50%】"
git push origin dev
~~~

![1585463238060](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585463238060.png)

睡觉。。。

一觉睡到天亮，继续去公司，忙着将功能开发完成。

打开公司电脑，开干，公司电脑项目还是昨天下班完成的，下班在家加班的代码还没同步过来。

![1585463369125](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585463369125.png)

我们需要同步最新代码

~~~bash
# 1. 切换到dev分支
git checkout dev
# 2. 拉最新代码，不必再clone，因第一次也已经克隆了，只需pull最新代码
git pull origin dev
~~~

![1585463470072](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585463470072.png)

同步完成继续，马不停蹄的撸代码

![1585463543841](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585463543841.png)

![1585464123031](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585464123031.png)

终于完工，提交代码

~~~bash
git add .
git commit -m "短视频开发完成"
git push origin dev
~~~

开发完毕，准备上线了，需要将dev分支代码合并到主分支master上。

~~~bash
# 1. 切换到master分支
git checkout master
# 2. 合并dev到主分支
git merge dev
# 3. 推送
git push origin master
~~~

一般也最好将dev分支也推送到远程

~~~bash
# 1. 切换到master分支
git checkout master
# 2. 合并
git merge dev
git push origin master
~~~

记得，家里代码要同步

~~~bash
# 拉master
git checkout master
git pull origin master

# 拉dev
git checkout dev
git pull origin dev
~~~

就这样，完成了公司和家里两边开发。

公司业务越来越大，工作之余，钱也有了，现在就缺个妹子，有钱就不怕没妹子，没过多久，找了一个身材脸蛋都不错的妹子，就这样他们幸福快乐的一起约会，看电影。

有一天P正在公司写代码

~~~bash
git checkout dev
git pull origin dev
~~~

突然妹子跑过来，说电影都要开始了，怎么还不走，P说等下，再过几分钟，最后经不住妹子的嗲，直接忘记push，就关电脑了。

![1585466198019](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585466198019.png)

~~~bash
git add .
git commit -m "公司开发新闻模块"

# 忘记push了
~~~

和妹子看完电影，又吃饭，，，妹子叫您去她家坐一会，但是你总是惦记心爱的代码，于是说改天吧，赶紧打个的回家。

~~~bash
git checkout dev
git pull origin dev
~~~

![1585466497444](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585466497444.png)

拉取最新代码之后，才发现公司开发的模块“新闻”忘记提交了，但是时间又来不及重新写，只好先开发其他功能再说。

![1585466723900](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585466723900.png)



提交代码，睡觉

~~~bash
git add .
git commit -m "在家开发吃货以及需求文档"
git push origin dev
~~~

夜已深，赶紧去梦里约会

第二天照常，来到公司周而复始的开电脑，拉代码开干。

~~~bash
git checkout dev
git pull origin dev
~~~

![1585466978147](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585466978147.png)

提示有冲突，这是因为昨天晚上忘记提交代码，下班在家里拉取的没同步在公司修改的，现在拉到本地有合并，可能产生冲突。`index.html`文件产生冲突，因为在家和公司都修改了这个文件，而另外个`吃货模块开发文档.md`，因为是新增的文件所以不会产生冲突。

怎么解决冲突呢？直接手动解决，找到公司电脑这个文件。

![1585467451120](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585467451120.png)

确认哪些不必要的，手工删除

![1585467481689](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585467481689.png)

继续开发新功能，下班记得提交代码到远程仓库。

~~~bash
git add .
git commit -m "解决公司与家里合并冲突问题"
git push origin dev
~~~



## 多人协同开发

随着公司业务不但扩展，发展前景越来越好，老P感觉独立作战越来越有心无力了，需要扩大公司规模，招几个小弟来开发了，自己脱离敲代码的阶段，是时候站出来，全局看待公司发展。

招了2个小弟，小A和小B，准备开始做游戏模块了，老P首先创建一个项目

~~~bash
# 查看当前路径
$ pwd
/d/Learn

# 创建项目目录
$ mkdir Games

# 进入项目
$ cd Games

# 初始化
$ git init
# 查看文件信息
$ ls -alh
total 8.0K
drwxr-xr-x 1 44801 197609 0  3月 30 12:07 ./
drwxr-xr-x 1 44801 197609 0  3月 30 12:07 ../
drwxr-xr-x 1 44801 197609 0  3月 30 12:07 .git/

# 开始创建应用
$ touch main.py

# 添加到暂存区
git add .
# 提交本地库
git commit -m '游戏app项目启动'
~~~

现在老P已经添加到本地库去了，要想让小弟们开发，还需要在GitHub上创建一个远程仓库。

有2种方式，1种直接像之前一样创建远程仓库，

![1585542045010](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585542045010.png)

![1585542207390](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585542207390.png)



![1585542253701](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585542253701.png)

这样对方就会收到一封邀请的邮件，同意加入。不过这种方式适合于个人。

在公司一般团体，更多倾向于组织的形式。

![1585542340623](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585542340623.png)

![1585542832072](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585542832072.png)

可以看到这里需要钱，这里拿免费的来演示，我们选第一个

![1585543458080](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585543458080.png)

我这选择个人，

![1585544878820](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585544878820.png)

创建完成： 

![1585545323426](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585545323426.png)

现在我们在这个组织下面创建我们的仓库：

![1585547574159](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585547574159.png)

创建仓库过程同之前操作

![1585547646394](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585547646394.png)

创建完成，老P需要将新建的游戏项目推送到远程仓库：

~~~bash
git remote add origin https://github.com/qmpython/Games.git
git push -u origin master
~~~

![1585547928549](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585547928549.png)

推送完成。

我们看看之前提交的记录：
![1585548371782](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585548371782.png)

commit id是个哈希值，太长，我们可以使用tag进行版本号控制。

~~~bash
git tag -a v1 -m "基线版"   # 本地创建tag信息
git push origin --tags    # 将本地tag信息推送到远程仓库
~~~

![1585548488394](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585548488394.png)



![1585548230673](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585548230673.png)

![1585548259078](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585548259078.png)



一切就绪，现在要分派任务给小弟了，先创建一个分支用于开发：

~~~bash
git checkout -b dev    # 创建并切换分支
git push origin dev    # 将本地分支推送到远程仓库

~~~

现在就准备邀请小弟加入组织了：

![1585548981300](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585548981300.png)

![1585548999477](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585548999477.png)



![1585549035333](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585549035333.png)

![1585549069568](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585549069568.png)

被邀请人会收到一封邮件：

![1585549145834](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585549145834.png)

如果看不到，则需对方将当前的组织的链接发给你的成员<https://github.com/Organization_Name>在页面上面图片中的信息，点击View invitation然后加入该组织

![1585570846875](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585570846875.png)

![1585570903684](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585570903684.png)

用同样方法可以邀请另外成员。

管理员登录，查看组织，可看到成员对组织默认只有可读权限。

![1585571346023](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585571346023.png)

我们进入仓库，邀请小弟加入该仓库：

![1585571542414](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585571542414.png)

邀请成员，并给可写权限：
![1585571620447](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585571620447.png)

这样我们现在已经邀请完成，开始给小弟分发任务了，将仓库地址发给小A：

~~~bash
# 1. 在D盘新建目录xjkp_a
mkdir xjkp_a
# 2. 进入目录
cd xjkp_a 
# 3. 克隆仓库
git clone https://github.com/qmpython/Games.git

# 4. 进入仓库
cd Games
# 5. 进入dev分支
git checkout dev
# 6. 在dev分支中再独立出一个分支xjkp
git checkout -b xjkp
# 7. 进行开发
touch xjkp.py
# 提交
git add .
git commit -m "小鸡快跑游戏开发"
git push origin xjkp
~~~

![1585572645665](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585572645665.png)

游戏开发完成，现在要来做代码`reviews`，老P登录github进行配置规则：

![1585572837917](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585572837917.png)

![1585572974551](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585572974551.png)

![1585573016937](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573016937.png)



同理要合并到master上也要添加一条规则，这里省略不写了。

小弟登录github进入项目，进行reviews请求：

![1585573349329](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573349329.png)

![1585573703754](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573703754.png)

请求完成：

![1585573774016](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573774016.png)



需要leader老P去reviews了：

![1585573899011](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573899011.png)

![1585573934061](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573934061.png)

![1585573971759](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585573971759.png)

![1585574100508](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574100508.png)

查看文件代码，勾选viewed表示已查看了。

也可以命令方式reviews
![1585574192262](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574192262.png)

![1585574247452](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574247452.png)

这里我们直接在网页上：

![1585574273192](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574273192.png)

![1585574329010](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574329010.png)

确定完之后，表示已经将`xjkp`分支合并到`dev`分支了：

![1585574364093](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574364093.png)

我们来查看dev分支是否合并成功：

![1585574482981](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574482981.png)

已经合并成功了。

合并后，我们可以将`xjkp`分支删除：

![1585574560085](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585574560085.png)



## Git免密登录

之前我们push的时候都需要输入用户和密码，比较麻烦，我们可以免密登录。

* URL中体现

  ~~~bash
  # 将原来的地址
  https://github.com/juehuan182/demo.git
  # 改成
  https://用户名:密码@github.com/juehuan182/demo.git
  
  # 结果变成这样：
  git remote add origin https://用户名:密码@github.com/juehuan182/demo.git
  git push origin master
  ~~~

  由于直接是基于`HTTPS`的，如果对于已有的，可以在`git/config`里修改地址：
  ![1585634680341](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585634680341.png)

  

* 基于SSH实现

  ~~~bash
  # 1. 生成公钥私钥，在git bash中使用命令生成
  ssh-keygen # 默认放在~/.ssh目录下，id_rsa.pub公钥，id_rsa私钥
  
  # 2. 拷贝公钥内容，并设置到github中
  
  # 3. 在git本地中配置ssh地址
  git remote add origin git@github.com:juehuan182/demo.git
  git push origin master
  ~~~

  ①生成公钥私钥

![1585636096127](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636096127.png)

​		②拷贝公钥内容

![1585636212236](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636212236.png)

添加到`github`中：
![1585636275662](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636275662.png)

![1585636368683](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636368683.png)



![1585636380024](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636380024.png)

添加成功：

![1585636421349](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636421349.png)

后续使用SSH地址：
![1585636725373](C:\Users\44801\AppData\Roaming\Typora\typora-user-images\1585636725373.png)

### 六、忽略文件

场景：有时候我们即使改动了内容，但是我们也不想提交到远程仓库，比如我博客配置文件，里面都涉及到实际真实数据，我不可能将其提交到远程仓库，让别人看到，这样容易引起攻击，此时我们可以使用“忽略文件”的机制来控制。

~~~bash
# 1. 新建一个 .gitignore的文件，用于声明忽略文件或不忽略文件的规则，规则对当前目录及子目录生效。
touch .gitignore    #   该文件因为没有文件名，没办法直接在windows下直接创建，使用命令方式

# 2. 编写规则：
/js/      # 过滤掉整个js文件夹
*.css	    # 过滤掉所有.css文件
/js/test.js    # 过滤某个具体文件
!index.html    # 不过滤具体某个文件

# 在忽略文件中，以#开头都是注释。
~~~


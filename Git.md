**4.** ***\*Git命令行操作\****

4.1本地库初始化

命令：git init

效果：

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps1.jpg) 

注意：.git目录中存放的是本地库相关的子目录和文件，不要删除也不要胡乱修改。

 

4.2设置签名

形式：

用户名：tom

Email地址：[goodMorning@atguigu.com](mailto:goodMorning@atguigu.com)

作用：区分不同开发人员的身份

辨析：这里设置的签名和登录远程库（代码托管中心）的账号、密码没有任何关系

命令：

项目级别/仓库级别：仅在当前本地库范围内有效

git ***\*config\**** user.name tom_pro

git ***\*confi\****g user.email [goodMorning_pro@atguigu.com](mailto:goodMorning_pro@atguigu.com)

信息保存的位置：./.git/config文件

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps2.jpg) 

系统用户级别：登录当前操作系统的用户范围

git config ***\*--global\**** user.name tom_glb

git config ***\*--global\**** user.email [goodMorning_glb@atguigu.com](mailto:goodMorning_glb@atguigu.com)

信息保存的位置：~/.gitconfig文件

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps3.jpg) 

级别优先级：

就近原则：  （1）项目级别优先于系统用户级别，二者都有时，采用项目							  级别的签名；

（2）如果只有系统用户级别签名，就以系统用户级别为准；

（3）二者都没有，不允许，会报错。

 

4.3 基本操作

4.3.1状态查看操作

git status

查看工作区、暂存区状态

4.3.2添加操作

git add [file name]

将工作区的“新建/修改”添加到暂存区

4.3.3提交操作

git commit -m “commit message” [file name]

将暂存区的文件提交到本地库

 

 

 

 

 

 

 

 

4.3.4查看历史记录操作

git log 

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps4.jpg) 

多屏显示时的控制方式：

空格向下翻页，b向上翻页，q退出

git log --pretty=oneline

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps5.jpg) 

git log --oneline  只显示HEAD指针当前位置后面的历史版本

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps6.jpg) 

git reflog			显示所有历史版本

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps7.jpg) 

HEAD{移动到当前版本需要多少步}

 

 

4.3.5前进后退

本质

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps8.png)![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps9.jpg) 

①基于索引值操作[推荐]  配合git reflog

git reset --hard [局部索引值]

git reset --hard a6ace91

②使用^符号：只能后退  配合 git log --oneline

git reset --hard HEAD^^^  一个^表示后退一步

③使用~符号：只能后退

git reset --hard HEAD~3  数字表示后退的步数

4.3.6  reset命令的三个参数对比

--soft参数  绿字表示没有用commit提交到本地库的状态，把暂存区凸显出来

仅仅在本地库移动HEAD指针  cat

--mixed	  把工作区凸显出来

在本地库移动HEAD指针

重置暂存区

--hard

在本地库移动HEAD指针

重置暂存区

重置工作区

4.3.7 删除文件并找回

前提：删除前，文件存在时的状态提交到了本地库。

操作： git reset --hard [指针位置]

删除操作已经提交到本地库：指针位置指向该文件存在的历史记录

删除操作尚未提交到本地库：指针位置使用HEAD

 

4.3.8 比较文件差异

git diff [文件名]

将工作区中的文件和暂存区进行比较

git diff [本地库中历史版本][文件名]

将工作区的文件和本地库历史记录比较

不带文件名

比较工作区的多个文件

4.4 分支管理

4.4.1 什么是分支？

在版本控制过程中，使用多条线同时推进多个任务

4.4.2 分支的好处？

同时并行推进多个功能开发，提高开发效率

各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响，失败的分支删除重新开始即可。彼此独立，有利于开发过程中去试错。

 

4.4.3 分支操作

创建分支

git branch [分支名]

查看分支

git branch -v

切换分支

git checkout [分支名]

合并分支

第一步：切换到接受修改的分支（被合并，增加新内容）上

git checkout [接受的分支名]

第二步：执行merge命令

git merge [有新内容的分支名]

解决冲突

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps10.png)冲突的表现

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps11.png)![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps12.png)![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps13.png)![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps14.png)![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps15.png)![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps16.jpg) 

 

冲突的解决

（1）编辑文件，删除特殊符号

（2）把文件修改到满意的程度，保存退出

（3）git add [文件名]

（4）git commit -m “日志信息” 注意：此时commit不能带具体文件名

 

**5.** ***\*Git基本原理\****

**5.1** ***\*哈希\****

哈希是一个系列的加密算法，各个不同的哈希算法虽然加密强度不同，但是有以下几个共同点:


①不管输入数据的数据量有多大，输入同-一个哈 希算法，得到的加密结果长度固定。
②哈希算法确定，输入数据确定，输出数据能够保证不变I
③哈希算法确定，输入数据有变化，输出数据一定有变化，而且通常变化很大
④哈希算法不可逆

Git底层采用的是SHA-1算法。
	哈希算法可以被用来验证文件。原理如下图所示:

Git就是靠这种机制来从根本上保证数据完整性的。

 

**5.2** ***\*Git保存版本的机制\****

Git把数据看作是小型文件系统的一组快照，每次提交更新时Git都会对当前的全部文件制作一个快照并保存这个快照的索引。为了高效，如果文件没有修改，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件，所以Git的工作方式可以称之为快照流。

Git文件管理机制细节

 

**5.3** ***\*Git分支管理机制\****

 

**6.** ***\*Github\****

6.1 账号信息

修改头像

6.2 创建远程库

只需要给远程库起个名即可

6.3 创建远程库地址别名

git remote -v  查看当前所有远程库地址别名

git remote add [别名] [远程库地址]

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps17.jpg) 

 

6.4 推送操作

git push [别名][分支名]

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps18.jpg) 

6.5 克隆操作

git clone [远程地址]

![img](file:///C:\Users\Administrator\AppData\Local\Temp\ksohtml9356\wps19.jpg) 

效果：

（1）完整的把远程库下载到本地

（2）创建origin远程地址别名

（3）初始化本地库

6.6团队成员邀请

 

 

 

6.7拉取操作

pull=fetch+merge

git fetch [远程库地址别名][远程分支名]

git merge [远程库地址别名/远程分支名]

 

6.8 解决冲突

要点：	

（1）如果不是基于github远程库的最新版本所做的修改，不能推送，必须先拉取。

（2）拉取下来后如果进入冲突状态，则按照“分支冲突解决”操作解决即可。

类比：

债权人：老王（开发人员 不同的本地库）

债务人：小刘（github）

老王说10天后归还即可，小刘接受，双方达成一致。

老王媳妇说5天后归还，小刘不能接受，老王媳妇需要找老王确认后再执行。

 

 

 

 

 

 

 

 

 

 
# 实验一：开发者测试（3）
**GitStack地址：http://106.14.179.34/gitstack/**  
**username:admin  password:admin**  
**Jenkins地址：http://106.14.179.34:8086/**  
**username:zhengjinhui  password:123456**  
## 一.安装和配置Git代码仓库
根据实验手册从地址http://gitstack.com 中下载GitStack软件，安装成功后，在浏览器的地址栏里输入http://localhost/gitstack 就可以打开登录界面。登录后进入Repositories页面，通过Repositories页面视图，可以在服务器上创建新的空仓库。直接输入仓库名，然后点击Create按钮即可完成仓库的创建。创建好的仓库会在Repositories页面中显示出来，同时显示该仓库的clone地址：http://localhost/JenkinsTest.git。  
![1.png](https://i.loli.net/2018/11/23/5bf77e8d3b355.png)  
点击User&Group下的Users，通过Create Users创建用户。  
![2.png](https://i.loli.net/2018/11/23/5bf77ee2babb6.png)  
创建好用户后，点击Repositories，进入Repositories页面后，点击代管理仓库JenkinsTest对应的Action图标中间的两个小人的图标进入下图所示界面。  
![9.png](https://i.loli.net/2018/11/23/5bf77f0f40e95.png)  
 在该页面可以添加或删除具有访问JenkinsTest仓库权限的用户。通过Add user可添加读写用户，点击Action下的×图标可以删除曾经授权的用户。  
 ## 二.安装和配置Jenkins持续集成工具
 从Jenkins官网下载最新的Jenkins工具war包，在命令行输入Java命令“java -jar jenkins2.war --ajp13Port=-1 --httpPort=8086”可启动Jenkins且将Jenkins的运行端口改至8086端口。启动Jenkins后，在浏览器的地址栏输入“ http://localhost:8086 ”可以验证Jenkins工具是否正常启动。  
我第一次安装Jenkins的时候安装相关插件的时候部分失败了，出现了下图的页面。  
![10.png](https://i.loli.net/2018/11/23/5bf77f958b7b4.png)  
于是我卸载后重新下载了其他版本，最终所有插件都安装成功了，即Jenkins安装成功了。  
安装成功后，Jenkins正常启动，可看到如下页面。  
![14.png](https://i.loli.net/2018/11/23/5bf78019dcf58.png)  
在左侧导航栏里点击“系统管理”按钮，在如下页面中选择“全局工具配置”。  
![15.png](https://i.loli.net/2018/11/23/5bf78086e0ec0.png)  
进入全局工具配置页面后找到git配置项，在git配置项下的“Path to executable”一栏添加本机的git.exe程序路径即可完成设置，如下图。  
再找到Ant配置项，点击新增Ant按钮，在Name一栏填写ant，选择自动安装，再选择版本即可完成设置，如下图。  
![16.png](https://i.loli.net/2018/11/23/5bf7814a5ca12.png)  
以上配置提交保存后，返回上一页面，选择“系统设置”，进入系统设置页面后找到Git plugin配置项，填好user.name和user.email后提交保存。  
![17.png](https://i.loli.net/2018/11/23/5bf7820fe8ecb.png)  
在GitStack安装目录的git文件夹下，双击git-bash.exe，打开git命令行。切换到希望用来克隆服务器代码仓库的本地目录，使用git clone下载文件。完整的克隆命令为：$git clone http://localhost/JenkinsTest.git。  
执行该克隆命令后，控制台的输出信息如下图。  
![19.png](https://i.loli.net/2018/11/23/5bf782762ef69.png)  
完成克隆后，本地将有远程代码仓库中JenkinsTest项目的最新代码的一个副本。下面将更新JenkinsTest项目的代码。在克隆所得的JenkinsTest文件夹里，加入要添加的文件，产生一个对项目的更改。然后使用git push命令可将本地代码变更提交到远程代码仓库中，使变更真正进入项目的代码版本管理系统。  
具体Git代码提交命令如下所示：cd JenkinsTest  
                              git add .  
                              git commit -m “add files”  
                              git push  
![37.png](https://i.loli.net/2018/11/23/5bf78300e247b.png)  
在网页端可查看提交信息，如下图。  
![22.png](https://i.loli.net/2018/11/23/5bf7833e199e8.png)  
完成代码提交后，Git仓库中文件的树结构如下图。  
![38.png](https://i.loli.net/2018/11/23/5bf7836f6b889.png)  
## 三．使用持续集成工具响应代码变更，并获得新构建的软件版本
使用持续集成工具响应代码变更，并获得新构建的软件版本。  
首先在Jenkins的初始页面，点击左侧的“新建项目”，选择一个自由风格的持续集成任务，并起一个名字（Test1），点击OK完成创建。创建好持续集成任务后，会自动进入任务的配置页面。  
在源码管理项中选择Git选项，填写好Repository URL，并可添加授权用户。  
![24.png](https://i.loli.net/2018/11/23/5bf7841fe0385.png)  
如选择添加授权用户将弹出如下对话框，填好用户名和密码后点击“添加”即可添加成功。  
![26.png](https://i.loli.net/2018/11/23/5bf78447cda9f.png)  
在构建触发器项中选择“轮询SCM”选项，并填写日程表，如下图（“H/2 * * * *”表示2分钟检查一次git的变化情况）。  
![25.png](https://i.loli.net/2018/11/23/5bf784ab0d8be.png)  
在构建项下的增加构建步骤中选择“Invoke Ant”。  
![41.png](https://i.loli.net/2018/11/23/5bf7852f6623a.png)  
提交保存设置即可。  
## 四．缺陷管理——Redmine
新建项目Test1。  
![29.png](https://i.loli.net/2018/11/23/5bf785e5bf40b.png)  
新建问题，在描述中添加错误描述，并选择指派给谁。  
![30.png](https://i.loli.net/2018/11/23/5bf786003dd7e.png)  
问题建好后如下图。  
![31.png](https://i.loli.net/2018/11/23/5bf7861a0dcf4.png)  
![32.png](https://i.loli.net/2018/11/23/5bf786361aa29.png)  
指派人员把项目问题修复完成后，可以通过“clear”按钮消除问题。  
![33.png](https://i.loli.net/2018/11/23/5bf786800f434.png)  
进入“My page”，可看见项目管理员的指派给自己的问题。  
![34.png](https://i.loli.net/2018/11/23/5bf786b15113e.png)
## 五．冒烟测试
将修改好的项目代码放到到JenkinsTest文件夹。  
使用git-bash.exe把新增文件push到云端。  
![35.png](https://i.loli.net/2018/11/23/5bf786ee1ab71.png)  
等待轮询周期，查看轮询日志。  
![39.png](https://i.loli.net/2018/11/23/5bf7870f64f21.png)  
查看控制台输出。  
![40.png](https://i.loli.net/2018/11/23/5bf7872a63e33.png)

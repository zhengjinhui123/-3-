# 实验一：开发者测试（3）
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

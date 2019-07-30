# Windows安装Gradle
本文将粗略的搭建一个Spring源码的阅读环境，为后面的源码阅读做一个准备。之前一直使用的是Maven，没有接触过Gradle，但是spring的源码是使用Gradle搭建的，所以还是很有必要学习一下，而且网上大多数的声音都介绍Gradle比Maven优秀。
# 安装Gradle
- 从[Gradle官网](https://gradle.org/releases/)下载安装安装包
<img src="https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Project_Construction_Tools/Gradle/InstallPng.png">  
> 下载下来的是安装包，最好解压到当前文件夹  
> 二进制安装包中只包含可执行文件（一般使用这个就好了，由于是外国网站，完整版下载太慢）   
> 完整版中包括可执行文件，源代码和API文档  

- 配置环境变量

> GradleHome配置

<img src = "https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Project_Construction_Tools/Gradle/GraldeHome.png">

> Path配置

<img src = "https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Project_Construction_Tools/Gradle/GradlePath.png">

> 打开目录行工具，输入gradle -v，能看到gradle的版本信息表示安装已经成功

<img src = "https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Project_Construction_Tools/Gradle/GradleSuccess.png">
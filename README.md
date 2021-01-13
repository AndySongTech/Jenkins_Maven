## 1.Jenkins简介
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123213935531.png)
Jenkins，原名Hudson，2011年改为Jenkins，它是一个开源的实现**持续集成**的软件工具。

Jenkins是一个开源软件项目，是基于Java开发的一种持续集成工具，用于监控持续重复的工作，旨在提供一个开放易用的软件平台，使软件的持续集成变成可能。

Jenkins功能包括： 持续的软件版本发布/测试项目。 监控外部调用执行的工作。

## 2.持续集成、持续交付、持续部署概念

### 2.1.持续集成Continuous Intergration (CI)
**项目开发**
各个小组分别负责各个具体模块开发，本模块独立测试虽然能够通过，但是上线前夕将所有模块整合到一起集成测试却发现很多问题，想要解决就需要把很多代码返工重写而且仍然有可能有问题，但现在时间很可能不够了。那怎么做会好一些呢？
经常性、频繁的把所有模块集成在一起进行测试，有问题尽早发现，这就是持续集成。
**关注点**
持续集成的关注点在于尽早发现项目整体运行问题，尽早解决

### 2.2.持续部署Continuous Deployment（CD）
**项目开发**
开发过程中进行单元测试能够通过，但是部署到服务器上运行出现问题。那怎么做会好一些呢？仅仅单元测试还不够，各个模块都必须能够在服务器上运行。
**关注点**
持续部署的关注点在于项目功能部署至服务器后可以运行，为下一步测试环节或最终用户正式使用做好准备
### 2.3.持续交付Continuous Delivery（CD）
**项目开发**
项目的各个升级版本之间间隔时间太长，对用户反馈感知迟钝，无法精确改善
用户体验，用户流失严重。
那怎么做会好一些呢？
用小版本不断进行快速迭代，不断收集用户反馈信息，用最快的速度改进优化。
**关注点**
持续交付的关注点在于研发团队的最新代码能够尽快让最终用户体验到

>集成是指软件个人研发的部分向软件整体部分交付，以便尽早发现个人开发部分的问题；
部署是代码尽快向可运行的开发/测试节交付，以便尽早测试；
交付是指研发尽快向客户交付，以便尽早发现生产环境中存在的问题。
## 3.持续集成流程
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123215246644.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123215610184.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 4.安装Jenkins
### 4.1.Jenkins的下载

安装Jenkins需要安装正确的java环境以支持jenkins的运行：

```
2.164(2019-02)及更新版本:Java 8或Java 11
2.54(2017-04)更新版本:Java 8
1.612(2015-05)及更新版本:Java 7
```
本文直接使用war包安装
下载地址：[https://jenkins-ci.org/content/thank-you-downloading-windows-installer/](https://jenkins-ci.org/content/thank-you-downloading-windows-installer/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123220550530.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70) 

### 4.2.部署Jenkins

- 检查服务器的JDK版本：

```shell
[root@VM_0_15_centos ~]# java -version
java version "1.8.0_144"
Java(TM) SE Runtime Environment (build 1.8.0_144-b01)
Java HotSpot(TM) 64-Bit Server VM (build 25.144-b01, mixed mode)
```
- 准备一个TomCat

```shell
[root@VM_0_15_centos opt]# ll
total 271596
drwxr-xr-x   9 root root      4096 Nov 23 22:11 apache-tomcat-8.5.46
-rw-r--r--   1 root root  11623939 Oct 14 15:18 apache-tomcat-8.5.46.tar.gz
```
- 修改tomcat名字为JenkinsServer

```shell
[root@VM_0_15_centos opt]# ll
total 271596
drwxr-xr-x   9 root root      4096 Nov 23 22:11 JenkinsServer
-rw-r--r--   1 root root  11623939 Oct 14 15:18 apache-tomcat-8.5.46.tar.gz
```
- 准备jenkins.war文件,将war文件放到Tomcat的webapp目录下

```shell
[root@VM_0_15_centos webapps]# pwd
/opt/JenkinsServer/webapps
[root@VM_0_15_centos webapps]# ll
total 75540
drwxr-x--- 15 root root     4096 Nov 23 22:11 docs
drwxr-x---  6 root root     4096 Nov 23 22:11 examples
drwxr-x---  5 root root     4096 Nov 23 22:11 host-manager
-rw-r--r--  1 root root 77330344 Nov 23 22:14 jenkins.war
drwxr-x---  5 root root     4096 Nov 23 22:11 manager
drwxr-x---  3 root root     4096 Nov 23 22:11 ROOT
```

- 启动Tomcat
访问   http://122.51.50.249:8080/jenkins 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123221742817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)如果出现如下页面恭喜你成功了，如果访问不到，有可能是版本不匹配!
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123221929417.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)

**获取管理员密码：**

```shell
[root@VM_0_15_centos logs]# cat /root/.jenkins/secrets/initialAdminPassword
be76491b01ff4c7a94ab682ec6c0d125
```
获取了密码之后输入密码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123222507531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**选择插件来安装**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123225409643.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**选择无**
我们稍后安装插件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123225459224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**创建第一个管理员用户**
![在这里插入图片描述](https://img-blog.csdnimg.cn/201911232256546.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**使用admin账户继续**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123225806749.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**保存并完成**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123225838515.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
 **开始使用jenkins**
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123225902552.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**系统管理----->全局安全配置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123232826599.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**出现如下问题**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123232923991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**打开Tomcat的server.xml配置文件,添加编码格式**

```xml
[root@andycentos conf]# vim /opt/jenkinsserver/conf/server.xml
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" 
           URIEncoding="UTF-8"/>
```
```shell
[root@andycentos ~]cd /opt/jenkinsserver/bin/
[root@andycentos bin]./shutdown.sh
[root@andycentos bin]./startup.sh
重新启动,tomcat!
```

## 5.安装maven
1：在/usr/local目录下创建一个名字叫做maven3的目录

```shell
[root@VM_0_15_centos opt]# cd /usr/local/
[root@VM_0_15_centos local]# mkdir maven3
[root@VM_0_15_centos local]# cd maven3/
[root@VM_0_15_centos maven3]# pwd
/usr/local/maven3
```
2：将apache-maven-3.3.9-bin.tar.gz移动到maven3这个目录中去

```shell
[root@VM_0_15_centos maven3]# cp /opt/apache-maven-3.3.9-bin.tar.gz /usr/local/maven3/
[root@VM_0_15_centos maven3]# ll
total 8296
-rw-r--r-- 1 root root 8491533 Nov 23 23:35 apache-maven-3.3.9-bin.tar.gz
```
3：解压这个目录

```shell
[root@VM_0_15_centos maven3]# tar -zxvf apache-maven-3.3.9-bin.tar.gz
apache-maven-3.3.9/boot/plexus-classworlds-2.5.2.jar
apache-maven-3.3.9/lib/maven-embedder-3.3.9.jar
apache-maven-3.3.9/lib/maven-settings-3.3.9.jar
apache-maven-3.3.9/lib/plexus-utils-3.0.22.jar
apache-maven-3.3.9/lib/maven-core-3.3.9.jar
```
4：配置如下的环境变量

```shell
export JAVA_HOME=/opt/jdk1.8.0_144
export MAVEN_HOME=/usr/local/maven3/apache-maven-3.3.9
export PATH=${JAVA_HOME}/bin:$PATH:${MAVEN_HOME}/bin
```
## 6.配置maven

**全局工具配置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123234112457.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**配置maven的根路径**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123234228142.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**配置JDK的使用**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123234338904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
保存！

## 7.安装Git
第一步：安装编译 git 时需要的包

```shell
yum install -y curl-devel expat-devel gettext-devel openssl-devel zlib-devel
yum install -y gcc perl-ExtUtils-MakeMaker
```

第二步：删除已有的 git

```shell
yum remove git
```

第三步：Git 官网下载 Git 最新版 tar 包，移动到/usr/local 目录下

```shell
cd /usr/local
tar -zxvf git-2.9.3.tar.gz
ll
drwxr-xr-x.  2 root root    4096 Apr 11  2018 bin
drwxr-xr-x.  2 root root    4096 Apr 11  2018 etc
drwxr-xr-x.  2 root root    4096 Apr 11  2018 games
drwxrwxr-x  21 root root   12288 Aug 13  2016 git-2.9.3
-rw-r--r--   1 root root 5918768 Nov 23 23:47 git-2.9.3.tar.gz
drwxr-xr-x.  2 root root    4096 Apr 11  2018 include
drwxr-xr-x.  2 root root    4096 Apr 11  2018 lib
drwxr-xr-x.  2 root root    4096 Apr 11  2018 lib64
drwxr-xr-x.  2 root root    4096 Apr 11  2018 libexec
drwxr-xr-x   3 root root    4096 Nov 23 23:35 maven3
drwxr-xr-x  12 root root    4096 Nov 23 22:39 qcloud
drwxr-xr-x.  2 root root    4096 Apr 11  2018 sbin
drwxr-xr-x.  5 root root    4096 Mar  7  2019 share
drwxr-xr-x.  2 root root    4096 Apr 11  2018 src
```

Ø 第四步：编译安装

```shell
cd git-2.9.3
make prefix=/usr/local/git all 
make prefix=/usr/local/git install
```

配置环境变量
>export PATH=$PATH:/usr/local/git/bin

```shell
export JAVA_HOME=/opt/jdk1.8.0_144
export MAVEN_HOME=/usr/local/maven3/apache-maven-3.3.9
export PATH=${JAVA_HOME}/bin:$PATH:${MAVEN_HOME}/bin:/usr/local/git/bin
```

使环境变量生效

```shell
source /etc/profile
```

第五步：检查一下版本号

```shell
git --version
```
## 8.安装Git插件
**安装支持Git的插件**
插件管理----会遇到问题(可用插件无法搜索)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123235444828.png)
解决方案:
       
```
vim /root/.jenkins/hudson.model.UpdateCenter.xml  将https改成http
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191123235545945.png)
**搜索插件下载**
>如果插件安装不成功，那么直接进行重试！

安装Git插件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124000115648.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)安装，并不重启
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124000221716.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
安装scm-api插件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124082612952.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 9.配置Git
![在这里插入图片描述](https://img-blog.csdnimg.cn/201911241044468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 10.构建一个项目
**创建一个新任务**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124091207258.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**输入任务的名字**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124100253624.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**构建一个自由风格的软件项目**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124100320715.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**项目配置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124100530468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124100715317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**配置源码的路径**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019112410081872.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**Gitee源码地址**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124112308522.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/201911241126242.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 11.实现一次构建
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124102105579.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124112818722.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
查看构建之后的目录：

```shell
[root@VM_0_15_centos 1.0-SNAPSHOT]# pwd
/root/.m2/repository/com/bruceliu/jinkins/web/demo/jinkins-web/1.0-SNAPSHOT
[root@VM_0_15_centos 1.0-SNAPSHOT]# ll
total 8692
-rw-r--r-- 1 root root    3922 Nov 24 11:18 jinkins-web-1.0-SNAPSHOT.pom
-rw-r--r-- 1 root root 8887958 Nov 24 11:25 jinkins-web-1.0-SNAPSHOT.war
-rw-r--r-- 1 root root     720 Nov 24 11:25 maven-metadata-local.xml
-rw-r--r-- 1 root root     195 Nov 24 11:25 _remote.repositories
```

## 12.安装部署的插件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124113347987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**可用插件上进行搜索：Deploy to Container**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124113514579.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124114116630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 13.准备要部署Tomcat服务器
**Docker拉取tomcat镜像**

```shell
[root@VM_0_10_centos ~]# docker pull tomcat
Using default tag: latest
Trying to pull repository docker.io/library/tomcat ... 
latest: Pulling from docker.io/library/tomcat
844c33c7e6ea: Pull complete 
ada5d61ae65d: Pull complete 
f8427fdf4292: Pull complete 
f025bafc4ab8: Pull complete 
67b8714e1225: Pull complete 
64b12da521a3: Pull complete 
2e38df533772: Pull complete 
4144d55bbb47: Pull complete 
a767078bbe38: Pull complete 
81f4cc5808bc: Pull complete 
Digest: sha256:996d406c509a4ebe2f4e96eeda331a354f1663b7ec0ff06685b75c4decef7325
Status: Downloaded newer image for docker.io/tomcat:latest
```
**启动tomcat容器**

```shell
[root@VM_0_10_centos bin]# pwd
/opt/apache-tomcat-8.5.46/bin
[root@VM_0_10_centos bin]# ./startup.sh 
Using CATALINA_BASE:   /opt/apache-tomcat-8.5.46
Using CATALINA_HOME:   /opt/apache-tomcat-8.5.46
Using CATALINA_TMPDIR: /opt/apache-tomcat-8.5.46/temp
Using JRE_HOME:        /opt/jdk1.8.0_144
Using CLASSPATH:       /opt/apache-tomcat-8.5.46/bin/bootstrap.jar:/opt/apache-tomcat-8.5.46/bin/tomcat-juli.jar
Tomcat started.
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124122710641.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70) **设置Tomcat的访问的用户名和密码**
 打开Tomcat/conf文件

```
vi tomcat-users.xml 
```

添加如下的内容

```xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="tomcat" password="tomcat" roles="manager-status,manager-gui,manager-script,manager-jmx"/>

```
配置以上内容后访问ip:8080，如果点击Host manager或者 Manager App没有权限访问，请操作接下来第二步

需要编辑 tomcat/webapps/manager/META-INF/context.xml 文件,注释掉以下部分

```xml
<!--
<Valve className="org.apache.catalina.valves.RemoteAddrValve"
allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
-->
```
启动TomCat
```shell
[root@VM_0_10_centos bin]# netstat -apn | grep 8080
tcp6       0      0 :::8080                 :::*                    LISTEN      14036/java  
```
在点击Manager App时配置的用户就生效了
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124124954586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124125047338.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)


## 14.配置构建后的操作
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124114207801.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124125145222.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124131826606.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 15.再执行一次构建
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124132213913.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124132351545.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
可以看到war包已经发布到部署的服务器了

```shell
[root@VM_0_10_centos webapps]# pwd
/opt/apache-tomcat-8.5.46/webapps
[root@VM_0_10_centos webapps]# ll
total 8704
drwxr-x--- 15 root root    4096 Nov 24 12:24 docs
drwxr-x---  6 root root    4096 Nov 24 12:24 examples
drwxr-x---  5 root root    4096 Nov 24 12:24 host-manager
drwxr-x---  4 root root    4096 Nov 24 13:23 jinkins-web
-rw-r-----  1 root root 8887958 Nov 24 13:23 jinkins-web.war
drwxr-x---  5 root root    4096 Nov 24 12:24 manager
drwxr-x---  3 root root    4096 Nov 24 12:24 ROOT
```
## 16.构建触发器
![d](https://img-blog.csdnimg.cn/20191124132714713.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
触发的地址：
http://122.51.50.249:8080/jenkins/job/JinkinsWeb/build?token=BRUCELIU_TRIGGER
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124133031598.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
## 17.配置Gitee
**找到勾子函数配置的地方(webhooks)**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124133159370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**配置触发构建**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124133358592.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124133423341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
**关闭防止站点伪造**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124133530703.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)**系统管理-----全局安全配置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124133638388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
把上面的勾去掉
重新启动服务器

## 18.测试持续集成
- IDEA中PUSH
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124134532329.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
- 测试是否正常触发钩子程序
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124134603661.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
- 发布到部署服务器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124134620708.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191124134630344.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0JydWNlTGl1X2NvZGU=,size_16,color_FFFFFF,t_70)

##### 注： 本内容来源于51石头老师的课件

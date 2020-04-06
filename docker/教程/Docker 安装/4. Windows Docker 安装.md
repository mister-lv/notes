# Windows Docker 安装

------

## win7、win8 系统

win7、win8 等需要利用 docker toolbox 来安装，国内可以使用阿里云的镜像来下载，下载地址：http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/

安装比较简单，双击运行，点下一步即可，可以勾选自己需要的组件：

![img](https://www.runoob.com/wp-content/uploads/2016/05/691999-20180512142142130-1831870973.png)

docker toolbox 是一个工具集，它主要包含以下一些内容：

- Docker CLI - 客户端，用来运行 docker 引擎创建镜像和容器。
- Docker Machine - 可以让你在 Windows 的命令行中运行 docker 引擎命令。
- Docker Compose - 用来运行 docker-compose 命令。
- Kitematic - 这是 Docker 的 GUI 版本。
- Docker QuickStart shell - 这是一个已经配置好Docker的命令行环境。
- Oracle VM Virtualbox - 虚拟机。

下载完成之后直接点击安装，安装成功后，桌边会出现三个图标，入下图所示：

![img](https://www.runoob.com/wp-content/uploads/2017/12/icon-set.png)

点击 Docker QuickStart 图标来启动 Docker Toolbox 终端。

如果系统显示 User Account Control 窗口来运行 VirtualBox 修改你的电脑，选择 Yes。

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513667960-3359-b2d-shell.png)

**$** 符号那你可以输入以下命令来执行。

```
$ docker run hello-world
 Unable to find image 'hello-world:latest' locally
 Pulling repository hello-world
 91c95931e552: Download complete
 a8219747be10: Download complete
 Status: Downloaded newer image for hello-world:latest
 Hello from Docker.
 This message shows that your installation appears to be working correctly.

 To generate this message, Docker took the following steps:
  1. The Docker Engine CLI client contacted the Docker Engine daemon.
  2. The Docker Engine daemon pulled the "hello-world" image from the Docker Hub.
     (Assuming it was not already locally available.)
  3. The Docker Engine daemon created a new container from that image which runs the
     executable that produces the output you are currently reading.
  4. The Docker Engine daemon streamed that output to the Docker Engine CLI client, which sent it
     to your terminal.

 To try something more ambitious, you can run an Ubuntu container with:
  $ docker run -it ubuntu bash

 For more examples and ideas, visit:
  https://docs.docker.com/userguide/
```

------

## Win10 系统

现在 Docker 有专门的 Win10 专业版系统的安装包，需要开启Hyper-V。

### 开启 Hyper-V

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-4363-20171206211136409-1609350099.png)

程序和功能

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-4368-20171206211345066-1430601107.png)

启用或关闭Windows功能

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-9748-20171206211435534-1499766232.png)

选中Hyper-V

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-6433-20171206211858191-1177002365.png)

### 1、安装 Toolbox

最新版 Toolbox 下载地址： https://www.docker.com/get-docker

点击 [Download Desktop and Take a Tutorial](https://www.runoob.com/wp-content/uploads/2016/05/70E63727-8DAD-4BBC-80D4-81E45963C8F3.png)，并下载 Windows 的版本，如果你还没有登录，会要求注册登录：

![img](https://www.runoob.com/wp-content/uploads/2016/05/70E63727-8DAD-4BBC-80D4-81E45963C8F3.png)

![img](https://www.runoob.com/wp-content/uploads/2016/05/320588F9-BA7B-4B6A-807C-5BDEF4523E46.png)

![img](https://www.runoob.com/wp-content/uploads/2016/05/5AEB69DA-6912-4B08-BE79-293FBE659894.png)

### 2、运行安装文件

双击下载的 Docker for Windows Installer 安装文件，一路 Next，点击 Finish 完成安装。

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513669129-6146-20171206214940331-1428569749.png)

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668903-9668-20171206220321613-1349447293.png)

安装完成后，Docker 会自动启动。通知栏上会出现个小鲸鱼的图标![img](https://www.runoob.com/wp-content/uploads/2017/12/1513582421-4552-whale-x-win.png)，这表示 Docker 正在运行。

桌边也会出现三个图标，入下图所示：

我们可以在命令行执行 docker version 来查看版本号，docker run hello-world 来载入测试镜像测试。

如果没启动，你可以在 Windows 搜索 Docker 来启动：

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513585082-6751-docker-app-search.png)

启动后，也可以在通知栏上看到小鲸鱼图标：

![img](https://www.runoob.com/wp-content/uploads/2017/12/1513585123-3777-whale-taskbar-circle.png)

------

## 镜像加速

### Windows 10

对于使用 Windows 10 的系统，在系统右下角托盘 Docker 图标内右键菜单选择 Settings，打开配置窗口后左侧导航菜单选择 Daemon。在 Registrymirrors 一栏中填写加速器地址 **https://registry.docker-cn.com** ，之后点击 Apply 保存后 Docker 就会重启并应用配置的镜像地址了。

![img](https://www.runoob.com/wp-content/uploads/2019/10/567993-20170216215240832-1373874687.png)
# docker操作

### docker打开交互界面-退出重进

![1697075112109](C:\Users\couco\AppData\Local\Temp\1697075112109.png)

**步骤说明**
步骤1：运行容器
首先，你需要运行容器。使用以下命令可以运行一个名为my-container的容器：

docker run -it --name my-container <image-name>
1.
其中，<image-name>是你想要使用的镜像名称。这个命令会在后台运行一个新的容器，并且打开一个交互式终端，允许你与容器进行交互。

步骤2：容器运行中
容器运行后，你可以在终端中执行你需要的操作，例如安装软件、运行程序等。在容器中，你可以像使用一个独立的虚拟机一样进行操作。

步骤3：停止容器
当你完成了容器中的操作，你可以停止容器，以便之后重新进入。使用以下命令可以停止容器：

docker stop my-container
其中，my-container是你所运行的容器的名称。这个命令会将容器停止，并释放容器占用的资源。你可以通过docker ps命令来查看容器是否已经停止。

步骤4：重新进入容器
如果你需要再次进入容器，可以使用以下命令重新进入容器：

docker start -ai my-container
其中，my-container是你所运行的容器的名称。这个命令会重新启动容器，并打开一个交互式终端，允许你与容器进行交互。-a选项表示将终端的输出附加到当前终端，使你能够查看容器的输出。

3. **示例代码**
    下面是一些示例代码，帮助你更好地理解上述步骤：

步骤1：运行容器
docker run -it --name my-container ubuntu:latest
这个命令会在后台运行一个基于Ubuntu最新版本的容器，并打开一个交互式终端。

步骤2：容器运行中
在容器中，你可以执行任何你需要的操作。例如，你可以安装软件包：

apt update
apt install -y <package-name>
这个命令会更新软件包列表，并安装一个名为<package-name>的软件包。

步骤3：停止容器
当你完成容器中的操作后，你可以停止容器。使用以下命令停止容器：

docker stop my-container
这个命令会停止名为my-container的容器。

步骤4：重新进入容器
当你需要再次进入容器时，使用以下命令重新进入容器：

docker start -ai my-container
这个命令会重新启动名为my-container的容器，并打开一个交互式终端。


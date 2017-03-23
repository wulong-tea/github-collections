# 一、 docker安装
    
```
#安装docker
sudo yum install docker

#docker以服务启动
sudo systemctl start docker

#查看docker服务状态
sudo systemctl status docker

#关闭docker服务
sudo systemctl stop docker

#重启docker服务
sudo systemctl restart docker

#使docker服务开机自运行
sudo systemctl enable docker
```

# 二、docker获取镜像

由于docker被墙，我们使用国内免费docker镜像源。

```
#从DaoCloud获取centos7镜像
sudo docker pull daocloud.io/centos:7

#查看image
sudo docker images

#重命名docker镜像
sudo docker tag daocloud.io/centos:7 centos:7

#删除镜像
sudo docker rmi daocloud.io/centos:7

#查看进程 
sudo docker ps 
    -a : 列出所有的进程，包括处于未运行状态的

```

# 三、启动镜像

```
#启动centos容器
 sudo docker run -d -i -t --name centos 67 /bin/bash 
```
参数详解
OPTIONS说明：
- -a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；
- -d: 后台运行容器，并返回容器ID；
- -i: 以交互模式运行容器，通常与 -t 同时使用；
- -t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
- --name="nginx-lb": 为容器指定一个名称；
- --dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致；
- --dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致；
- -h "mars": 指定容器的hostname；
- -e username="ritchie": 设置环境变量；
- --env-file=[]: 从指定文件读入环境变量；
- --cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定CPU运行；
- -m :设置容器使用内存最大值；
- --net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/Container: 四种类型；
- --link=[]: 添加链接到另一个容器；
- --expose=[]: 开放一个端口或一组端口；

# 四、进入镜像

```
sudo docker attach <容器id>
```

# 五、建立自定义镜像(利用dockeFile)
## 1. DockerFile介绍
### FROM 命令


```
FROM <image>
```

或


```
FROM <image>:<tag>
```

这个设置基本的镜像，为后续的命令使用，所以应该作为Dockerfile的第一条指令。

比如:


```
FROM centos:7
```

如果没有指定 tag ，则默认tag是latest，如果都没有则会报错。

### RUN 命令

RUN命令会在上面FROM指定的镜像里执行任何命令，然后提交(commit)结果，提交的镜像会在后面继续用到。

两种格式:


```
RUN <command> (the command is run in a shell - `/bin/sh -c`)
```

或:


```
RUN ["executable", "param1", "param2" ... ]  (exec form)
```

RUN命令等价于:


```
docker run image command
docker commit container_id
```

### 注释

使用 # 作为注释

如:


```
# Memcached
#
# VERSION       1.0

# use the ubuntu base image provided by dotCloud
FROM ubuntu

# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

# install memcached
RUN apt-get install -y memcached
```

### MAINTAINER 命令

```
MAINTAINER <name>
```

MAINTAINER命令用来指定维护者的姓名和联系方式

如:


```
MAINTAINER Jayce, jaycejia@gmail.com
```

### ENTRYPOINT 命令

有两种语法格式，一种就是上面的(shell方式):


```
ENTRYPOINT cmd param1 param2 ...
```

第二种是 exec 格式:


```
ENTRYPOINT ["cmd", "param1", "param2"...]
```

如:


```
ENTRYPOINT ["echo", "Whale you be my container"]
```

ENTRYPOINT 命令设置在容器启动时执行命令


```
root@tankywoo-docker:~# cat Dockerfile
FROM ubuntu
ENTRYPOINT echo "Welcome!"

root@tankywoo-docker:~# docker run 62fda5e450d5
Welcome!
```

USER 命令

比如指定 memcached 的运行用户，可以使用上面的 ENTRYPOINT 来实现:


```
ENTRYPOINT ["memcached", "-u", "daemon"]
```

更好的方式是：


```
ENTRYPOINT ["memcached"]
USER daemon
```


### EXPOSE 命令

EXPOSE 命令可以设置一个端口在运行的镜像中暴露在外


```
EXPOSE <port> [<port>...]
```

比如memcached使用端口 11211，可以把这个端口暴露在外，这样容器外可以看到这个端口并与其通信。


```
EXPOSE 11211
```

### 一个完整的例子:


```
# Memcached
#
# VERSION       2.2

# use the ubuntu base image provided by dotCloud
FROM ubuntu

MAINTAINER Victor Coisne victor.coisne@dotcloud.com

# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

# install memcached
RUN apt-get install -y memcached

# Launch memcached when launching the container
ENTRYPOINT ["memcached"]

# run memcached as the daemon user
USER daemon

# expose memcached port
EXPOSE 11211
```

### ENV 命令

用于设置环境变量


```
ENV <key> <value>
```

设置了后，后续的RUN命令都可以使用

使用此dockerfile生成的image新建container，可以通过 docker inspect 看到这个环境变量:


```
root@tankywoo-docker:~# docker inspect 49bfc7a9817f
    ...
    "Env": [
        "name=tanky",
        "HOME=/",
        "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    ],
    ...
```

里面的name=tanky就是设置的。

也可以通过在docker run时设置或修改环境变量:


```
docker run -i -t --env name="tanky" ubuntu:newtest /bin/bash
```

### ADD 命令

从src复制文件到container的dest路径:


```
ADD <src> <dest>
```

```<src>``` 是相对被构建的源目录的相对路径，可以是文件或目录的路径，也可以是一个远程的文件url
```<dest>``` 是container中的绝对路径


### VOLUME 命令


```
VOLUME ["<mountpoint>"]
```

如:


```
VOLUME ["/data"]
```

创建一个挂载点用于共享目录

具体参考 Docker 4 -- 总结

### WORKDIR 命令


```
WORKDIR /path/to/workdir
```

配置```RUN```, ```CMD```, ```ENTRYPOINT``` 命令设置当前工作路径

可以设置多次，如果是相对路径，则相对前一个 ```WORKDIR``` 命令

比如:


```
WORKDIR /a WORKDIR b WORKDIR c RUN pwd
```

其实是在 /a/b/c 下执行 ```pwd```


### CMD 命令

有三种格式:


```
CMD ["executable","param1","param2"] (like an exec, preferred form)
CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
CMD command param1 param2 (as a shell)
```

一个Dockerfile里只能有一个CMD，如果有多个，只有最后一个生效。

> The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT as well.
TODO 还没搞清楚这个的作用


总结一下，基本常用的命令是: FROM, MAINTAINER, RUN, ENTRYPOINT, USER, PORT, ADD

## 2. 利用Dockerfile构建image


```
#通过build命令创建docker image，最后的.是build路径
sudo docker build -f <file name>-t <tag name>/<image name> .
    -t : tag 一般为组织标识
    -f : 指定自定义Dockerfile文件
```



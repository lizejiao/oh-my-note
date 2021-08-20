### Docker安装

centos  为例：查看版本：`cat /etc/redhat-release`
[参考网址](https://docs.docker.com/install/linux/docker-ce/centos/)

- **先安装gcc：** `yum -y install gcc`    

- **查看版本：** `gcc -v`

**安装需要的软件包**

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

#### 阿里加速：

```shell
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

- **查看配置：** `vi /etc/yum.repos.d/docker-ce.repo`
- **更新软件包：** `yum makecache fast`
- **安装docker：**  `yum install docker-ce docker-ce-cli containerd.io`
- **配置文件位置：** `/etc/sysconfig/docker`
- **启动docker：** `systemctl start docker`
- **设置开机启动：** `systemctl enable docker`
- **查看docker启动进程：** `ps -ef|grep docker`
- **查看docker版本：** `docker version  docker info`   

#### 下载镜像

- `docker pull mysql:5.7`  
- `docker pull rabbitmq:management` （带管理台的MQ）
- `docker pull zookeeper:latest`  
- `docker pull redis:rc-buster`

[镜像搜索地址](https://hub.docker.com/search?q=&type=image)

[镜像加速](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

------

#### 权限问题解决

docker守护进程启动的时候，会默认赋予名字为docker的用户组读写Unix socket的权限，因此只要创建docker用户组，并将当前用户加入到docker用户组中，那么当前用户就有权限访问Unix socket了，进而也就可以执行docker相关命令

1. 添加docker用户组 `sudo groupadd docker` 
2. 将登陆用户加入到docker用户组中  `sudo gpasswd -a  $USER  docker`
3. 更新用户组 `newgrp docker`
4. 测试docker命令是否可以使用sudo正常使用 `docker ps` 

------

#### 镜像操作

- 查看镜像：`docker images`    
- 展示所有所有镜像（包含中间镜像层）：`docker images -a`
- 查询镜像：`docker search 镜像名字`
- 删除镜像：`docker rmi 镜像id`

#### 容器操作

- **启动mysql：** `docker run -p 3306:3306 --name mysql01 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7`
- **启动rabitmq：** `docker run -d -p 5672:5672 -p 15672:15672 --name myrabitmq 镜像id` 
- **启动redis：** `docker run -d -p 6379:6379 --name myredis 镜像id`   
- **启动zookeeper：** `docker run --name zk01 -p 2181:2181 --restart always -d 镜像id` 
- **启动nacos：** `docker run --name nacos-2.0.1 -e MODE=standalone -p 8849:8848 -d nacos/nacos-server:2.0.1`
- **启动kibana：** `docker run -d --name kibana7.7.1 --net mynet   -p 5601:5601 kibana:7.7.1`

###### Kibana Doker启动相关配置

`docker exec -it kibana7.7.1 bash cd config vi kibana.yml`

- **查看日志：** docker logs -f -t --tail 100 kibana7.7.1
- **更新启动参数：** docker update --restart=always xxx  
- **查看所有容器：** `docker ps -a`
- **查看启动容器：** `docker ps`    
- **启动已停止的容器：** `docker start 容器id或名字`
- **关闭容器 ：** `docker stop 容器id`    
- **取消容器开机启动：** `docker update --restart=no 容器ID`
- **强制关闭：**  `docker kill 容器id`   
- **删除已停止容器 ：** `docker rm 容器id`    
- **删除没有停止容器：**  `docker rm -f 容器id`  
- **进入容器内部：** `docker exec -it 程序id /bin/bash`    
- **exit 关闭容器退出(自测不会退出)：**    `ctrl+p+q`
- **查看日志：** `docker logs -f (追加) -t (加入时间戳) --tail 3 (显示最后3行) 容器id`  
- **查看容器结构细节：** `docker inspect 容器id`  
- **拷贝容器中的文件：** `docker cp 容器id:文件路径 要拷贝到的路径`
- **提交自己的docker镜像：** `docker commit -a="lgd" -m="mysql-lgd" 243baa0ea2a7 ligoudan/lgd-mysql:1.0`  






##Docker 命令


| 命令                                       | 说明                                       |
| ---------------------------------------- | ---------------------------------------- |
| docker                                   | 显示所有docker可用的命令信息                        |
| docker command --help                    | 显示详细的指定命令的用法                             |
| docker start containerID                 | 启动容器                                     |
| docker stop containerID                  | 停止容器                                     |
| docker ps                                | 查看正在运行的容器                                |
| docker ps -a                             | 查看所有创建过的容器(无论是否启动)                       |
| docker ps -l                             | 查看最后一次创建的容器                              |
| docker run -d  imageID                   | 创建容器，并后台运行                               |
| docker run -d -p port:容器端口  imageID      | 后台运行，并绑定端口 默认绑定tcp端口                     |
| docker run -d -p port:容器端口 --name cname  imageID | 后台运行，并绑定端口 默认绑定tcp端口                     |
| docker run -d -p port:容器端口 --name cname -v 本地目录:容器目录  imageID | 后台运行，并绑定端口 默认绑定tcp端口                     |
| docker run -d -p port:容器端口/udp  imageID  | 后台运行，并绑定udp端口                            |
| docker run -d -p IP:port:容器端口  imageID   | 后台运行，并绑定IP和端口                            |
| docker run -d -P imageID                 | P 自己自动指定端口映射                             |
| docker run -it ubuntu:15.10 /bin/bash    | 交互式启动容器                                  |
| docker exec -it cID  /bin/bash           | 进入一个正在运行的容器  也可能是/bin/sh，因为不确定每个容器都安装了bash |
| docker cp /www/runoob 96f7f14e99ab:/www/ | 将主机的目录拷贝到容器中指定的目录                        |
| docker cp /www/runoob 96f7f14e99ab:/www  | 将主机的目录拷贝到容器中，并指定目录名                      |
| docker cp  96f7f14e99ab:/www /tmp/       | 将容器中文件拷贝到本地                              |
| docker port ID                           | 显示容器端口与本地端口的对应关系                         |
| docker logs containerID                  | 查看指定容器内部的标准日志输出                          |
| docker logs -f containerID               | 像tail -f 一样查看指定容器内部日志输出                  |
| docker top ID                            | 显示容器机的进程                                 |
| docker rm ID                             | 删除容器，删除前必须先停止容器                          |
| docker images                            | 列出本地镜像列表                                 |
| docker search name                       | 在dock仓库搜索相关镜像                            |
| docker pull imageID:tag                  | 从仓库下载镜像，如果不指定tag，则下载最新版latest            |
| docker commit -m="has update" -a="runoob" e218edb10161 runoob/ubuntu:v2 | 提交修改过的容器为新的镜像                            |
| docker tag imageID  newtag               | 为镜像文件新建标签                                |
| docker build -t tag .                    | 构建镜像 指定tag名称和DockerFile的路径               |
| docker inspect 容器ID或容器名 \|grep '"IPAddress"' | 查看容器IP。如不加参数，则以json格式显示容器的全部信息           |
| docker save -o /home/user/images/ubuntu_14.04.tar ubuntu:14.04 | 导出镜像                                     |
| docker load --input ubuntu_14.04.tar     | 导入镜像                                     |
| docker export 7691a814370e > ubuntu.tar  | 导出容器，将容器导出为一个镜像                          |
| cat ubuntu.tar \| docker import - test/ubuntu:v1.0 | 将容器文件导入为一个镜像                             |
| docker import ubuntu.tar test/ubuntu:v1.0 | 将容器归档文件导入为一个镜像                           |



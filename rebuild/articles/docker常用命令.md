本文3090字，阅读约需8分钟

Hi，大家好，`Docker`作为轻量级的、高性能的沙箱容器，使用频率极高，功能非常强大。强大的功能需要繁杂的命令来支撑，docker命令很多，多得记不住。好记性不如烂笔头，烂笔头不如实战练习，本文汇总docker常用的命令，并对命令进行说明和举例，可以随用随取。

**一**

**常规命令**

**1**

**启动 Docker**

```javascript
# 微信公众号：ITester软件测试小栈
sudo systemctl start docker
```

**2**

**停止 Docker**

```javascript
# 微信公众号：ITester软件测试小栈
sudo systemctl stop docker
```

**3**

**重启 Docker**

```javascript
# 微信公众号：ITester软件测试小栈
sudo systemctl restart docker
```

**4**

**修改配置后重启 Docker**

```javascript
# 微信公众号：ITester软件测试小栈
sudo systemctl daemon-reload
sudo systemctl restart docker
```

**5**

**查看版本**

```javascript
# 微信公众号：ITester软件测试小栈
docker version
```

### **6**

**查看Docker 信息**

```javascript
# 微信公众号：ITester软件测试小栈
docker info
```

### **7**

**Docker 帮助**

```javascript
# 微信公众号：ITester软件测试小栈
docker --help
```



**二**

**镜像命令**

### **1**

**查看Docker上已经安装的镜像**

```javascript
# 微信公众号：ITester软件测试小栈
docker images
```

### **2**

**搜索Docker hub上面的镜像**

```javascript
# 微信公众号：ITester软件测试小栈
# 以tomcat为例
docker search tomcat
```

### **3**

**下载镜像**

```javascript
# 微信公众号：ITester软件测试小栈
# 以下载tomcat为例
docker pull tomcat[:version]
```

### **4**

**删除镜像**

```javascript
# 微信公众号：ITester软件测试小栈
# 以删除tomcat为例
docker rmi tomcat[:version]
# 通过镜像ID删除
docker rmi -f 镜像ID
# 通过镜像ID删除多个
docker rmi -f 镜像名1:TAG 镜像名2:TAG 
# 删除全部
# docker images -qa : 获取所有镜像ID
docker rmi -f $(docker images -qa)
```



**三**

**容器命令**

### **1**

**启动容器**

```javascript
# 微信公众号：ITester软件测试小栈
docker run [options] image [command] [arg...]
```

### **常用参数：**

```javascript
# 微信公众号：ITester软件测试小栈
-d: 后台运行容器,并返回容器ID

-i: 以交互式运行容器,通常与-t同时使用

-p: 端口映射,格式为 主机(宿主)端口:容器端口

-t: 为容器重新分配一个伪输入终端,通常与-i同时使用

--name="name": 为容器指定一个名称

--dns 8.8.8.8: 为容器指定一个dns服务器,默认与宿主一致

--dns-search domain:为容器指定一个DNS域名,默认与宿主一致

-h "hostname": 指定容器的hostname

-e arg="value": 设置环境变量

-env-file=[]:从指定文件读入环境变量

--cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定的cpu运行

-m: 设置容器使用内存最大值

--net="bridge": 指定容器的网络连接类型,支持bridge/host/none/container四种类型

--link=[]:添加链接到另外一个容器

--expose=[]:开放一个端口或一组端口,宿主机使用随机端口映射到开放的端口
```

**实例：**

```javascript
# 微信公众号：ITester软件测试小栈
docker run --name mynginx -d nginx:latest
# 映射多个端口
docker run -p 80:80/tcp -p 90:90 -v /data:/data -d nginx:latest
```

### **2**

**查看正在运行的Docker 容器**

```javascript
# 微信公众号：ITester软件测试小栈
docker ps
```

### **常用参数：**

```javascript
# 微信公众号：ITester软件测试小栈
# 显示所有容器，包括当前没有运行的容器
-a
# 显示最近创建的容器
-l
# 显示最近创建的N个容器
-n
# 静默模式,只显示容器ID
-q
# 不截断输出
--no-trunc
```

### **3**

**退出容器**

```javascript
# 微信公众号：ITester软件测试小栈
# 退出并停止
exit
# 容器不停止退出
ctrl+P+Q
```

### 

### **4**

**启动容器**

```javascript
# 微信公众号：ITester软件测试小栈
docker start 容器ID或容器name
```

### **5**

**重启容器**

```javascript
# 微信公众号：ITester软件测试小栈
docker restart 容器ID或容器name
```



### **6**

**停止容器**

```javascript
# 微信公众号：ITester软件测试小栈
docker stop 容器ID或容器name
```

### **7**

**强制停止容器**

```javascript
# 微信公众号：ITester软件测试小栈
docker kill 容器ID或容器name
```

### **8**

**删除容器**

```javascript
# 微信公众号：ITester软件测试小栈
# 删除已经停止的容器
docker rm 容器ID或容器name 
# 强制删除已经停止或正在运行的容器
docker rm -f  容器ID或容器name 
#一次性删除所有正在运行的容器
docker rm -f $(docker ps -qa)
```



### **9**

**从容器拷贝文件到**[**宿主机**](https://cloud.tencent.com/product/cdh?from=10680)

```javascript
# 微信公众号：ITester软件测试小栈
docker cp 容器ID或容器名称:/文件路径与文件名 宿主机地址

```

### **实例:**

```javascript
# 微信公众号：ITester软件测试小栈
拷贝容器coco的tmp文件夹下的info.txt到宿主机的当前位置
docker cp coco:/tmp/info.txt .
```



**四**

**日志命令**

```javascript
# 微信公众号：ITester软件测试小栈
docker logs -f -t --tail 10 容器ID或容器名称
```

**参数说明：**

```javascript
# 微信公众号：ITester软件测试小栈
# 加入时间戳
-t
# 跟随最新的日志打印
-f
# 输出最后几行的日志
--tail 行数
```

```
docker exec -it 容器名 命令
```

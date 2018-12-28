
## 28/12 晴

### 1. kubelet GC机制
>今天发现当镜像所在磁盘使用率超过85%时，kubelet会开始清除镜像。查阅资料发现是GC机制搞得鬼！kubelet默认每1min会执行容器的GC操作，默认根据磁盘使用情况执行镜像的GC操作，之后更该docker默认镜像存储目录到空间更大磁盘解决问题。[参考](https://www.cnblogs.com/cf532088799/p/7865952.html "https://www.cnblogs.com/cf532088799/p/7865952.html")
### 2. 更该docker默认镜像存储目录
#### 2.1 修改`docker.service`文件
```shell
vim /etc/systemd/system/multi-user.target.wants/docker.service
ExecStart=/usr/bin/dockerd --graph=/data/docker --storage-driver=overlay --registry-mirror=https://jxus37ad.mirror.aliyuncs.com
```
* --graph=/data/docker 新的存储位置<br>
* --storage-driver=overlay 当前存储驱动(选填)<br>
* --registry-mirror 镜像仓库地址(选填)<br>
#### 2.2 重启docker
```shell
systemctl daemon-reload
systemctl restart docker
```
>[参考](https://www.cnblogs.com/bigberg/p/8057807.html "https://www.cnblogs.com/bigberg/p/8057807.html")
### 3. kubectl expose
```shell
kubectl expose (-f FILENAME | TYPE NAME) [--port=port] [--protocol=TCP|UDP] [--target-port=number-or-name] [--name=name] [--external-ip=external-ip-of-service] [--type=type] [-n namespace]
```
* --port=port svc监听端口
* --target-port 容器端口
* --external-ip 外部ip
* -n namespace 默认default
>[参考](https://www.kubernetes.org.cn/2377.html "https://www.kubernetes.org.cn/2377.html")



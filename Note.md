
# 28/12 晴
## 1.kubelet GC机制
>>今天发现当镜像所在磁盘使用率超过85%时，kubelet会开始清除镜像。查阅资料发现是GC机制搞得鬼！kubelet默认每1min会执行容器的GC操作，默认根据磁盘使用情况执行镜像的GC操作，之后更该docker默认镜像存储目录到空间更大磁盘解决问题。关于kubelet的GC机制参见这篇博文https://www.cnblogs.com/cf532088799/p/7865952.html

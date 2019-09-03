# k8s实践(七)：存储卷和数据持久化(Volumes and Persistent Storage)

<br>

**环境说明：**

 
| 主机名 | 操作系统版本 | ip | docker version | kubelet version | 配置 | 备注 |
| :------: | :------:  | :------: | :------: | :------: | :------: |:------: |
| master | Centos 7.6.1810 | 172.27.9.131 |Docker 18.09.6 | V1.14.2 | 2C2G | master主机 |
| node01 | Centos 7.6.1810 | 172.27.9.135 |Docker 18.09.6 | V1.14.2 | 2C2G | node节点 |
| node02 | Centos 7.6.1810 | 172.27.9.136 |Docker 18.09.6 | V1.14.2 | 2C2G | node节点 |
| centos7 | Centos 7.3.1611 | 172.27.9.181 | × | × | 1C1G | nfs服务器 |


<br>

&emsp;&emsp;Kubernetes的卷是pod的一个组成部分，因此像容器一样在pod的规范中就定义了。它们不是独立的Kubernetes对象，也不能单独创建或删除。pod中的所有容器都可以使用卷，但必须先将它挂载在每个需要访问它的容器中。在每个容器中，都可以在其文件系统的任意位置挂载卷。


<br>

&emsp;&emsp;容器磁盘上的文件的生命周期是短暂的，这就使得在容器中运行重要应用时会出现一些问题。首先，当容器崩溃时，kubelet会重启它，但是容器中的文件将丢失——容器以干净的状态（镜像最初的状态）重新启动。其次，在 Pod 中同时运行多个容器时，这些容器之间通常需要共享文件。Kubernetes 中的 Volume 抽象就很好的解决了这些问题。



<br>

&emsp;&emsp;本文将对emptyDir,hostPath,共享存储NFS,PV及PVC分别进行测试实践。
<br>
<br>

**文章目录：**
# 一、Volume
## 1. 概念
## 2. 为什么需要Volume
### 3. Volume类型
# 二、emptyDir
## 1. emptyDir概念
## 2. 创建pod emptyDir-fortune
### 2.1 loong576/fortune镜像
## 3. 访问nginx
### 3.1 创建service
### 3.2 nginx访问
# 三、hostPath
## 1. 概念
## 2. 创建pod hostpath-nginx
### 2.1 创建挂载目录
### 2.2 创建pod
## 3. 访问pod hostpath-nginx
# 四、NFS共享存储
## 1. 概念
## 2. nfs搭建及配置
## 3. 新建pod mongodb-nfs
## 4. nfs共享存储测试
### 4.1 向MongoDB写入数据
### 4.2 查看写入的数据
### 4.3 删除pod并重建
### 4.4 新pod读取共享存储数据
# 五、PV and PVC
## 1. 概念
## 2. 创建PV
### 2.1 nfs配置
## 2.2 PV创建
## 3. 创建PVC
### 3.1 PVC创建
### 3.2 查看选中的PV
## 4. pod中使用PVC



<br>
<br>

**详细搭建过程及测试：**

https://blog.51cto.com/3241766/2431728





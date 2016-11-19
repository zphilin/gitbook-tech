# 使用docker搭建hadoop集群

### 制作基于ubuntu的Hadoop基础镜像

> 文中使用的到的docker知识及命令可参考 Docker基础
> 
> 在开始之前需确保已安装好docker环境

#### 安装JAVA

```
#由于hadoop运行需要java环境，在宿主机新建一个容器用于配置java及安装hadoop
docker run -it ubuntu
apt-get install software-properties-common python-software-properties 
add-apt-repository ppa:webupd8team/java
apt-get update 
apt-get install oracle-java7-installer 
java -version
```

#### 安装Hadoop

```
cd ~
mkdir soft
cd soft
mkdir hadoop
wget http://mirrors.sonic.net/apache/hadoop/common/hadoop-2.6.5/hadoop-2.6.5.tar.gz
tar -zxvf hadoop-2.6.5.tar.gz
```








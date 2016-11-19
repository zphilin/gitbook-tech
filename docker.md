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

vim ~/.bashrc
export JAVA_HOME=/usr/lib/jvm/java-7-oracle 
export HADOOP_HOME=/root/soft/hadoop/hadoop-2.6.5 
export HADOOP_CONFIG_HOME=$HADOOP_HOME/etc/hadoop 
export PATH=$PATH:$HADOOP_HOME/bin 
export PATH=$PATH:$HADOOP_HOME/sbin
```

#### 配置Hadoop

分别配置 **core-site.xml**、**hdfs-site.xml**、**mapred-site.xml三个文件**

```
cd $HADOOP_CONFIG_HOME
mkdir tmp
mkdir namenode
mkdir datanode
#创建各节点的存放目录用于配置
```

vim core-site.xml 配置configuration中的property 如下

> &lt;configuration&gt;
> 
>  &lt;property&gt;
> 
>  &lt;name&gt;hadoop.tmp.dir&lt;\/name&gt;
> 
>  &lt;value&gt;\/root\/soft\/hadoop\/hadoop-2.6.5\/tmp&lt;\/value&gt;
> 
>  &lt;description&gt;A base for other temporary directories.&lt;\/description&gt;
> 
>  &lt;\/property&gt;
> 
>  &lt;property&gt;
> 
>  &lt;name&gt;fs.default.name&lt;\/name&gt;
> 
>  &lt;value&gt;hdfs:\/\/master:9000&lt;\/value&gt;
> 
>  &lt;final&gt;true&lt;\/final&gt;
> 
>  &lt;description&gt;The name of the default file system. A URI whose scheme and authority determine the FileSystem implementation. The  uri's scheme determines the config property \(fs.SCHEME.impl\) naming the FileSystem implementation class. The uri's authority is used to determine the host, port, etc. for a filesystem.
> 
> &lt;\/description&gt;
> 
>  &lt;\/property&gt;
> 
> &lt;\/configuration&gt;

vim hdfs.site.xml 

> &lt;configuration&gt;
> 
>  &lt;property&gt;
> 
>  &lt;name&gt;dfs.replication&lt;\/name&gt;
> 
>  &lt;value&gt;2&lt;\/value&gt;
> 
>  &lt;final&gt;true&lt;\/final&gt;
> 
>  &lt;description&gt;Default block replication.
> 
>  The actual number of replications can be specified when the file is created.
> 
>  The default is used if replication is not specified in create time.
> 
>  &lt;\/description&gt;
> 
>  &lt;\/property&gt;
> 
>  &lt;property&gt;
> 
>  &lt;name&gt;dfs.namenode.name.dir&lt;\/name&gt;
> 
>  &lt;value&gt;\/root\/soft\/hadoop\/hadoop-2.6.5\/namenode&lt;\/value&gt;
> 
>  &lt;final&gt;true&lt;\/final&gt;
> 
>  &lt;\/property&gt;
> 
>  &lt;property&gt;
> 
>  &lt;name&gt;dfs.datanode.data.dir&lt;\/name&gt;
> 
>  &lt;value&gt;\/root\/soft\/hadoop\/hadoop-2.6.5\/datanode&lt;\/value&gt;
> 
>  &lt;final&gt;true&lt;\/final&gt;
> 
>  &lt;\/property&gt;
> 
> &lt;\/configuration&gt;

`cp mapred-site.xml.template mapred-site.xml `

`vim mapred-site.xml`


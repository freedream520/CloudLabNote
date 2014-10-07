# 安装并配置Hadoop开发环境

作者 :  马超  mctt90@gmail.com

---

**1. 配置java开发和运行环境** <br><br>
在ubuntu下可以使用如下命令:
```bash
sudo apt-get install openjdk-7-jre-headless
sudo apt-get install openjdk-7-jdk
```
<br>
测试java代码
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
<br>
```bash
javac HelloWorld.java
java HelloWorld
```
<br>

**2. 修改主机名和hosts文件** <br><br>
将主机名改为master和slave
```bash
sudo vim /etc/hostname
```
<br>
例如将ubuntu07改为master,ubuntu10改为worker01<br>
修改master的hosts文件,并拷贝到每台worker上
```bash
sudo vim /etc/hosts
```
<br>
例如:
```bash
10.0.0.7 master
10.0.0.10 slave01
10.0.0.12 slave02
....
```
<br>

**3. 设置Master免密码登陆到worker** <br><br>
见'SSH免密码登陆'一文
<br>

**4. 复制Hadoop安装包到所有机器** <br><br>
下载hadoop安装包,例如hadoop-1.0.0-bin.tar.gz, 上传到master中, 在传给worker, 然后解压
```bash
tar -zxvf hadoop-1.0.0-bin.tar.gz
scp hadoop-1.0.0-bin.tar.gz alex@worker01:~
scp hadoop-1.0.0-bin.tar.gz alex@worker02:~
...
```
<br>
**5. 编辑配置文件** <br><br>
```bash
cd hadoop-1.0.0/etc/hadoop
vim hadoop-env.sh
```
<br>

仅需要设置JAVA-HOME
```bash
export JAVA-HOME=/usr/lib/jvm/java-7-openjdk-amd64
```
<br>

core-site.xml:
```bash
<configure>
    <property>
        <name>fs.default.name</name>
        <value>hdfs://master:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/</value>
    </property>
</configure>
```
<br>
mapred-site.xml:
```bash
<configure>
    <property>
        <name>mapred.job.tracker</name>
        <value>master:9001</value>
    </property>
</configure>
```
<br>

hdfs-site.xml:
```bash
<configure>
    <property>
        <name>dfs.replication</name>
        <value>3</value>
    </property>
</configure>
```
<br>
masters:
```bash
master
```

slaves:
```bash
worker01
worker02
...
```
<br>

**6. 将配置文件拷贝到各台slave**
```bash
scp hadoop-env.sh core-site.xml hdfs-site.xml masters slaves alex@worker01:~/hadoop-1.0.0/etc/hadoop
```
<br>

# 安装并配置Spark开发环境

作者 ：马超 mctt90@gmail.com

---

**1.  安装java** <br><br>
此步骤略过<br>

**2.  安装scala**<br><br>
必须保证spark与scala的版本对应，一般我都是下载最新版本的scala.<br>
```bash
tar -zxf scala-2.9.3.tgz
mv scala-2.9.3 /usr/lib
vim /etc/profile
# add the following lines at the end
export SCALA_HOME=/usr/lib/scala-2.9.3
export PATH=$SCALA_HOME/bin:$PATH
# save and exit vim
source /etc/profile
# test
scala -version
```
<br>

**3. 下载预编译好的spark**<br><br>
如果不是做源码级别的修改，建议下载预编译好的spark版本，因为自己编译可能出现被墙的情况。fuck GFW <br>

**4. Local模式**

解压
```bash
tar -zxf spark-0.8.0-incubating-bin-hadoop1.tgz
```
<br>
设置SPARK环境变量
```bash
vim ~/etc/profile
# add the following lines at the end
export SPARK_HOME=$HOME/spark-0.8.0
# save and exit vim
# make the bash profile take effect immediately
source /etc/profile
```
<br>

运行spark
```bash
cd $SPARK_HOME
./run-example org.apache.spark.examples.SparkPi local
```
<br>

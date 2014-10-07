# 安装并配置Hadoop开发环境

作者 :  马超  mctt90@gmail.com

---

**配置java开发和运行环境** <br><br>
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

**修改主机名和hosts文件** <br><br>
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

**设置Master免密码登陆到worker** <br><br>
见<SSH免密码登陆>一文
<br>


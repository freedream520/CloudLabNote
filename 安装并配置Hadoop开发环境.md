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




# Java 字节码反编译成汇编

> 本位以windows环境为前提，JDK版本为Oracle Sun JDK8-64位

## Hsdis环境准备

### 1.下载hsdis-amd64.dylib

> 下载地址如下：https://github.com/evolvedmicrobe/benchmarks/blob/master/hsdis-amd64.dylib

### 2.下载hsdis-amd64.dll

> 下载地址如下：https://github.com/atzhangsan/file_loaded

### 3.配置hsdis-amd64.dylib和hsdis-amd64.dll

a.将下载好的hsdis-amd64.dll文件放置在JDK路径下`\jre\bin`目录下。

> e.g. C:\Program Files\Java\jdk1.8.0_161\jre\bin

b.将下载好的hsdis-amd64.dylib文件放置在JDK路径下的`\jre\lib`目录下。

> e.g. C:\Program Files\Java\jdk1.8.0_161\jre\lib

### 4.测试验证是否配置成功

使用命令`java -XX:+UnlockDiagnosticVMOptions -XX:+PrintAssembly -version`验证是否配置成功。如果出现如下所示则说明配置成功。

![image-20210414230849483](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414230849483.png)

### 5.自行构建hsdis(如果你有兴趣的话)

如果你有兴趣自行编译hsdis的话，可以参考如下的几个链接，然后把编译好的文件放在jdk的jre目录下的如上所`3`述路径。

1.http://www.chrisnewland.com/building-hsdis-on-linux-amd64-on-debian-369

2.http://psy-lob-saw.blogspot.com/2013/01/java-print-assembly.html

## JITWatch环境

### 1.下载JITWatch

> 下载路径如下：https://github.com/AdoptOpenJDK/jitwatch/releases

如果你有兴趣的话，当然也可以参考官方文档进行编译。

JITWatch链接如下：

> https://github.com/AdoptOpenJDK/jitwatch

编译命令如下：

```shell
ant编译：
ant clean compile test run
maven编译：
mvn clean compile test exec:java
gradle编译：
gradlew clean build run
```

### 2.配置运行JITWatch

a.启动，使用`java -jar jitwatch-ui-1.4.0-shaded-win.jar`启动jitwatch，启动成功后如下所示

![image-20210414232505669](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414232505669.png)

b.配置，点击`sandbox`按钮打开窗口，再点击`Configure Sandbox`按钮，配置如下几个参数

> 1.java classes目录
>
> 2.java 运行目录为你本地的配置使用的JDK路径
>
> 3.java运行参数，添加hsdis的运行参数配置

![image-20210414233652204](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414233652204.png)

c.运行，点击`open`按钮打开需要编译的java代码，点击`Run`按钮运行得到下图所示

![image-20210414232726380](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414232726380.png)

![image-20210414234418226](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414234418226.png)



### 3.JITwatch简单使用

#### 模块化查看字节码和汇编码

![image-20210414234700267](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414234700267.png)

#### 使用topList查看资源占用率

在JITWatch窗口点击`TopList`按钮，即可查看资源占用率。

![image-20210414235239556](https://new-blog-1251602255.cos.ap-shanghai.myqcloud.com/img/image-20210414235239556.png)

#### 更多资料

1.https://www.chrisnewland.com/images/jitwatch/HotSpot_Profiling_Using_JITWatch.pdf

2.https://github.com/AdoptOpenJDK/jitwatch/wiki

## 参考文章

1.利用hsdis和JITWatch查看分析HotSpot JIT compiler生成的汇编代码.https://blog.csdn.net/hengyunabc/article/details/26898657

2.JITWatch Wiki.https://github.com/AdoptOpenJDK/jitwatch/wiki
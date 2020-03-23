## 实用的Java编程技巧之命名攻略

### 一、命名工具推荐

> 1.命名神器：[CODELF](https://unbug.github.io/codelf/)
>
> 2.翻译神器：[Google translate](https://translate.google.cn/)
>
> 3.国内比较良心的翻译工具：[有道翻译](http://fanyi.youdao.com/)

### 二、命名策略

1.命名，命名应该使用纯英文命名，而不使用拼音或者不明其意的英语表达。

**正例:** life/game

**反例:** shenghuo/youxi

2.包名定义，包名应该使用小写，每一个点之间仅有一个自然单词，且每一个自然单词应该使用单数形式。

**正例:** net.java.util

**反例:** net.java.utils

3.类名定义，类名使用**UpperCamelCase**风格，但**DO/BO/DTO/PO/VO/UID等业务类型除外**。

**正例:** Book/BookService/BookDTO/TcpService

**反例:** BookDto/BookSERVICE/TCPService

4.方法名、参数名、成员变量、局部变量都使用**lowerCamelCase**风格。

**正例:** getName()/userInformation

**反例:** GetName()/UserInformation

5.常量命名，常量命名使用大写命名，且每个单词间使用下划线"_"进行分割。

**正例:** SUM_COUNT/MAX_VALUE

**反例:** Sum_Count/MAXVALUE

6.抽象类使用Abstract/Base开头，异常处理类使用Exception类结尾，测试类使用Test结尾。

**正例:** AbstractMessage/MessageException

**反例:** Message/MessageExcep/TestMessage

7.枚举类命名，应该以Enum结尾，且枚举类中成员名称需要全部使用大写,且单词之间使用下划线"_"进行分割。

**正例:** ErrorMessageEnum  

**正例:** SUCCESS/FAILED

**反例:** ErrorMessage

**反例:** success/failed

8.定义数组类型，类型应与中括号紧紧相连。

**正例:** int[] message, String[] agrs

**反例:**  int message[], String args[]

9.接口的方法和属性不加任何修饰符(包括public也不加)，并且使用javadoc对每个接口或者属性进行注释说明。

**正例:**

```java
/** 
 * 获取用户信息 
 */
void getUserInformation();
```

**反例:**

```java
//获取用户信息
public void getUserInformation();
```

10.对于接口和实现类的命名约束。

①.对于DAO类和Service类，基于SOA理念，暴露出来的一定是接口，内部实现类使用Impl进行实现。

**正例:** MessageDAO/MessageService接口对应MessageDAOImpl与MessageServiceImpl实现类

```java
public interface MessageDAO {
    /**     
     * 用于发送信息     
     */    
    void send();
}
```
```java
public class MessageDAOImpl implements MessageDAO {
    @Override
    public void send() {
        //todo
    }
}
```

**反例:** MessageDAO类与MessageService类

```java
public class MessageDAO {
    public void send() {
        //todo
    }
}
```

②.如果接口表示能力，应该取名为对应的形容词接口(推荐)。

**正例:** Comparable/Translatable

**反例:** Translate

备注：以上内容来自于阿里巴巴开发手册[阿里巴巴Java开发手册](https://yq.aliyun.com/download/2720?utm_content=m_1000019584)


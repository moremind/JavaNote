# Java基础

面向对象设计模式

1.GoF 23:23中设计模式，构建、结构、行为

2.方法设计：名称、访问性、参数、返回类型、异常

3.泛型设计：类级别、方法级别

4.异常设计：层次性、传播性



## 方法设计

* 单元：一个雷或者一组类

  * 类采用名词结构
    * 动词过去式+名词(ContextRefreshedEvent)
    * 动词ing+名词(InitalizingBean)
    * 形容词+名词(ConfigurableApplicationContext)

* 执行：某个方法

  * 方法命名：动词

    * execute
    * run
    * callback

  * 方法参数：名词

  * 异常

    * 根(顶层)异常

      * Throwable
        * checked类型：Exception
        * unchecked类型：RuntimeException
        * 不常见：Error

    * Java1.4  `java.lang.StackTraceElement`
    	* 添加异常原因(cause)
    	
    	  ```java
    	  /**
    	    * The throwable that caused this throwable to get thrown, or null if this
    	    * throwable was not caused by another throwable, or if the causative
    	    * throwable is unknown.  If this field is equal to this throwable itself,
    	    * it indicates that the cause of this throwable has not yet been
    	    * initialized.
    	    *
    	    * @serial
    	    * @since 1.4
    	    */
    	      private Throwable cause = this;
    	  ```
    	
    	  * 反模式：吞到某个异常中
    	  * 性能：注意`fillInStackTrace()`方法的开销，避免异常栈调用深度。
    	    * 方法一：JVM参数控制栈深度(物理屏蔽)
    	    * 方法二：logback日志框架控制堆栈输出深度(逻辑屏蔽)

## 泛型设计

Java泛型属于编译时处理，运行时擦写。



## Java函数式设计

### 匿名内置类

基本特性：

* 无名称类
* 声明位置(执行模块):
  * static block
  * 实例block
  * 方法、block内部或者代码

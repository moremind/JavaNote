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
  * 构造器
* 并非特殊的类结构
  * 类全名称：${package}.${declared_class}.${num}.class

### Lambda表达式

* 基本特点
  * 流程编排清晰
  * 函数类型编程
  * 改善代码臃肿
  * 兼容接口升级
* 实现手段
  * @FunctionInterface 接口
  * Lambda语法
  * 方法引用
  * 接口default方法实现
* 编程局限
  * 单一抽象方法
  * Lambda调试困难
  * Stream API操作能力有限

```java
		//匿名类传统写法
        new PropertyChangeListener() {
            @Override
            public void propertyChange(PropertyChangeEvent evt) {
                println(evt);
            }
        };

        // Lambda基本写法
        PropertyChangeListener listener = evt -> {
            println(evt);
        };

        //lambda简略写法
        PropertyChangeListener listener1 = LambdaDemo::println;

```

**四种模式**

```java
    // SCFP = Supplier + Consumer + Function + Predicate
    // 四种模式(缺啥Action模式)
    // Action 模式
    private static void showAction() {
        Runnable runnable = new Runnable() {
            @Override
            public void run() {

            }
        };
        Runnable runnable1 = () -> {};

        Runnable runnable2 = () -> {
        };
    }
    
    // Supplier模式
    private static void showSupplier() {

        String string = "Hello, World";

        Supplier<String> stringSupplier = () -> "Hello, World";
        Supplier<String> stringSupplier1 = () -> new Integer(2).toString();

    }

    // Consumer模式
    private static void showConsumer() {
        //匿名类传统写法
        new PropertyChangeListener() {
            @Override
            public void propertyChange(PropertyChangeEvent evt) {
                println(evt);
            }
        };
        // Lambda基本写法
        PropertyChangeListener listener = evt -> {
            println(evt);
        };

        //lambda简略写法
        PropertyChangeListener listener1 = LambdaDemo::println;
    }

    // Function 模式，有输入有输出
    private static void showFunction() {
        Function<String, Integer> f = LambdaDemo::compareTo;
    }
    private static Integer compareTo(String value) {
        return value.compareTo("Hello, World");
    }
```


### 函数式接口

基本特性

* 所有的函数式接口都引用一段执行代码
* 函数式接口没有固定的类型，固定模式（// SCFP = Supplier + Consumer + Function + Predicate）+ Action
* 利用方法引用来实现模式匹配



## 模块化设计基础

### 强封装性

基本特性

* 并非所有的public class 都可以被运用，需要使用`exports`来配合。
* `exports`所配置的package下并需要有Class
* 对人的要求就高了，必须了解module-info.java
  * 1.必须了解相关`module-info.java`语义
  * 2.需要了解某些类的依赖
  * 需要了解某些类的职责
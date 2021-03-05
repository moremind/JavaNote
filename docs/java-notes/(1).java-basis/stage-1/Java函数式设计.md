# Java函数式设计

* 理解@FunctionInterface

  * 函数式接口类型

    * 提供类型 - Supplier<T>

    ```java
    	public static void main(String[] args) {
            Supplier<Long> supplier = getLong();
    
            Callable<String> callable = new Callable<String>() {
                @Override
                public String call() throws Exception {
                    return getHelloWorld();
                }
            };
    
            Callable<String> callable2 = SupplierDemo::getHelloWorld;
    
        }
        public static String getHelloWorld() {
            return "Hello World";
        }
    
        public static Supplier<Long> getLong() {
            return System::currentTimeMillis;
        }
    ```

    * 消费类型 - Consumer<T>

    ```java
        public static void main(String[] args) {
            Consumer consumer = System.out::println;
            Consumer<String> consumer2 = ConsumerDemo::echo;
    
            // Fluent API
            // consumer2 -> consumer -> consumer
            consumer2.andThen(consumer).andThen(consumer).accept("Hello");
        }
        private static void echo(String message) {
            System.out.println(message);
        }
    ```

    * 转换类型 - Function<T, R>

    ```java
        public static void main(String[] args) {
            Function<String, Long> stringLongFunction = Long::valueOf;
            System.out.println(stringLongFunction.apply("1"));
    
            Function<Long, String> stringFunction = String::valueOf;
            System.out.println(stringFunction.apply(1L));
    
            Long value = stringLongFunction.compose(String::valueOf).apply(1L);
        }
    ```

    * 断定类型 - Predicate<T>

    ```java
        public static void main(String[] args) {
            Predicate<File> predicate = file -> {
                return false;
            };
        }
    ```

    * 隐藏类型 - Action

    ```java
        // 匿名内置类
        Runnable runnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("Hello");
            }
        };
        Runnable runnable2 = () -> {
        };
    ```

    

* 函数式接口设计

  * Supplier

  ```java
  public static void main(String[] args) {
          echo("Hello,World"); // 固定参数
          echo(() -> { // 变化实现
              sleep(1000);
              return "Hello,World";
          });
          echo(SupplierDesignDemo::getMessage);
  
          getMessage(); //及时返回数据
  
          Supplier<String> message = supplyMessage(); // 待执行
  
          message.get(); // 实际执行
      }
  
      public static String getMessage() {
          sleep(1000);
          return "Hello,World";
      }
      private static Supplier<String> supplyMessage() {
          return SupplierDesignDemo::getMessage;
      }
  
      private static void sleep(long millis) {
          try {
              Thread.sleep(millis);
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
      }
  
      public static void echo(String message) { // 拉模式
          System.out.println(message);
      }
  
      public static void echo(Supplier<String> message) { // 推模式
          System.out.println(message.get());
  
      }
  ```

  * Function

  ```java
      public static void main(String[] args) {
          Function function = a -> a;
          // Function 可以用于同类转化
          Function<Integer, Integer> divide2 = a -> a / 2;
      }
  ```

  * Predicate

  ```java
      public static void main(String[] args) {
          List<Integer> number = Arrays.asList(1, 2, 3, 4, 5);
          Collection<Integer> even = filter(number, num -> num % 2 == 0);
          System.out.println(even);
      }
  
      private static <T> Collection<T> filter(Collection<T> source, Predicate<T> predicate) {
          //集合类操作，亲不要直接利用参数
          List<T> copy = new ArrayList<>(source);
          Iterator<T> iterator = copy.iterator();
          while (iterator.hasNext()) {
              T element = iterator.next();
              if (!predicate.test(element)) {
                  iterator.remove();
              }
          }
          return Collections.unmodifiableList(copy);
      }
  ```

* 函数式在框架中的运用

* Stream API设计

  * 转化：Stream#map(Function)
  * 过滤：Stream#filter(Predicate)
  * 排序
    * Stream#sorted()
    * Stream#sorted(Comparator)

  ````java
  public static void main(String[] args) {
          count(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
          sort(6, 2, 3, 1, 9, 7);
          sort((x, y) -> (x < y) ? 1 : ((x == y) ? 0 : -1),
                  6, 2, 3, 1, 9, 7);
          parallelSort(6, 2, 3, 1, 9, 7);
      }
  
      private static void println(Object object) {
          System.out.printf("[%s] : %s\n", Thread.currentThread().getName(), object);
      }
  
      private static void parallelSort(Integer... numbers) {
          Stream.of(numbers)
                  .sorted()
                  .parallel()
                  .forEach(StreamDemo::println);
      }
  
      private static void count(Integer... numbers) {
          Stream.of(numbers)
                  .reduce(Integer::sum)
                  .ifPresent(System.out::println);
      }
      
      private static void sort(Integer... numbers) {
          Stream.of(numbers)
                  .sorted()
                  .forEach(System.out::println);
      }
      private static void sort(Comparator<Integer> comparator, Integer... numbers) {
          Stream.of(numbers)
                  .sorted(comparator)
                  .forEach(System.out::println);
      }
  ````

  
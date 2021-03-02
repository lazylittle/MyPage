##java多线程
### 多线程的用处
将长耗时的操作放到线程中执行,避免程序长时间等待,提高程序的执行效率。
并发执行一个任务加快任务的执行效率
### 实现方式
#### 继承thread类，重写run方法
```java
public class threadtestclass {
    public static void main(String[] args) {
        Thread mythread = new threadtest();
        mythread.start();
        System.out.println("这里是一个主线程");
    }

}
class threadtest extends Thread {
    @Override
    public void run() {
        System.out.println("这里是一个子线程");
    }
}

```
####实现Runnable接口，并用其初始化Thread，然后创建Thread实例，并调用start方法
```java

public class threadtestclass {
    public static void main(String[] args) {
        Thread mythread = new Thread(new threadtest());
        mythread.start();
        System.out.println("这里是一个主线程");
    }
}
class threadtest implements Runnable {
    @Override
    public void run() {
        System.out.println("这里是一个子线程");
    }
}
```
####可以使用lambda表达式进行简化
```java
 public static void main(String[] args)  {

        Thread t = new Thread(()->{
            System.out.println("这里是一个子线程");
        });
        t.start();
        System.out.println("这里是一个主线程");
    }
```
###实现Callable接口,重写call方法，此方法具有返回值
```java
public class threadtestclass {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        Callable<String> c = new threadtest();
        //用于接收线程的返回值
        FutureTask<String> ft = new FutureTask<String>(c);
        Thread t = new Thread(ft);
        t.start();
        System.out.println("这里是一个主线程");
        t.join();
        System.out.println(ft.get());
    }
}
class threadtest implements Callable<String> {
    @Override
    public String call() throws Exception {
        System.out.println("这里是一个子线程");
        return "返回子线程";
    }
}
```
###使用线程池进行线程
```java

public class threadtestclass {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
            ExecutorService executorService = Executors.newFixedThreadPool(5);
            //没有返回值的方法
            executorService.execute(new threadtest());
            FutureTask<String> ft = new FutureTask<String>(new threadtest2());
            //有返回值的方法
            executorService.submit(ft);
            executorService.shutdown();
            System.out.println(ft.get());

    }
}
class threadtest implements Runnable {
        @Override
    public void run() {
        System.out.println("这里是一个子线程");
    }
}
class threadtest2 implements Callable<String> {
    @Override
    public String call() throws Exception {
        System.out.println("有返回值的子线程");
        return "返回值";
    }
}

```

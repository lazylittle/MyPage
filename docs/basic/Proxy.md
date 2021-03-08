##动态代理
代理(Proxy)是一种设计模式,提供了对目标对象另外的访问方式;即通过代理对象访问目标对象.这样做的好处是:可以在目标对象实现的基础上,增强额外的功能操作,即扩展目标对象的功能.
这里使用到编程中的一个思想:不要随意去修改别人已经写好的代码或者方法,如果需改修改,可以通过代理的方式来扩展该方法
###代理的作用
在不改动原有代码的情况下，增加对象方法的扩展和统一处理，例如统一异常处理，统一日志记录
###静态代理
静态代理就是通过重写接口方法达成的
```java

interface ITestServices {
    void sayHello();
}
class TestServicesImpl implements ITestServices {
    @Override
    public void sayHello() {
        System.out.println("hello world");
    }
}
//此处的类同样实现了sayHello方法 并且没有改变TestServicesImpl类的sayHello方法逻辑
class ProxyTestServicesImpl implements ITestServices{
    ITestServices target;
    public ProxyTestServicesImpl(ITestServices testServices){
        target=testServices;
    }
    @Override
    public void sayHello() {
        System.out.println("静态代理实现");
        target.sayHello();
    }
}
public class poxyclass {
    public static void main(String[] args) {
        TestServicesImpl testServices = new TestServicesImpl();
        ITestServices proxyTestServices=new ProxyTestServicesImpl(testServices);
        proxyTestServices.sayHello();

    }
}
```
输出结果
![tupian](icon/静态代理结果.png)

###动态代理

动态代理中最重要的两个类Proxy和InvocationHandler，用于创建对象和扩展方法


```java

interface ITestServices {
    void sayHello();
}

class TestServicesImpl implements ITestServices {
    @Override
    public void sayHello() {
        System.out.println("hello world");
    }
}

class Logger implements InvocationHandler {
    Object target;

    public Logger(Object targets) {

        target = targets;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        doSomethingBefore();
        Object result = method.invoke(target, args);
        doSomethingAfter();
        return result;
    }

    private void doSomethingBefore() {

        System.out.println("动态代理测试:方法执行之前");
    }

    private void doSomethingAfter() {

        System.out.println("动态代理测试:方法执行之后");
    }
}

public class poxyclass {
    public static void main(String[] args) {

        TestServicesImpl testServices = new TestServicesImpl();
        Logger logger = new Logger(testServices);
        ITestServices proxTestServices = (ITestServices) Proxy.newProxyInstance(TestServicesImpl.class.getClassLoader(), TestServicesImpl.class.getInterfaces(), logger);
        proxTestServices.sayHello();
    }
}

```
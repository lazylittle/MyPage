##注解
###什么是注解
注解就是JAVA 中的一种注释机制，标注的值会被嵌入到字节码文件中,使得注解可以java读取到
###注解的作用
* 可以用来代替配置文件
* 大量的框架使用了注解
###内置注解
java的内置注解
#### 作用于代码
* @Override - 检查该方法是否是重写方法。
* @Deprecated - 标记过时方法。
* @SuppressWarnings - 指示编译器去忽略注解中声明的警告。
* @SafeVarargs - Java 7 开始支持，忽略任何使用参数为泛型变量的方法或构造函数调用产生的警告。只能用于标记构造函数和方法。
* @FunctionalInterface - Java 8 开始支持，标识一个匿名函数或函数式接口。该注解只能标记在"有且仅有一个抽象方法"的接口上。
#### 作用于其他注解（元注解）
* @Retention - 标识这个注解怎么保存，是只在代码中，还是编入class文件中，或者是在运行时可以通过反射访问。
* @Documented - 标记这些注解是否包含在用户文档中。
* @Target - 标记这个注解应该是哪种 Java 成员。
* @Inherited - 标记这个注解是继承于哪个注解类(默认 注解并没有继承于任何子类)。
* @Repeatable - Java 8 开始支持，标识某注解可以在同一个声明上使用多次。
###自定义注解
####语法
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface testannotation {
    int show();
    String show2();
    String show3() default "4";
}
```                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
####使用注解
```java
//show3属性有默认值可以不用赋值

@testannotation(show = 2, show2 = "3")
public class streamClass {
    public static void main(String[] args) throws ClassNotFoundException {
        streamClass t = new streamClass();
        Class<?> c1 = t.getClass();
        testannotation ano = c1.getAnnotation(testannotation.class);
        System.out.println( ano.show());
        //是否包含指定的注解
        System.out.println(c1.isAnnotationPresent(testannotation.class));
    }
}
```


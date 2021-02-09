##反射
###什么是反射
对于任何一个类,都能够获取到这个类的所有属性和方法,对于任意一个对象，都能够调用它的任意一个方法和属性.
这种动态获取的信息以及动态调用对象的方法的功能就称为java语言的反射机制
###获取类的构造函数
```java
 Class c1 = Class.forName("java.lang.String");            
            //获取所有的构造函数(public)
            Constructor[] constructors = c1.getConstructors();
            for (Constructor c : constructors) {
                 System.out.println(c);
            }
            //获取所有声明的构造函数(包括private)
            Constructor[] constructors1 = c1.getDeclaredConstructors();
            for (Constructor c : constructors1) {
                System.out.println(c);
            }
```
###创建对象
```java
 Class c1 = Class.forName("java.lang.String");
            //调用默认构造函数
            object obj1= c1.newInstance();
            //调用指定构造函数
            Constructor con1 = c1.getConstructor(char[].class); //获取入参为char[] 的构造函数
            char[] chars = new char[]{'h', 'e', 'l', 'l', 'o', ',', 'w', 'o', 'r', 'l', 'd'};
            Object obj = con1.newInstance(chars);
            System.out.println(obj);
            //使用私有的构造函数
            con1.setAccessible(true);
            Object obj2 = con1.newInstance();
```
###获取对象的属性
```java
            Class c1 = Class.forName("student");
            //获取所有public的属性
            Field[] fields = c1.getFields();
            for (Field field : fields) {
                System.out.println(field);
            }
            //获取所有声明的属性，包括private
            Field[] fields1=c1.getDeclaredFields();
            for (Field field : fields1) {
                System.out.println(field);
            }
```
###为对象的属性赋值
```java
            Class c1=Class.forName("student");
            //创建对象
            Object obj=c1.newInstance();
            //获取属性
            Field field= c1.getField("name");
            //设置属性的值
            field.set(obj,"123");
            System.out.println(field.get(obj));
```
###获取对象的方法
```java
            Class c1 = Class.forName("student");
            //创建对象
            Object obj = c1.newInstance();
            //获取方法 public
            Method[] methods = c1.getMethods();
            for (Method method : methods) {
                System.out.println(method);
            }
            //获取方法 包括private
            Method[] methods2 = c1.getDeclaredMethods();
            for (Method method : methods2) {
                System.out.println(method);
            }
```
###调用对象的方法
```java
            Class c1 = Class.forName("student");
            //创建对象
            Object obj = c1.newInstance();
            //获取方法 public
            Method methods = c1.getMethod("printf");
            //获取私有的方法
            Method method2 = c1.getDeclaredMethod("print",int.class);
            method2.setAccessible(true);
            //调用
            System.out.println(methods.invoke(obj));
```


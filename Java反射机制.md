# Java反射机制

反射机制：在**运行状态**中，对于任意一个类，能知道该类的所有属性和方法；对于任意一个对象，能调用它的任意方法和属性。（程序在运行时获取自身的信息）（给定一个类的名字就可以通过反射机制获取该类的所有信息）

<img src="http://c.biancheng.net/uploads/allimg/191213/5-19121314235A02.png" alt="img" style="zoom: 67%;" />

```java
	//方式一：调用运行时类的属性：.class
    Class<Person> clazz1 = Person.class;
    System.out.println(clazz1);//class cn.bruce.java.Person
 
    //方式二：通过运行时类的对象,调用getClass()
    Person p1 = new Person();
    Class<? extends Person> clazz2 = p1.getClass();
    System.out.println(clazz2);//class cn.bruce.java.Person
 
    //方式三：调用Class的静态方法：forName(String classPath)
    Class<?> clazz3 = Class.forName("cn.bruce.java.Person");
    System.out.println(clazz3);//class cn.bruce.java.Person
 
    //方式四：使用类的加载器：ClassLoader  (了解)
    ClassLoader classLoader = ReflectionTest.class.getClassLoader();
    Class<?> clazz4 = classLoader.loadClass("cn.bruce.java.Person");
    System.out.println(clazz4);//class cn.bruce.java.Person
    System.out.println(clazz1 == clazz4);//true
```



> Java 反射机制主要提供了以下功能，这些功能都位于`java.lang.reflect`包。

- 在运行时**判断**任意一个对象**所属的类**。
- 在运行时**构造**任意一个**类的对象**。
- 在运行时**判断**任意一个类所具有的**成员变量和方法**。
- 在运行时**调用**任意一个**对象的方法**。
- 生成**动态代理**。

> 要想知道一个类的属性和方法，必须先获取到该类的字节码文件对象。获取类的信息时，使用的就是 Class 类中的方法。所以先要获取到每一个字节码文件（.class）对应的 Class 类型的对象.
>
> 所有 Java 类均继承了 Object 类，在 Object 类中定义了一个 getClass() 方法，该方法返回同一个类型为 Class 的对象。
>
> ```java
> Class labelCls = label1.getClass();    // label1为 JLabel 类的对象
> ```

![image-20220608231534574](C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220608231534574.png)

#### 反射机制API

#### java.lang.Class 类

反射的和心累，可以获取类的属性、方法等信息

```java
public class ReflectionTest01 {
    public static void main(String[] args) {
        // 获得Class实例
        // 1.通过类型class静态变量
        Class clz1 = String.class;
        String str = "Hello";
        // 2.通过对象的getClass()方法
        Class clz2 = str.getClass();
        // 获得int类型Class实例
        Class clz3 = int.class;
        // 获得Integer类型Class实例
        Class clz4 = Integer.class;
        System.out.println("clz2类名称：" + clz2.getName());
        System.out.println("clz2是否为接口：" + clz2.isInterface());
        System.out.println("clz2是否为数组对象：" + clz2.isArray());
        System.out.println("clz2父类名称：" + clz2.getSuperclass().getName());
        System.out.println("clz2是否为基本类型：" + clz2.isPrimitive());
        System.out.println("clz3是否为基本类型：" + clz3.isPrimitive());
        System.out.println("clz4是否为基本类型：" + clz4.isPrimitive());
    }
}
```

#### java.lang.reflect 包

[java.lang.reflect](http://c.biancheng.net/view/1109.html) 包提供了反射中用到类，主要的类说明如下：

- Constructor 类：提供类的构造方法信息。
- Field 类：提供类或接口中成员变量信息。
- Method 类：提供类或接口成员方法信息。
- Array 类：提供了动态创建和访问 Java 数组的方法。
- Modifier 类：提供类和成员访问修饰符信息。

```java
// 1. 通过类型class静态变量
Class clz1 = String.class;
String str = "Hello";
// 2. 通过对象的getClass()方法
Class clz2 = str.getClass();
```

```java
public class ReflectionTest02 {
    public static void main(String[] args) {
        try {
            // 动态加载xx类的运行时对象
            Class c = Class.forName("java.lang.String");
            // 获取成员方法集合
            Method[] methods = c.getDeclaredMethods();
            // 遍历成员方法集合
            for (Method method : methods) {
                // 打印权限修饰符，如public、protected、private
                System.out.print(Modifier.toString(method.getModifiers()));
                // 打印返回值类型名称
                System.out.print(" " + method.getReturnType().getName() + " ");
                // 打印方法名称
                System.out.println(method.getName() + "();");
            }
        } catch (ClassNotFoundException e) {
            System.out.println("找不到指定类");
        }
    }
}
```

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220609085556344.png" alt="image-20220609085556344" style="zoom:67%;" />

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220609085617970.png" alt="image-20220609085617970" style="zoom: 67%;" />

```java
public class Test01 {
    public static void main(String[] args) {
        // 获取动态类Book
        Class book = Book.class;
        // 获取Book类的所有构造方法
        Constructor[] declaredContructors = book.getDeclaredConstructors();
        // 遍历所有构造方法
        for (int i = 0; i < declaredContructors.length; i++) {
            Constructor con = declaredContructors[i];
            // 判断构造方法的参数是否可变
            System.out.println("查看是否允许带可变数量的参数：" + con.isVarArgs());
            System.out.println("该构造方法的入口参数类型依次为：");
            // 获取所有参数类型
            Class[] parameterTypes = con.getParameterTypes();
            for (int j = 0; j < parameterTypes.length; j++) {
                System.out.println(" " + parameterTypes[j]);
            }
            System.out.println("该构造方法可能拋出的异常类型为：");
            // 获取所有可能拋出的异常类型
            Class[] exceptionTypes = con.getExceptionTypes();
            for (int j = 0; j < exceptionTypes.length; j++) {
                System.out.println(" " + parameterTypes[j]);
            }
            // 创建一个未实例化的Book类实例
            Book book1 = null;
            while (book1 == null) {
                try { // 如果该成员变量的访问权限为private，则拋出异常
                    if (i == 1) {
                        // 通过执行带两个参数的构造方法实例化book1
                        book1 = (Book) con.newInstance("Java 教程", 10);
                    } else if (i == 2) {
                        // 通过执行默认构造方法实例化book1
                        book1 = (Book) con.newInstance();
                    } else {
                        // 通过执行可变数量参数的构造方法实例化book1
                        Object[] parameters = new Object[] { new String[] { "100", "200" } };
                        book1 = (Book) con.newInstance(parameters);
                    }
                } catch (Exception e) {
                    System.out.println("在创建对象时拋出异常，下面执行 setAccessible() 方法");
                    con.setAccessible(true); // 设置允许访问 private 成员
                }
            }
            book1.print();
            System.out.println("=============================\n");
        }
    }
}
```

![image-20220609085718853](C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220609085718853.png)

```java
public class Test02 {
    public static void main(String[] args) {
        // 获取动态类Book1
        Book1 book = new Book1();
        Class class1 = book.getClass();
        // 获取Book1类的所有方法
        Method[] declaredMethods = class1.getDeclaredMethods();
        for (int i = 0; i < declaredMethods.length; i++) {
            Method method = declaredMethods[i];
            System.out.println("方法名称为：" + method.getName());
            System.out.println("方法是否带有可变数量的参数：" + method.isVarArgs());
            System.out.println("方法的参数类型依次为：");
            // 获取所有参数类型
            Class[] methodType = method.getParameterTypes();
            for (int j = 0; j < methodType.length; j++) {
                System.out.println(" " + methodType[j]);
            }
            // 获取返回值类型
            System.out.println("方法的返回值类型为：" + method.getReturnType());
            System.out.println("方法可能抛出的异常类型有：");
            // 获取所有可能抛出的异常
            Class[] methodExceptions = method.getExceptionTypes();
            for (int j = 0; j < methodExceptions.length; j++) {
                System.out.println(" " + methodExceptions[j]);
            }
            boolean isTurn = true;
            while (isTurn) {
                try { // 如果该成员变量的访问权限为private，则抛出异常
                    isTurn = false;
                    if (method.getName().equals("staticMethod")) { // 调用没有参数的方法
                        method.invoke(book);
                    } else if (method.getName().equals("publicMethod")) { // 调用一个参数的方法
                        System.out.println("publicMethod(10)的返回值为：" + method.invoke(book, 10));
                    } else if (method.getName().equals("protectedMethod")) { // 调用两个参数的方法
                        System.out.println("protectedMethod(\"10\",15)的返回值为：" + method.invoke(book, "10", 15));
                    } else if (method.getName().equals("privateMethod")) { // 调用可变数量参数的方法
                        Object[] parameters = new Object[] { new String[] { "J", "A", "V", "A" } };
                        System.out.println("privateMethod()的返回值为：" + method.invoke(book, parameters));
                    }
                } catch (Exception e) {
                    System.out.println("在设置成员变量值时抛出异常，下面执行setAccessible()方法");
                    method.setAccessible(true); // 设置为允许访问private方法
                    isTurn = true;

                }
            }
            System.out.println("=============================\n");
        }
    }
}
```

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220609085914794.png" alt="image-20220609085914794" style="zoom:67%;" />

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
public class Test03 {
    public static void main(String[] args) {
        Book2 book = new Book2();
        // 获取动态类Book2
        Class class1 = book.getClass();
        // 获取Book2类的所有成员
        Field[] declaredFields = class1.getDeclaredFields();
        // 遍历所有的成员
        for(int i = 0;i < declaredFields.length;i++) {    
            // 获取类中的成员变量
            Field field = declaredFields[i];
            System.out.println("成员名称为：" + field.getName());
            Class fieldType = field.getType();
            System.out.println("成员类型为：" + fieldType);
            boolean isTurn = true;
            while(isTurn) {
                try {    
                    // 如果该成员变量的访问权限为private，则抛出异常
                    isTurn = false;
                    System.out.println("修改前成员的值为：" + field.get(book));
                    // 判断成员类型是否为int
                    if(fieldType.equals(int.class)) {
                        System.out.println("利用setInt()方法修改成员的值");
                        field.setInt(book, 100);
                    } else if(fieldType.equals(float.class)) {    
                        // 判断成员变量类型是否为float
                        System.out.println("利用setFloat()方法修改成员的值");
                        field.setFloat(book, 29.815f);
                    } else if(fieldType.equals(boolean.class)) {    
                        // 判断成员变量是否为boolean
                        System.out.println("利用setBoolean()方法修改成员的值");
                        field.setBoolean(book, true);
                    } else {
                        System.out.println("利用set()方法修改成员的值");
                        field.set(book, "Java编程");
                    }
                    System.out.println("修改后成员的值为：" + field.get(book));
                } catch (Exception e) {
                    System.out.println("在设置成员变量值时抛出异常，下面执行setAccessible()方法");
                    field.setAccessible(true);
                    isTurn = true;
                }
            }
            System.out.println("=============================\n");
        }
    }
}
```

#### 反射机制面试题

1. 反射使用步骤：获取Class对象、调用Class对象方法

2. 获取Class对象的3种方法

   1. 调用某个对象的getClass()方法

        ```java
        Person p = new Person();
        Class clazz = p.getClass();
        ```

   2. 调用某个类的class属性来

     ```java
     Class clazz = Person.class
     ```

   3. 使用Class类中的forName()静态方法

    ```java
    Class clazz = Class.forName("类的全路径")
    ```

   

3. 创建对象的两种方法

- 调用Class对象的newInstance()

```java
//使用Class对象的newInstance()方法来创建该Class对象对应的实例。要求对应类有默认的构造函数
Class clazz = Class.forName("reflection.Person");
Person p =(Person)clazz.newInstance();
```

- 调用Constructor对象的newInstance()

```java
//使用Class对象获取指定的Constructor对象 → 调用Constructor对象的newInstance()创建Class类对象的实例
Constructor c = clazz.getDeclaredConstructor(String.class,String.class,int.class);
Person p1 = (Person) c.newInstance("李四","男","20");
```

- 调用对象的方法

```java
Method setAgeMethod = clazz.getMethod("setAge",int.class);
setAgeMethod.invoke(p,12);
```

4. 使用反射机制的实例

- JDBC中，加载数据库驱动程序
- Web服务器中，调用Servlet方法
- Spring框架中，注入属性，调用方法
- ......
[TOC]

### Java基础

#### IDEA常用快捷键

| 快捷键         | 功能                                   |
| -------------- | -------------------------------------- |
| `Alt+Enter`    | 导入包 / 自动补全代码                  |
| `Ctrl+Y`       | 删除光标所在行                         |
| `Ctrl+D`       | 复制光标所在行的内容，插入光标位置下面 |
| `Ctrl+Alt+L`   | 格式化代码                             |
| `Ctrl+L`       | 单行注释，再按取消注释                 |
| `Ctrl+Shift+L` | 多行注释                               |

#### 方法的重载

- 方法的重载：**多个方法的名称（函数名称）一样，但是参数列表不一样**，那么这个方法就是重载。
- 方法重载与下列因素相关：参数的个数不同、参数的类型不同、参数的多个类型顺序不同。方法重载与下列因素无关：与参数的名称无关（形参名称），**与函数的返回值类型无关**。

```java
public class Day01 {
    public static void main(String[] args) {
        int res = add(3, 6);
        System.out.println(res);
        System.out.println("Result is: " + add(3, 6) + "Result is: " + add(3, 6, 9));
    }
	
    // 多个方法的名称一样(add)，但是参数列表不一样。
    public static int add(int a, int b) { // 重载
        int res = a + b;
        return res;
    }

    public static int add(int a, int b, int c) { // 重载
        int res = a + b + c;
        return res;
    }

    public static double add(double a, int b, int c, int d) { // 重载
        double res = a + b + c + d;
        return res;
    }
}
```

#### 数组的初始化

- 数组的动态初始化格式：`数据类型[] 数组名称 = new 数据类型[数据长度]`，动态初始化直接指定长度。
- 数组的静态初始化格式：`数据类型[] 数组名称 = new 数据类型[] {元素1, 元素2, ...}`，动态初始化直接指定内容。
- 获取数组的长度：行长度`array.length`，没有`()`，列长度`array[0].length`。

```java
public static void demoArr() {
    int[] arr1 = new int[10]; // 动态数组
    for (int i = 0; i < arr1.length; i++) {
        System.out.print(arr1[i] + " ");
    }
    System.out.println();
    int[] arr2 = new int[]{1, 2, 3, 5, 9}; // 静态数组
    for (int i = 0; i < arr2.length; i++) {
        System.out.print(arr2[i] + " ");
    }
    System.out.println();
    int[][] arr3 = {{4, 7, 8, 91}, {1, 5, 6, 6, 99}}; // 简写格式静态数组、二维数组
    for (int i = 0; i < arr3.length; i++) {
        for (int j = 0; j < arr3[0].length; j++) {
            System.out.print(arr3[i][j] + " ");
        }
    }
    System.out.println();
}
/*
0 0 0 0 0 0 0 0 0 0 
1 2 3 5 9 
4 7 8 91 1 5 6 6 
*/
```

#### JVM内存划分

- JVM（Java Virtual Machine）的内存划分：

| 区域名称        | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| 寄存器          | 给CPU使用，和我们开发无关。                                  |
| 本地方法栈      | JVM在使用操作系统功能的时候使用，和我们开发无关。            |
| 方法区          | **存储可以运行的class文件**。                                |
| 堆内存          | 存储对象或者数组，**凡是new创建出来的东西，都存储在堆内存中**。堆内存中的东西都有一个地址值：16进制。堆内存里的数据都有默认值：整数为0，浮点数为0.0，字符为'\u0000'，布尔为false，引用类型为null。 |
| 方法栈（Stack） | **方法运行时使用的内存，存放的都是方法中的局部变量**。**方法的运行一定要在栈当中运行**。局部变量：方法的参数，或者是方法体{ }内部的变量。作用域：一旦超出作用域，立刻从栈内存当中消失。 |

![image-20200706181448910](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200706181448910.png)

#### Arrays 排序

|                                        | 功能                                             |
| -------------------------------------- | ------------------------------------------------ |
| `Arrays.toString(array)`               | 数组转字符串（返回字符串）                       |
| `Arrays.sort(array)`                   | 默认升序排列（直接在原数组中排序，无返回值）     |
| `sort(T[] a, Comparator<? super T> c)` | 根据指定比较器产生的顺序对指定对象数组进行排序。 |

```java
public class Day01 {
    public static void main(String[] args) {
        int[] list = new int[]{5, 9, 8, 7, 6, 2};
        // 默认升序排序，默认时可以使用基本类型数组，如int[]
        Arrays.sort(list);

        Integer[] nums = {5, 9, 8, 7, 6, 2};
        // 使用Comparator接口修改规则为升序, 这时nums必须为包装类型【引用类型】
        Arrays.sort(nums, new Comparator<Integer>() {
            @Override
            public int compare(Integer a, Integer b) {
                return b - a;
            }
        });
        System.out.println(Arrays.toString(nums)); // [9, 8, 7, 6, 5, 2]

        // 升序的简写，使用lambda表示式
        Arrays.sort(nums, (a, b) -> (b - a)); // [9, 8, 7, 6, 5, 2]
    }
}
```

#### 类的格式和内存划分

- 类格式：`类名称 对象名 = new 类名称();`。

```java
public class DemoClass {
    String name = "wzk";
    int age = 24;

    public void yourName() {
        System.out.println("Your name is " + name);
    }
}
// 类要在main()中才能被调用
DemoClass stu = new DemoClass();
System.out.println(stu.name); // wzk
stu.yourName(); // Your name is wzk
```

![image-20200706220934157](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200706220934157.png)

![image-20200706221644993](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200706221644993.png)

- 成员方法的参数类型也是可以类。

![image-20200707133013938](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200707133013938.png)

- 成员方法的返回值类型也是可以类。

![image-20200707133715515](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200707133715515.png)

#### private关键字

- `private`关键字的作用及使用：
  - 当类内变量使用了`private`后，这个变量只能在该类内方法中被使用，在其他类内不能被调用使用该变量，如果想要调用，只能使用`Setter`和`Getter`方法的组合来实现。
  - `Setter`方法无返回值，参数类型与成员变量（`name, age`）类型要一致；`Getter`方法无参数，必须有返回值且返回值类型与成员变量（`age`）类型一致。
- 使用了`private`关键字的成员变量，在其他类内只能被**间接访问**（使用`Setter,Getter`方法间接访问），而不能直接访问。

```java
// 具有private变量的类
public class DemoClass {
    String name = "wzk";
    private int age = 24;

    public void setAge(int num) {
        if (num >= 0 && num <= 100) {
            age = num;
        } else {
            System.out.println("age, out of range.");
        }
    }

    public int getAge() {
        return age;
    }
}

// 另一个类试图调用DemoClass类内的变量和方法
public class Day01 {
    public static void main(String[] args) {
        DemoClass stu = new DemoClass();
        System.out.println(stu.name); // stu.name在该类中能被调用
//        System.out.println(stu.age); // stu.age在该类中不能被调用
        stu.setAge(21); // setter方法
        int newAge1 = stu.getAge(); // getter方法
        System.out.println(newAge1); // 这样就改了private age了
    }
}
```

- 当成员变量名`name`和方法的参数名`name`相同时，方法根据”就近原则“会认为**方法中的变量名是参数名而不是成员变量名**。若要正确区分两者：需要在成员变量名`name`前加上`this.`，即是`this.name`。**这个`this`实际上就是被调用的类的地址（即`DemoClass`类的地址）**。

```java
public class DemoClass {
    String name = "wzk";
    int age = 24;

    public void yourAge(int age) {
        if (age >= 0 && age <= 100) {
            this.age = age; // this.age是成员变量名, age是方法的参数
            System.out.println("this代表什么(打印看看)：" + this);
        }
    }
}

public class Day01 {
    DemoClass stu = new DemoClass();
    System.out.println("stu类的地址是：" + stu);
    stu.yourAge(21);
    }
}
/*
stu类的地址是：wzk.DemoClass@312b1dae
this代表什么(打印看看)：wzk.DemoClass@312b1dae
*/
```

#### 构造方法

- **构造方法**（有点像Python的初始化操作`def __init__(self):`）。格式： `public 类名称(参数类型 参数名称)`，**构造方法不能有返回值`return`，方法中也没有`void`**，一般有无参构造方法和全参构造方法。

```java
public class DemoClass {
    String name = "wzk";
    int age = 24;
	
    // 两个构造方法 DemoClass 是【重载】
    public DemoClass(){ // 无参数构造方法
        System.out.println("无参数构造方法");
    }

    public DemoClass(int age, String name){ // 构造方法，无void
        System.out.println("全参数构造方法");
        this.name = name;
        this.age = age;
    } // 无返回值return
}

public class Day01 {
    public static void main(String[] args) {
        DemoClass stu = new DemoClass(); // 使用无参构造
        DemoClass stu2 = new DemoClass(22, "kzw"); // 使用全参构造
        System.out.println("now, name is: " + stu2.name + ", age is: " + stu2.age);
    }
}
/*
无参数构造方法
有参数构造方法
now, name is: kzw, age is: 22
*/
```

#### 标准类的构成

- 一个标准的类（Java Bean）由四部分组成：
  - **所有成员变量都要使用`private`关键字修饰**；
  - 每一个成员变量都有一对 `Getter`、`Setter`方法；
  - 必须有一个无参数的「构造方法」；
  - 必须有一个全参数的「构造方法」。

```java
public class StandardClass {
    private String name = "wzk"; // 成员变量private化
    private int age = 24;
    public StandardClass() {
        System.out.println("无参数构造方法");
    }
    public StandardClass(String name, int age) {
        System.out.println("全参数构造方法");
        this.name = name;
        this.age = age;
    }
    public String getName() {
        System.out.println("Name Getter()方法");
        return name;
    }
    public void setName(String name) {
        System.out.println("Name Setter()方法");
        this.name = name;
    }
    public int getAge() {
        System.out.println("Age Getter()方法");
        return age;
    }
    public void setAge(int age) {
        System.out.println("Age Setter()方法");
        this.age = age;
    }
}

public class Day01 {
    public static void main(String[] args) {
        StandardClass stu = new StandardClass();
        System.out.println("name is: " + stu.getName() + ", age is: " + stu.getAge()); // Getter方法读取private成员变量
        StandardClass stu2 = new StandardClass("kzw", 100);
        stu2.setAge(22);
        stu2.setName("王xx"); // Setter方法修改private成员变量
        System.out.println("name is: " + stu2.getName() + ", age is: " + stu2.getAge());
    }
}
/*
无参数构造方法
Name Getter()方法
Age Getter()方法
name is: wzk, age is: 24
全参数构造方法
Age Setter()方法
Name Setter()方法
Name Getter()方法
Age Getter()方法
name is: 王xx, age is: 22
*/
```

#### 键盘输入API Scanner

- API使用之键盘输入数字。类`java.util.Scanner`，由键盘输入`System.in`，输入字符串`.next()`，输入整数`.nextInt()`。使用过程：`导包 -> 创建 -> 使用`。

```java
import java.util.Scanner; // 1. 导包

public class Day01 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // 2. 创建
        int num = sc.nextInt(); // 3. 使用
        System.out.println("你输入的数字是：" + num); // 【空格】和【回车】都是输入完毕的意思
        String str = sc.next();
        System.out.println("你输入的字符串是：" + str);
    }
}
/*
666
你输入的数字是：666
six six
你输入的字符串是：six
*/
```

#### 匿名对象

- 匿名对象格式：`new 类名称()`。匿名对象只能使用一次，再次使用时不得不重新`new`一个匿名对象。**匿名对象可以作为：方法的参数、方法的返回值**。

```java
public class Day01 {
    public static void main(String[] args) {
        Scanner sc = printScanner(new Scanner(System.in)); // 参数为匿名参数
        String str = sc.next();
        System.out.println("返回的字符串是：" + str);
    }

    public static Scanner printScanner(Scanner sc) {
        int num = sc.nextInt();
        System.out.println("你输入的是：" + num);
        System.out.print("输入你将返回的字符：");
        return new Scanner(System.in); // 返回值也是匿名参数
    }
}
/*
6
你输入的是：6
输入你将返回的字符：six
返回的字符串是：six
*/
```

#### 随机Random API

- API之`Random`类使用：

```java
public class Day01 {
    public static void main(String[] args) {
        Random r = new Random();
        int a = r.nextInt(10);
        System.out.println("[0, 10)范围的随机数是： " + a);
        int b = r.nextInt();
        System.out.println("int范围的随机数是：" + b);
    }
}
/*
[0, 10)范围的随机数是： 3
int范围的随机数是：-1441671585
*/
```

#### 类作为数组类型

- 数组的类型不仅可以是`基本类型 int, float, String`或者`引用类型 Integer, Float`，**还可以是自己定义的类`class`（数组的每个元素存储的是类所在的地址）**。

```java
public class Person {
    private String name = "wzk"; // 成员变量private化
    private int age = 24;
    public Person() {
        System.out.println("无参数构造方法");
    }
}
Person[] arr = new Person[4]; // 定义数组，其类型为Person类，初始值为null
```

#### ArrayList封装的使用

- `ArrayList`类的使用：`public class ArrayList<E> extends AbstractList<E> implements List<E>`
  - 数组的长度一旦定义就不能改变；`ArrayList`对象的**长度可以随时改变**。
  - `ArrayList`的类型 与 其中每一个元素的**类型都必须要保持一致**。
  - 创建方法：`ArrayList<String> arr = new ArrayList<>();` 。
  - `ArrayList<泛型>`，泛型必须是引用类型，不能是基本类型（`byte, short, long, int, float, double, char, boolean`）。**如果希望向集合中添加基本类型，需要使用基本类型的包装类**，即`Byte, Short, Long, Integer, Float, Double, Character, Boolean`，注意`Interger, Character`的写法与其他首字母变大写不同。例如：`ArrayList<Integer> arr = new ArrayList<>();`是正确的， `ArrayList<int> arr = new ArrayList<>();`是错误的。

```java
import java.util.ArrayList;

// .add(), .size(), .remove(), .get()操作
public class Day01 {
    public static void main(String[] args) {
        ArrayList<String> arr = new ArrayList<>();
        arr.add("张三");
        boolean isSuccess = arr.add("李四"); // ArrayList类型的add()操作一定返回true
        System.out.println(isSuccess);
        System.out.println(arr.size());
        
        String getElem = arr.get(1); // 返回值类型即ArrayList类型
        System.out.println(getElem);
        arr.remove(0);
        
        arr.add("one");
        for (int i = 0; i < arr.size(); i++) { // 遍历
            System.out.print(arr.get(i) + " ");
        }
    }
}
/*
true
2
李四
李四 one
*/
```

#### 装箱与拆箱

- **自动装箱与自动拆箱**：
  - 自动装箱：基本类型 ---> 包装类型（引用类型）。
  - 自动拆箱：包装类型 ---> 基本类型。

#### 创建字符串的四种方式

- **创建字符串常见的3+1方法**：
  - `public String()`：创建一个空白字符串，不含有任何内容。
  - `public String(char[] array)`：根据字符数组的内容，来创建对应的字符串。
  - `public String(byte[] array)`：根据字节数组的内容，来创建对应的字符串。
  - 一种直接创建：`String str = "Hello";` ，右边直接用双引号。注意：直接写上双引号，就是字符串对象。

```java
// import java.lang.String类代表字符串。
public class Day01 {
    public static void main(String[] args) {
        // 使用空参构造
        String str1 = new String(); // 小括号留空，说明字符串什么内容都没有。
        System.out.println("第1个字符串：" + str1);
        
        // 根据【字符数组】创建字符串
        char[] charArray = { 'A', 'B', 'C' };
        String str2 = new String(charArray);
        System.out.println("第2个字符串：" + str2);
        
        // 根据【字节数组】创建字符串
        byte[] byteArray = { 97, 98, 99 }; // ASCII 97 -> 'a'
        String str3 = new String(byteArray);
        System.out.println("第3个字符串：" + str3);
        
        // 直接创建
        String str4 = "Hello";
        System.out.println("第4个字符串：" + str4);
    }
}
/*
第1个字符串：
第2个字符串：ABC
第3个字符串：abc
第4个字符串：Hello
*/
```

#### 字符串常量池

- **字符串常量池**：程序当中直接写上双引号的字符串，就在字符串常量池中。
  - 字符串常量池在【堆内存】中。
  - 对于【基本类型】来说，== 是进行【数值】的比较。
  - 对于【引用类型】来说，== 是进行【地址值】的比较。

```java
public class Day01 {
    public static void main(String[] args) {
        String str1 = "abc"; // str1在堆中的字符串常量池内
        String str2 = "abc"; // str2在堆中的字符串常量池内
        
        char[] s = {'a', 'b', 'c'}; // s在堆中，但不在字符串常量池中
        String str3 = new String(s); //new出来的东西在堆中，即str3在堆中
        
        System.out.println(str1 == str2); // true，地址相同
        System.out.println(str1 == str3); // false，地址不同
        System.out.println(str2 == str3); // false，地址不同
    }
}
```

![image-20200708202433334](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200708202433334.png)

#### 字符串的比较与获取

- **字符串内容比较**：
  - 如果比较双方一个常量、一个变量，推荐**把常量字符串写在前面**。（因为`.`之前的对象不能为`null`，会报错`NullPointerException`）。即推荐：`"abc".equals(str)`，不推荐：`str.equals("abc")`。
  - `a.equals(b)`和`b.equals(a)`效果一样，为**不忽略大小写**的比较。
  - `a.equalsIgnoreCase(b)`为**忽略大小写**的比较。

```java
public class Demo01StringEquals {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        char[] charArray = {'H', 'e', 'l', 'l', 'o'};
        String str3 = new String(charArray);

        System.out.println(str1.equals(str2)); // true
        System.out.println(str2.equals(str3)); // true
        System.out.println("Hello".equals(str1)); // true

        String str5 = null;
        System.out.println("abc".equals(str5)); // 推荐：false
//        System.out.println(str5.equals("abc")); // 不推荐：报错，空指针异常NullPointerException

        String strA = "Java";
        String strB = "java";
        System.out.println(strA.equals(strB)); // false，严格区分大小写
        System.out.println(strA.equalsIgnoreCase(strB)); // true，忽略大小写
    }
}
```

- **字符串的获取**：
  - 获取字符串长度：`a.length()`。
  - 连接字符串：`a.concat(b)`，因为**字符串是不可变类型**，即不能被修改，故该操作是**新创建**了一个字符串。
  - 获取索引处的字符：`a.charAt(3)`。
  - 获取某一字符串第一次出现的索引：`a.IndexOf(str)`，没有该字符串`str`则返回`-1`。
  - `substring(int beginIndex) `，返回一个`[beginIndex, length-1]`的新字符串，它是此字符串的一个子字符串。
  - `substring(int beginIndex, int endIndex) `，返回一个`[beginIndex, endIndex)`的新字符串。
  - 字符串转字符数组：`str.toCharArray();`。
  - 数组转字符串：`Arrays.toString(arr)`。
  - 字符串替换：字符串`XY`替换为`*`：`conStr.replace("XY", "*")`。
  - 字符串切分：`str3.split(",");` ，按指定字符切分字符串。**特别注意**：如果按英文`"."`进行切分时，需要这样写`"\\."`（转义字符格式，原本的`"."`有别的含义）。

```java
public class Day01 {
    public static void main(String[] args) {
        String str = "helloWorld";
        System.out.println("长度：" + str.length());
        System.out.println("第5个位置的字符：" + str.charAt(5));
        int index = str.indexOf("oWo");
        System.out.println("字符串oWo第一次出现的位置：" + index);
        String conStr = "XYZ".concat(str); // XYZhelloWorld
        System.out.println("XYZ连接str后的字符：" + conStr);
        System.out.println("index后的字符串：" + conStr.substring(3));
        System.out.println("[begin, end)间的字符串:" + conStr.substring(3, 8));
        char[] chars = conStr.toCharArray(); // 字符串转字符数组
        System.out.println("数组转字符串：" + Arrays.toString(chars));
        System.out.println("指定的字符串替换：" + conStr.replace("XY", "*"));
        String str3 = "abc,def,ghi";
        String[] arr3 = str3.split(","); // 按指定字符切分字符串
        for (int i = 0; i < arr3.length; i++) {
            System.out.print(arr3[i] + "  ");
        }
    }
}
/*
长度：10
第5个位置的字符：W
字符串oWo第一次出现的位置：4
XYZ连接str后的字符：XYZhelloWorld
index后的字符串：helloWorld
[begin, end)间的字符串:hello
数组转字符串：[X, Y, Z, h, e, l, l, o, W, o, r, l, d]
指定的字符串替换：*ZhelloWorld
abc  def  ghi  
*/
```

#### 静态static关键字

- 静态`static`关键字修饰成员变量：如果一个成员变量使用了 `static `关键字，那么**这个变量不再属于new出来的对象，而是属于所在的类，所有对象共享此变量**。
- 静态`static` 修饰成员方法：一旦使用静态`static` 修饰成员方法，那么该方法就成为了静态方法，而静态方法不是属于new出来的对象，而是属于类的，即引用格式**变成 `类名称.成员方法()`**。
- 静态成员变量：`类名称.静态成员变量`、静态成员方法：`类名称.静态成员方法()`。
- 对于**本类当中**的静态成员方法**在本类中**调用，可以省略`类名称.`，即直接调用`静态成员方法`。
- 静态方法中不能直接访问当前类内的非静态成员变量、静态方法中不能使用`this`关键字。

```java
public class DemoClass {
    private String name;
    static int age;
    public DemoClass() {
    }
    public DemoClass(String name) { // 没有age
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public static int getAge() {
        return age;
    }
    public void setName(String name) {
        this.name = name;
    }
    public static void setAge(int age) {
        // 这里因为age被static修饰，成为类中被共享的成员变量，
        // 使用格式：类名称.static修饰的成员变量
        DemoClass.age = age;
        
        // age为static成员变量，正确写法
        System.out.println("静态方法调用静态成员变量：" + age);
        // + this.name or name 都是错误写法
		// System.out.println("静态方法调用非静态成员变量：" + this.name);
    }
}

public class Day01 {
    public static void main(String[] args) {
        DemoClass stu = new DemoClass("wzk");
        // 在DemoClass类中age被static修饰，
        // 所以age不再属于对象自己（stu），而是属于所在的类（DemoClass）
        // 使用类名称.静态成员方法调用
        DemoClass.age = 24;
        System.out.println("名字：" + stu.getName() + "年龄：" + stu.age);
        
        DemoClass stu2 = new DemoClass("kzw");
        // age属于所在的类（DemoClass），故stu2.age获取后即为类（DemoClass）内的值
        System.out.println("名字：" + stu2.getName() + "年龄：" + stu2.age);
        
        System.out.println("使用 类名称.成员方法 获取被static修饰的成员方法，推荐（防止误以为成员方法是普通的成员方法而不是静态成员方法）：" + DemoClass.getAge());
        
        System.out.println("当然也可以通过获取对象的成员方法那样获取static修饰的成员方法，但是不推荐：" + stu2.getAge());
    }
}
/*
名字：wzk年龄：24
名字：kzw年龄：24
使用 类名称.成员方法 获取被static修饰的成员方法，推荐（防止误以为成员方法是普通的成员方法而不是静态成员方法）：24
当然也可以通过获取对象的成员方法那样获取static修饰的成员方法，但是不推荐：24
*/
```

- 静态`static`成员变量与普通成员变量的内存图：**静态成员变量在方法区中的静态区**，而普通成员变量在堆内存中。

![image-20200710173353376](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200710173353376.png)

#### 静态代码块

- **静态代码块**：
  - 特点：当第一次用到本类时，静态代码块执行**唯一的一次**；
  - 因此，静态内容总是**优先于**非静态，所以**静态代码块比构造方法先执行**；
  - 静态代码块典型用途：用来一次性地对静态成员变量进行赋值。

```java
/*
【静态代码块格式】：
public class 类名称{
	static {
	int age = 10;
	String name = "iou";
	// ... 静态代码块内容
	}
}
*/

public class DemoClass {
    static { // 静态代码块
        System.out.println("当第一次用到本类时，静态代码块执行**唯一的一次**");
    }

    public DemoClass() {
        System.out.println("构造方法后执行");
    }
}

public class Day01 {
    public static void main(String[] args) {
        DemoClass stu1 = new DemoClass();
        DemoClass stu2 = new DemoClass(); // 第二次使用该类时，静态代码块不再执行
    }
}
/*
当第一次用到本类时，静态代码块执行**唯一的一次**
构造方法后执行
构造方法后执行
*/
```

#### 继承

- 继承的作用：当发生了类继承关系之后，子类可以直接继承父类的操作，可以实现代码的重用，子类最低也维持和父类相同的功能，子类也可以进行功能上的扩充。

![image-20200710181829545](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200710181829545.png)

- 继承关系父类构造方法的执行先于子类构造方法：对象在进行实例化前**首先调用父类构造方法，再调用子类构造方法**实例化子类对象。实际**在子类构造方法的第一条语句中，隐含了一个语句`super()`，调用父类的无参构造**，同时如果父类里没有提供无参构造，那么这个时候就必须使用`super(参数)`明确指明要调用的父类构造方法。
- 继承的格式：

```java
// 定义父类的格式：（一个普通的类定义）
public class 父类名称 {
    // ...
}

// 【定义子类的格式】：
public class 子类名称 extends 父类名称 {
    // ...
}
```

- Java 中只允许单继承不允许多继承（即一个子类仅继承一个父类），但允许多级继承（即A继承B，B继承C）。
- 在进行继承的时候，子类会继承父类的**所有结构**（包括私有属性、构造方法、普通方法）。
  - **显示继承**：所有【非私有操作】属于显示继承（可以直接调用）。
  - **隐式继承**：所有【私有操作】属于隐式继承（不可以直接调用，需要通过其它形式调用（`getter`或者`setter`方法））。

```java
/*
在继承的关系中，“子类就是一个父类”。也就是说，子类可以被当做父类看待。
例如父类是员工，子类是讲师，那么“讲师就是一个员工”。关系：is-a。
*/

public class DemoExtends {
    int num = 10;
    int numExtends = 50;
    public void fatherMethod(){
        System.out.println("执行父类的方法：" + num);
    }
}

public class DemoChildren extends DemoExtends {
    int num = 20;

    public void chilMethod() {
        System.out.println("子类特有的方法：" + num);
    }
}

public class Day01 {
    public static void main(String[] args) {
        DemoChildren chi = new DemoChildren();
        chi.fatherMethod(); // 通过子类执行父类的方法
        chi.chilMethod();   // 子类执行自己特有的方法
        
        // 子类调用成员变量num，子类chi有该成员变量，调用自己类中的该成员变量即可，
        // 即【就近原则（如果没有才调用父类的num）】
        System.out.println(chi.num);
        // 子类调用成员变量numExtends，调用父类的成员变量（因为子类没有该变量）
        System.out.println(chi.numExtends);
        
        // 通过子类调用自己特有的方法，成员变量num使用子类的成员变量即可（就近原则）
        chi.chilMethod();
        //通过子类执行父类的方法，成员变量num需要使用父类的
        chi.fatherMethod();
    }
}
/*
执行父类的方法：10
子类特有的方法：20
20
50
子类特有的方法：20
执行父类的方法：10
*/
```

#### super关键字

- `super`关键字：
  - 可以在子类中访问父类的成员变量，格式：`super.父类成员变量`。
  - 可以在子类中访问父类的成员方法，格式：`super.父类成员方法`。
  - **子类构造方法中必须访问父类构造方法（有参构造 / 无参构造都可）**，格式：子类构造方法的第一条语句`super(...)`。

#### this关键字

- `this`关键字：
  - 可以在**本类**中访问**本类**的成员变量，格式：`this.本类成员变量`。
  - 可以在**本类**中访问**本类**的成员方法，格式：`this.本类成员方法`。
  - 可以在**本类**的某一个构造方法中访问**本类**的另一个构造方法，格式：`this(某一个构造方法的参数)`
  - `super(某一个构造方法的参数)`和`this(某一个构造方法的参数)`都要求是构造方法的**第一条语句**，所以两者**不能共存**。

#### 覆盖重写@Override

- **覆盖重写**：在继承关系中，子类和父类的成员方法相同（即方法名称相同 + 参数列表相同）。这样在子类中的方法会覆盖父类中的方法。检测子类中方法是不是有效地覆盖重写，是在方法前一行加一句`@Override`（如果你确定是覆盖重写了，也可以不加 `@Override`）检查是否报错。
- 子类方法的返回类型必须【小于等于】父类方法的返回类型范围。
- 子类方法的权限修饰符必须【大于等于】父类方法的权限修饰符。
  - 小扩展提示：`public > protected > (default) > private`

```java
/*
方法覆盖重写的注意事项：

1. 必须保证父、子类之间方法的名称相同，参数列表也相同。
@Override：写在方法前面，用来检测是不是有效的正确覆盖重写。
这个注解就算不写，只要满足要求，也是正确的方法覆盖重写。

2. 子类方法的返回类型必须【小于等于】父类方法的返回类型范围。例如：子类String <= Object
小扩展提示：java.lang.Object类是所有类的公共最高父类（祖宗类），java.lang.String就是Object的子类。

3. 子类方法的权限必须【大于等于】父类方法的权限修饰符。
小扩展提示：public > protected > (default) > private
备注：(default)不是关键字default，而是什么都不写，留空。
 */
```

- **为什么要进行覆盖重写？**开发了新手机，新手机相比旧手机增加了一些功能。那么就可以进行覆盖重写对应的部分以增加功能。

![image-20200713170012321](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200713170012321.png)

```java
/*
对于上图中，来电显示部分增加了新功能，但是旧手机的显示号码功能依然保留
*/

public class NewPhone extends Phone { // 定义一个新手机，使用老手机作为父类

    @Override
    public void show() {
        // 把父类的show方法拿过来重复利用（旧手机的显示号码功能依然保留，super直接拿来）
        super.show();
        // 子类 来电显示部分 增加的新功能
        System.out.println("显示姓名");
        System.out.println("显示头像");
    }
}
```

#### 继承中的构造方法

- **继承中构造方法的访问特点**：
  - 子类**必须**调用父类**构造方法**，不写则**赠送**`super()`，也表明创建子类对象时，**先执行父类的构造方法，后执行子类的构造方法**；
  - `super()`写了则用写的指定的`super()`调用；
  - `super()`只能有一个，还必须为子类构造方法的第一句。
  - `super(参数)`可以是无参构造方法也可以是有参构造方法。

```java
public class DemoExtends { // 父类
    public DemoExtends() {
        System.out.println("父类无参构造方法");
    }
}

public class DemoChildren extends DemoExtends { // 子类
    public DemoChildren() {
        // super(); // 子类必须调用父类构造方法，不写则赠送super()
        System.out.println("子类无参构造方法");
        // super(); // 错误，super()必须为子类构造方法的 第一句
    }
}

public class Day01 {
    public static void main(String[] args) {
        DemoChildren chi = new DemoChildren(); // 先执行父类构造方法然后执行子类构造方法
    }
}
/*
父类无参构造方法
子类无参构造方法
*/
```

#### super与this关键字在继承关系中的使用

-  **`super`与`this`关键字在继承关系中的图解**：`this`指示本类地址，`super`指示父类地址，后面均可接成员变量 / 成员方法。

![image-20200713224754808](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200713224754808.png)

- **继承的三大特性**：单继承、多级继承、共同继承。

![image-20200713225751575](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200713225751575.png)

#### 抽象abstract

- **抽象**：
  - 抽象方法：就是加上`abstract`关键字，然后去掉大括号，直接分号结束。格式：`权限修饰符 abstract 返回类型 方法名();`。
  - **抽象类**：存在抽象方法的类，必须是抽象类。在`class`之前写上`abstract`即为抽象类。
  - 一个抽象类不一定含有抽象方法，但含有抽象方法的类一定是抽象类。
  - **如何使用抽象类和抽象方法**：
    1. 不能直接创建`new`抽象类对象。
    2. **必须用一个子类来继承抽象父类**。
    3. 子类**必须覆盖重写**抽象父类当中**所有的**抽象方法。覆盖重写（实现）：子类去掉抽象方法的`abstract`关键字（可以前面一行加上`@Override`检查是否是覆盖重写），补上方法体大括号，然后代码体内写要实现的内容。**注意**：如果子类**并没有完全覆盖重写**父类的**所有的**抽象方法，那么子类也必须加上 `abstract`变为抽象类。
    4. 【创建子类对象】，对【子类中覆盖重写的抽象方法】进行使用即可。
  - `new`完子类对象之后，会**执行父类的构造方法**和子类的构造方法（因为子类的构造方法是必须要先执行一个`super(参数)`的，即父类构造方法）。

```java
public abstract class Animal { // abstract 即抽象类
    
    public abstract void eat(); // 这是一个抽象方法

    public void normalMethod() { // 这是普通的成员方法
	// ...
    }
}
```

#### 接口interface

- 接口格式：`权限修饰符 interface 接口名称{ // 方法体 }`。
- 接口中可以包含的内容仅限于以下几类（Java 9版本）：
  - 常量、（`final`修饰，不可改变）
  - 抽象方法（抽象方法没有方法体，实现类需要进行覆盖重写）、
  - 默认方法（默认方法：实现类不必覆盖重写即可访问的方法）、
  - 静态方法（实现类中使用类名称直接访问）、
  - 私有方法（普通私有方法、静态私有方法）。
- 接口使用步骤：接口不能直接`new`进行使用，必须有一个「实现类」来「实现」该接口。
  - 实现类格式：`public class 实现类名称 implements 接口名称 {// ...}`。
  - 接口的实现类必须覆盖重写（实现）接口中**所有的**抽象方法。
  - **注意**：如果实现类**并没有**覆盖重写接口中所有的抽象方法，那么这个实现类自己就**必须是抽象类**。
- 接口的**常量**格式：`public static final 数据类型 常量名 = 赋值;`。常量名推荐**全大写、单词之间用下划线分隔**。
- 接口的**抽象方法**格式：`public abstract 返回类型 方法名称();`。
- 接口的**默认方法**格式：`public default 返回类型 方法名称(){ // 方法体 }`。
  - 由于接口中可能会增加新的“标准”，如果增加抽象方法，那么所有的实现类都必须再覆盖重写**补充的**新增抽象方法的，很麻烦。故**新增的方法可以使用默认方法，实现类不必覆盖重写即可访问该默认方法**。
- 接口的**静态方法**格式：`public static 返回类型 方法名称(){ // 方法体 }`。
  - 静态方法与`new`对象没关系，只跟类有关系，即**直接使用类访问静态方法 / 静态变量**，格式：`类.静态方法(参数列表);`，故**在实现类中调用接口中的静态方法使用`接口类.静态方法(参数);`**为正确访问手法。
- 接口的**普通私有方法**格式：`private 返回类型 方法名称(){ // 方法体 }`。
  - 用途：解决**多个默认`default`方法**之间的重复代码问题。
- 接口的**静态私有方法**格式：`private static 返回类型 方法名称(){ // 方法体 }`。
  - 用途：解决**多个静态`static`方法**之间的重复代码问题。

```java
public interface DemoInterface {
	
    public static final double PI = 3.141592654; // 常量（成员变量），不可被修改
    
    // 以下四个都是抽象方法，
    // 在接口中，抽象类可以省略public 或者 abstract 或者两个都省略
    public abstract void method1();
    public void method2();
    abstract void method3();
    void method4();

    // 接口的默认方法
    public default void methodDef() {
        System.out.println("接口的默认方法可以有方法体");
    }

    public static void methodSta() {
        System.out.println("接口的静态方法，可以直接使用类访问静态方法");
        DemoInterface.methodSta(); // 直接使用类访问静态方法
    }

    private void methodPri1() {
        System.out.println("普通私有方法，用于解决多个默认`default`方法之间的重复代码问题。");
    }

    private static void methodPriSta2() {
        System.out.println("静态私有方法，用于解决多个静态`static`方法之间的重复代码问题。");
    }
}
```

- **继承父类并实现多个接口**：
  - 「实现类`MyInterfaceImpl`」继承多个接口的格式：`public class MyInterfaceImpl implements MyInterfaceA, MyInterfaceB { // 覆盖重写所有抽象方法 }`
  - 「子类`Zi`」继承「父类`Fu`」并实现多个接口的格式：`public class Zi extends Fu implements MyInterfaceA, MyInterfaceB { // 覆盖重写所有抽象方法 }`

```java
/*
使用接口的时候，需要注意：

1. 接口是【没有静态代码块或者构造方法】的。
2. 一个类的直接父类是唯一的，但是一个类可以同时实现多个接口。
格式：
public class MyInterfaceImpl implements MyInterfaceA, MyInterfaceB {
    // 覆盖重写所有抽象方法
}
3. 如果实现类所实现的多个接口当中，「存在重复的抽象方法，那么只需要覆盖重写一次即可」。
4. 如果实现类没有覆盖重写所有接口当中的所有抽象方法，那么「实现类就必须是一个抽象类」。
5. 如果实现类所实现的多个接口当中，存在「重复的默认方法」，那么【实现类一定要对冲突的默认方法进行覆盖重写】。
6. 一个类中，如果「直接父类当中的方法」和「接口当中的默认方法」产生了冲突，【优先用父类】当中的方法。
 */
```

- 接口之间的**多继承**：

```java
/*
1. 【类与类之间是单继承的】，直接父类只有一个。
2. 【类与接口之间是多实现的】，【一个类可以实现多个接口】。
3. 【接口与接口之间是多继承的】。

注意事项：
1. 多个父接口当中的抽象方法如果重复，没关系。
2. 多个父接口当中的「默认方法」如果重复，那么【子接口必须进行默认方法的覆盖重写】，【覆盖重写方法要保留着default关键字】。
 */
```

#### 多态

- **多态的使用**：
  - 格式：`父类名称 对象名 = new 子类名称();`或者`接口名称 对象名 = new 实现类名称();`。
  - 访问**成员变量**的两种方式：

    1. **直接通过对象名称**访问成员变量：【看创建该对象时，等号左边是谁，优先用谁，没有则向上找】。
    2. **间接通过成员方法**访问成员变量：【看该方法属于谁，优先用谁，没有则向上找】。
  - 访问**成员方法**的方式：
    1. 看`new`的后边是「谁」，就优先用「这个谁」的成员方法，没有则向上找。
  - 口诀：成员变量：编译看左边（的引用），运行还看左边（的引用）。    成员方法：编译看左边（的引用），运行看右边（的`new`对象）。

```java
/*
代码当中体现多态性，其实就是一句话：父类引用指向子类对象。
 */

// 口诀的代码层面理解
public class DemoExtends {
    int num = 10;

    public void methodFather() {
        System.out.println("父类方法执行");
    }
}

public class DemoChildren extends DemoExtends {
    int num = 20;

    public void methodChi() {
        System.out.println("子类方法执行");
    }
}

public class Day01 {
    public static void main(String[] args) {
        DemoExtends fat = new DemoChildren();
        System.out.println("成员变量编译看左（父类），执行看左（父类num）：" + fat.num); // 10
        
        // 编译看fat左边的引用，即DemoExtends父类，父类没有methodChi()方法，故编译就出错
        // Cannot resolve method 'methodChi' in 'DemoExtends'
//        fat.methodChi(); // 编译错误
        
        // 如果在多态中，我想用子类特有的方法methodChi()，该怎么办？
        DemoChildren chi = (DemoChildren) fat; // 「向下转型」，这样才能用子类特有的成员方法
        chi.methodChi(); // 输出：子类方法执行

        // 成员方法：编译看左，左边父类有methodFather()成员方法，编译通过；
        // 执行看右，即执行右边子类的方法methodFather()（子类没有，向上找）
        fat.methodFather(); //输出：父类方法执行
    }
}
```

- **为什么使用多态？**：无论右边`new`的时候换成哪个子类对象，等号左边调用方法都不会变化（即`Employee`不用随着右边`new`的变化而变化，``one.work(); //讲课`和`two.work(); //辅导`的成员方法也不用变（因为你新`new`的子类对象一定要有 `work();`成员方法） ）。

![image-20200714173131252](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200714173131252.png)

#### 对象的向上转型与向下转型

- **对象的向上转型与向下转型**：
  - 向上转型：其实就是多态写法。格式：`父类名称 对象名 = new 子类名称();`
  - 向下转型：其实是一个「还原」的动作（向下转型的前提是可以还原）。格式：`子类名称 对象名 = (子类名称) 父类对象`。
  - 如何才能知道一个**父类引用的对象**本来是什么类？
    - 使用`instanceof`进行判断：格式：`对象名 instanceof 类名称`，返回`true`表示该对象即为该类。
  - 注意：向下转型一定要进行`instanceof`判断。

![image-20200714185247462](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200714185247462.png)

#### final关键字

- `final`关键字：表示最终的、不可变的；

- `final`关键字可以用来修饰：一个类、一个成员方法、一个局部变量、一个成员变量。

- `final`关键字修饰一个类：

  - 格式：`修饰符 final class 类名称 { // 方法体}`；
  - 注意：`final`修饰的类只能有父类、**不能有子类**，所以【其所有成员方法都不能被覆盖重写】。

- `final`关键字修饰一个成员方法：

  - 格式：`修饰符 final 返回类型 方法名称 { // 方法体}`；
  - 注意：`final`修饰成员方法时【其子类不能对这个方法进行覆盖重写】。

- `final`关键字修饰一个方法中的局部变量：

  - 格式：`final 引用类型 / 基本类型 对象名 = new 对象 / 赋值语句`；
  - 如果`final`修饰的是基本类型，那么**其值**永远不可能再被修改；
  - 如果`final`修饰的是引用类型，那么**其地址**永远不可能再被修改，【但是**其地址内对应的值**却可以随便被修改】。

- `final`关键字修饰一个成员变量：

  - 由于成员变量具有默认值，所以用了`final`之后【必须手动赋值，不会再给默认值了】。
  - 对于`final`关键字修饰的成员变量，**要么使用直接赋值，要么通过构造方法赋值**（二者选其一）。
    - 可以【通过等号进行直接赋值】（这时要注意不能再使用`setter()`方法）。
    - 【通过构造方法进行赋值】，必须保证类当中**所有重载的构造方法**，都最终会对`final`的成员变量进行赋值（这时要注意不能再使用`setter()`方法了）。

  ```java
  public class Person {
      private final String name/* = "鹿晗"*/; // 通过等号进行直接赋值
  
      public Person() { // 通过构造方法进行赋值
          name = "关晓彤";
      }
      public Person(String name) { // 通过构造方法进行赋值
          this.name = name;
      }
  
      public String getName() {
          return name;
      }
  
  //    public void setName(String name) { // 这时要注意不能再使用setter()方法了
  //        this.name = name;
  //    }
  }
  ```


#### 四种权限修饰符

- **四种权限修饰符**：`public  >   protected   >   (default)   >   private`

```java
/*
Java中有四种权限修饰符：
                    public  >   protected   >   (default)   >   private
同一个类（我自己）        YES         YES             YES             YES
同一个包（我邻居）        YES         YES             YES             NO
不同包子类（我儿子）       YES         YES             NO              NO
不同包非子类（陌生人）     YES         NO              NO              NO
*/
```

#### 内部类

- 内部类包括：成员内部类（与成员变量处于同一层级）、局部内部类（定义在成员方法内部）。
- 成员内部类的定义格式：

```java
// 注意：内用外，随意访问；外用内，需要内部类对象。
修饰符 class 外部类名称 {
    修饰符 class 内部类名称 {
        // ...
    }
    // ...
}
```

- **成员内部类的使用**：
  - 间接方式：在外部类的成员方法当中使用内部类，然后main方法只调用外部类的成员方法。
  - 【直接方式】：公式：`外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称();`，则可以在外部类以外访问内部类。

```java
/*
如果一个事物的内部包含另一个事物，那么这就是一个类内部包含另一个类。
例如：身体和心脏的关系。又如：汽车和发动机的关系。

分类：
1. 成员内部类
2. 局部内部类（包含匿名内部类）

*/
public class Body { // 外部类

    public class Heart { // 成员内部类
        // 内部类的方法
        public void beat() {
            System.out.println("心脏跳动：蹦蹦蹦！");
            System.out.println("我叫：" + name); // 内用外，随意访问. 正确写法！
        }
    }
    
    // 外部类的成员变量
    private String name;
    // 外部类的方法
    public void methodBody() {
        System.out.println("外部类的方法");
        new Heart().beat(); // 【内部类匿名对象，访问内部类的方法】
    }
}

public class Demo01InnerClass {
    public static void main(String[] args) {
        Body body = new Body(); // 外部类的对象
        // 通过外部类的对象body，调用外部类的方法methodBody()，方法里面间接在使用内部类Heart
        body.methodBody();
        System.out.println("=====================");

        Body.Heart heart = new Body().new Heart(); // 直接方式
        heart.beat();
    }
}
```

- **内部类的（与外部类）同名变量的访问**：访问外部类成员变量：【`外部类名称.this.外部类成员变量名`】。

```java
// 如果出现了重名现象，那么格式是：外部类名称.this.外部类成员变量名
public class Outer {
    int num = 10; // 外部类的成员变量

    public class Inner /*extends Object*/ {
        int num = 20; // 内部类的成员变量

        public void methodInner() {
            int num = 30; // 内部类方法的局部变量
            System.out.println(num); // 局部变量，就近原则 30
            System.out.println(this.num); // 内部类的成员变量 20
            System.out.println(Outer.this.num); // 外部类的成员变量 10
        }
    }
}
```

- **局部内部类**：如果一个类是【定义在一个方法内部的】，那么这就是一个局部内部类。
- **局部内部类格式**：

```java
修饰符 class 外部「类」名称 {
    修饰符 返回值类型 外部类「方法」名称(参数列表) {
        class 局部内部类名称 {
            // ...
        }
        // ...
    }
}
```

- **局部内部类使用**：

```java
/*
“局部”：【只有当前所属的方法才能使用它】，出了这个方法外面就不能用了。

============================
小节一下类的权限修饰符：
public > protected > (default) > private
定义一个类的时候，「权限修饰符」可使用范围规则：
1. 外部类：public / (default)
2. 成员内部类：public / protected / (default) / private
3. 局部内部类：什么都不能写!
 */

class Outer { //外部类

    public void methodOuter() { // 成员方法
        class Inner { // 【局部内部类，不能有修饰符】
            int num = 10;
            public void methodInner() {
                System.out.println(num); // 10
            }
        }

        Inner inner = new Inner();
        inner.methodInner(); // 【只有当前所属的方法才能使用它】，出了这个方法外面就不能用了
    }

}
```

- **匿名内部类**：如果接口的实现类（或者是父类的子类）【只需要使用唯一的一次】，那么这种情况下就可以省略掉该类的定义，而改为使用【匿名内部类】。

```java
/*
匿名内部类的定义格式：
接口名称 对象名 = new 接口名称() {
    // 覆盖重写所有抽象方法
};

对格式“new 接口名称() {...}”进行解析：
1. new代表创建对象的动作
2. 接口名称就是匿名内部类需要实现哪个接口
3. {...}这才是匿名内部类的内容

另外还要注意几点问题：
1. 匿名内部类，在【创建对象】的时候，【只能使用唯一一次】。
如果希望多次创建对象，而且类的内容一样的话，那么就需要使用单独定义的实现类了。
2. 匿名对象，在【调用方法】的时候，【只能调用唯一一次】。
如果希望同一个对象，调用多次方法，那么必须给对象起个名字，使用非匿名对象。
3. 【匿名内部类】是省略了【实现类/子类名称】，但【还是有对象名称的】；但是匿名对象是省略了【对象名称】

强调：匿名内部类和匿名对象不是一回事！！！
 */
public class DemoMain {

    public static void main(String[] args) {

        // 使用匿名内部类，对象名称就叫objA。不是匿名对象！
        MyInterface objA = new MyInterface() {
            @Override
            public void method1() {
                System.out.println("匿名内部类实现了方法！111-A");
            }
        };
        
        objA.method1();
        System.out.println("=================");

        // 使用了匿名内部类，而且省略了对象名称，【是匿名内部类，也是匿名对象】
        new MyInterface() {
            @Override
            public void method1() {
                System.out.println("匿名内部类实现了方法！111-B");
            }
        }.method1(); // 如果希望再次调用成员方法，只能再创建一个匿名对象后访问
        
        // 因为匿名对象无法调用第二次方法，所以需要再创建一个匿名内部类的匿名对象
        new MyInterface() {
            @Override
            public void method1() {
                System.out.println("匿名内部类实现了方法！111-B");
            }
        }.method1();
    }
}
```

- 类作为成员变量的类型是可以的、同样接口作为成员变量的类型也是可以的。
- 接口作为方法的参数类型和返回值类型都是可以的。

#### Object类的equals方法

- 对于String字符串比较的方法 `a.equals(b)`，`a`不能为`null`，但是Object类的`equals(a, b)`方法`a, b`都可以为`null`。**Object类的equals方法源码如下**：

```java
public static boolean equals(Object a, Object b) {
    	// 首先判断地址值是否相同，地址相同字符串内容肯定相等；a b都为null时地址相同返回true
    	// 地址不同时比较内容
        return a == b || a != null && a.equals(b);
}
```

### 集合

#### 集合Collection

- **Collection**：Collection是所有单列集合的父接口，用于存储一系列符合某种规则的元素，它有两个重要的子接口，分别是`java.util.List`和`java.util.Set`。其中，`List`的特点是元素有序、元素可重复。`Set`的特点是元素无序，而且不可重复。`List`接口的主要实现类有`java.util.ArrayList`和`java.util.LinkedList`，`Set`接口的主要实现类有`java.util.HashSet`和`java.util.TreeSet`。

```java
public static void main(String[] args) {
    // 创建集合对象，使用多态形式，    多态：接口名称 对象名 = new 实现类名称();
    Collection<String> coll = new ArrayList<String>();
    coll.add("2020/7/20");
    coll.add("23:36");
    coll.contains("123");
    coll.size();
    coll.isEmpty();
    coll.remove('23：36');
    coll.toArray();
    coll.clear();
}
```

![image-20200720192650983](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200720192650983.png)

#### Iterator迭代

- 在程序开发中，经常需要遍历集合中的所有元素。`Iterator`接口也是Java集合中的一员，但它与`Collection`、`Map`接口有所不同，**`Collection`接口与`Map`接口主要用于存储元素，而`Iterator`主要用于迭代访问（即遍历）`Collection`中的元素，因此`Iterator`对象也被称为迭代器**。

```java
/*
 * 创建集合对象：Collection<String> coll = new ArrayList<String>();
 * 创建迭代器：coll.iterator()
 * 判断迭代器是否还有对象：iter.hasNext()
 * 获取下一个对象：iter.next()
 */

public static void main(String[] args) {
    // 创建集合对象，使用多态形式
    Collection<String> coll = new ArrayList<String>();
    coll.add("2020/7/20");
    coll.add("23:36");
    // 使用迭代器遍历 
    Iterator<String> iter = coll.iterator();
    while (iter.hasNext()) {
        System.out.println(iter.next());
    }
}
```

- **Iterator原理**：Iterator迭代器对象在遍历集合时，内部采用指针的方式来跟踪集合中的元素。在调用Iterator的next方法之前，**迭代器的索引位于第一个元素之前，不指向任何元素**，当第一次调用迭代器的next方法后，迭代器的索引会向后移动一位，指向第一个元素并将该元素返回，当再次调用next方法时，迭代器的索引会指向第二个元素并将该元素返回，依此类推，直到hasNext方法返回false，表示到达了集合的末尾，终止对元素的遍历。

![image-20200720231257425](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200720231257425.png)

#### 增强for循环

- 增强for循环(也称for each循环)是**JDK1.5**以后出来的一个高级for循环，**专门用来遍历数组和集合的**。它的**内部原理其实是个Iterator迭代器**，所以在遍历的过程中，**不能对集合中的元素进行增删操作**。

```java
public static void main(String[] args) {

    ArrayList<Integer> nums = new ArrayList<>();
    for (int i = 0; i < 5; i++) { // 普通for循环
        nums.add(i);
    }
    for (int ele : nums) { // 增强for循环，底层使用迭代器实现
        System.out.println(ele);
    }
}
```

#### 泛型

- **泛型**：可以在类或方法中预支地使用未知的类型。一般在new创建对象时，将未知的类型（泛型）指定到具体的数据类型。当没有指定泛型时，默认类型为Object类型。

```
Collection arr = new ArrayList(); // 不指定泛型
Collection<String> arr = new ArrayList<String>(); // 指定泛型为String类型
```

- 我们在集合中会大量使用到泛型。泛型，用来灵活地将数据类型应用到不同的类、方法、接口当中。将数据类型作为参数进行传递。
- **定义含有泛型的类**：格式：`修饰符 class 类名<代表泛型的变量> { // 方法体 }`，例如：`class ArrayList<E> { // 方法体 }`
  - **使用含有泛型的类**：在创建对象的时候确定泛型具体使用什么数据类型，例如：`ArrayList<String> list = new ArrayList<String>();`，此时，变量`E`的值就是`String`类型。
- **定义含有泛型的方法**：格式：`修饰符 <代表泛型的变量> 返回值类型 方法名(参数){ // 方法体  }`，例如：`public <E> E method1(E e) { // 方法体 }`
  - **使用含有泛型的方法**：调用方法时，确定泛型的类型。
- **定义含有泛型的接口**：格式：`修饰符 interface 接口名 <代表泛型的变量> {  }`
  - **使用含有泛型的接口**：
    - 定义实现类时指定泛型的类型，例如： `public class DemoInterfaceImpl implements DemoInterface<String>`，即在实现类中接口的泛型为`String`数据类型。
    - 始终不确定泛型的类型，不再实现类中指定泛型的类型，直到创建对象时才确定泛型的类型。

```java
public class DemoClass<E> { // 定义含有泛型的类
    public E age;

    public <E> E method1(E e) { // 定义含有泛型的方法
        return e;
    }
}

public interface DemoInterface<E> { // 定义含有泛型的接口
    public abstract <E> E method1(E e); // 抽象方法
}

// 在定义实现类时就确定接口的泛型（为String）
public class DemoInterfaceImpl implements DemoInterface<String> {

    @Override
    public <String> String method1(String s) { // 抽象方法覆盖重写
        return s;
    }
}

// 始终不确定泛型的类型，不再实现类中指定泛型的类型，直到创建对象时才确定泛型的类型
public class DemoInterfaceImpl2<E> implements DemoInterface<E> {

    @Override
    public <E> E method1(E s) {
        return s;
    }
}

public class Day01 {
    public static void main(String[] args) {
        DemoClass obj = new DemoClass(); // 没有指定泛型，则为Object类
        obj.age = "wzk";
        System.out.println(obj.age);
        Object s = obj.method1("没有指定泛型，则为Object类");
        System.out.println(s);

        DemoClass<Integer> num = new DemoClass<>(); // 指定泛型为整型数据类型
        obj.age = 20;
        System.out.println(num.age);
        int a = num.method1(666);
        System.out.println(a);
        
 		// 创建接口的实现类对象,已在实现类中指定了接口的泛型为String
        DemoInterfaceImpl impl = new DemoInterfaceImpl();
        String s1 = impl.method1("abc");
        System.out.println(s1);
        
        // 创建接口的实现类对象，并在此时指定实现类和接口的泛型为Integer
        DemoInterfaceImpl2<Integer> impl2 = new DemoInterfaceImpl2<>();
        int s2 = impl2.method1(999);
        System.out.println(s2);

    }
}
```

#### 受限泛型

- 受限泛型：泛型中可以指定一个泛型的**上限**和**下限**。

- **泛型的上限**：
  - **格式**： `类型名称 <? extends 类 > 对象名称`
  - **意义**： `只能接收该类型及其子类`

- **泛型的下限**：
  - **格式**： `类型名称 <? super 类 > 对象名称`
  - **意义**： `只能接收该类型及其父类型`
- 类的范围 / 类与类之间的继承关系：`Integer extends Number extends Object`、`String extends Object`。

```java
// 泛型的上限：此时的泛型?，必须是Number类型或者Number类型的子类
public static void getElement1(Collection<? extends Number> coll){}
// 泛型的下限：此时的泛型?，必须是Number类型或者Number类型的父类
public static void getElement2(Collection<? super Number> coll){}
```

#### List集合

- List作为Collection集合的子接口，不但继承了Collection接口中的全部方法，而且还增加了一些根据元素索引来操作集合的特有方法。

- `List`类是一个接口，其所有超级接口有： `Collection`、`Iterable`，所有已知实现类：`AbstractList, AbstractSequentialList, ArrayList, AttributeList, CopyOnWriteArrayList, LinkedList, RoleList, RoleUnresolvedList, Stack, Vector `。

#### ArrayList集合

- `java.util.ArrayList`集合数据存储的结构是数组结构。**元素增删慢，查找快**，由于日常开发中使用最多的功能为查询数据、遍历数据，所以`ArrayList`是最常用的集合。

```java
public static void main(String[] args) {
    List<String> list = new ArrayList<>();
    list.add("a");
    list.add("b");
    list.get(1);
    list.size();
    list.set(1, "bb");
    list.remove(0);
    Iterator<String> iter = list.iterator();
    for (String s : list) {
        System.out.println(list); // [bb]
        System.out.println(s);
    }
```

#### LinkedList集合

`java.util.LinkedList`集合数据存储的结构是链表结构。**方便元素添加、删除的集合**。LinkedList是List的子类，List中的方法LinkedList都是可以使用

- `public void addFirst(E e)`:将指定元素插入此列表的开头。
- `public void addLast(E e)`:将指定元素添加到此列表的结尾。
- `public E getFirst()`:返回此列表的第一个元素。
- `public E getLast()`:返回此列表的最后一个元素。
- `public E removeFirst()`:移除并返回此列表的第一个元素。
- `public E removeLast()`:移除并返回此列表的最后一个元素。
- `public E pop()`:从此列表所表示的堆栈处弹出一个元素。换句话说，移除并返回此列表的第一个元素。 
- `public void push(E e)`:将元素推入此列表所表示的堆栈。换句话说，将该元素插入此列表的开头。 
- `public boolean isEmpty()`：如果列表不包含元素，则返回true。

#### Set集合

`public interface Set extends Collection`，Set集合为一个不包含重复元素的 collection。

`java.util.Set`接口和`java.util.List`接口一样，同样继承自`Collection`接口，它与`Collection`接口中的方法基本一致，并没有对`Collection`接口进行功能上的扩充，只是比`Collection`接口更加严格了。与`List`接口不同的是，**`Set`接口中元素无序，并且都会以某种规则保证存入的元素不出现重复**。

- Set集合取出元素的方式可以采用：迭代器、增强for循环。

```java
public static void main(String[] args) {
    Set<Integer> set = new HashSet<>();
    set.add(54);
    set.add(65);
    for (int num : set) { // 增强for
        System.out.println(num);
    }
    Iterator<Integer> iter = set.iterator();
    while (iter.hasNext()) { //迭代器遍历
        System.out.println(iter.next());
    }
}
```

#### HashSet集合

什么是哈希表呢？

在**JDK1.8**之前，哈希表底层采用数组+链表实现，即使用链表处理冲突，同一hash值的链表都存储在一个链表里。但是当位于一个桶中的元素较多，即hash值相等的元素较多时，通过key值依次查找的效率较低。而JDK1.8中，**哈希表存储采用数组+链表+红黑树实现，当链表长度超过阈值（8）时，将链表转换为红黑树，这样大大减少了查找时间**。

- **HashSet存储自定义类型元素**：在HashSet中存放自定义类型元素时，**需要重写对象中的hashCode和equals方法**，建立自己的比较方式，才能保证HashSet集合中的对象唯一。

```java
import java.util.Objects;

public class DemoClass {
    private String name;
    public int age;

    public DemoClass() {
    }

    public DemoClass(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "DemoClass{" + "name='" + name + '\'' + ", age=" + age + '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        DemoClass demoClass = (DemoClass) o;
        return age == demoClass.age &&
                Objects.equals(name, demoClass.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}

public class Day01 {
    public static void main(String[] args) {
        HashSet<DemoClass> set = new HashSet<>();
        DemoClass d1 = new DemoClass("ABC", 18);
        DemoClass d2 = new DemoClass("ABC", 19);
        DemoClass d3 = new DemoClass("ABC", 18);
        set.add(d1);
        set.add(d2);
        set.add(d3);
        
        // 覆盖重写hashSet()和a.equals(b)方法后（前）
        System.out.println(d1.hashCode() == d2.hashCode()); // false (false)
        System.out.println(d1.hashCode() == d3.hashCode()); // true (false)
        System.out.println(d1.equals(d2)); // false (false)
        System.out.println(d1.equals(d3)); // true (false)
        
        System.out.println(set); // [DemoClass{name='ABC', age=19}, DemoClass{name='ABC', age=18}] (覆盖重写前包括三个对象)
        for (DemoClass d : set) {
            System.out.println(d); // DemoClass{name='ABC', age=19}  DemoClass{name='ABC', age=18}
        }
        
    }
}
```

#### LinkedHashSet集合

`public class LinkedHashSet extends HashSet`。HashSet下面有一个子类`java.util.LinkedHashSet`，它是链表和哈希表组合的一个数据存储结构，可以保证存储的数据在输出时**有序**（与HashSet一样，数据具有唯一性，即不可重复）。

#### 可变参数

如果我们定义一个方法需要接受多个参数（接收的个数不固定），并且多个参数类型一致，我们可以对其简化成如下格式：

```
修饰符 返回值类型 方法名(参数类型... 形参名){  }
```

其实这个书写完全等价于：

```
修饰符 返回值类型 方法名(参数类型[] 形参名){  }
```

只是后面这种定义，在调用时必须传递数组，而前者可以直接传递数据即可。

- 注意：如果在方法书写时，这个方法拥有多参数，参数中包含可变参数，**可变参数一定要写在参数列表的末尾位置**。

#### Collections集合和Comparator接口

`java.utils.Collections`是集合工具类，用来对集合进行操作。部分方法如下：

`public static <T> boolean addAll(Collection<T> c, T... elements)  `:往集合中添加一些元素。

`public static void shuffle(List<?> list) 打乱顺序`:打乱集合顺序。

`public static <T> void sort(List<T> list)`:将集合中元素按照默认规则排序。

`public static <T> void sort(List<T> list，Comparator<? super T> )`:将集合中元素按照指定规则排序。

- **Comparator比较器**：对于`public static <T> void sort(List<T> list，Comparator<? super T> )`:将集合中元素按照指定规则排序。对于待排序的类型需要实现Comparable接口完成比较的功能。所以，如果我们要按升序排序`list`集合，我们就必须覆盖重写`Comparator<? super T>`

```java
public class Day01 {
    public static void main(String[] args) {
        ArrayList<Integer> nums = new ArrayList<>();
        Collections.addAll(nums, 6, 9, 5, 1, 4); // 向nums中添加数个元素
        
        Collections.sort(nums); // 默认升序排序
        
        // 使用Comparator比较器修改为按降序规则排序
        Collections.sort(nums, new Comparator<Integer>() {
            @Override
            public int compare(Integer a, Integer b) { // 覆盖重写compare比较规则
                return b - a; // 如果返回值大于0按降序规则排序, 如果小于0按升序规则排序
            }
        }); // [9, 6, 5, 4, 1]
// ---------------------------------------------------
        ArrayList<DemoClass> list = new ArrayList<>();
        DemoClass demo1 = new DemoClass("abc", 18);
        DemoClass demo2 = new DemoClass("bcd", 19);
        DemoClass demo3 = new DemoClass("efg", 19);
        Collections.addAll(list, demo1, demo2, demo3);

        Collections.sort(list); // [DemoClass{name='abc', age=18}, DemoClass{name='efg', age=19}, DemoClass{name='bcd', age=19}]

        Collections.sort(list, new Comparator<DemoClass>() {
            @Override // 重写比较规则：第一规则按年龄升序排序，第二比较规则按字符串大小降序排序
            public int compare(DemoClass o1, DemoClass o2) {
                return (o1.getAge() - o2.getAge()) != 0 ? o1.getAge() - o2.getAge() : o2.getName().compareTo(o1.getName());
            }
        });
        System.out.println(list);
    }
}

/*
 * 如果要对自定义的类的对象按照你想要的规则进行排序，那么就需要覆盖重写Comparable<E>接口的compareTo方法
 */
public class DemoClass implements Comparable<DemoClass> { // 注意书写格式
    private String name;
    public int age;
    // ...
    
    @Override // 重写比较规则：第一规则按年龄升序排序，第二比较规则按字符串大小降序排序
    public int compareTo(DemoClass o) {
        return (this.getAge() - o.getAge()) != 0 ? this.getAge() - o.getAge():o.getName().compareTo(this.getName());
    }
}
```

**Comparator与Comparable两个接口的区别**：

**Comparable**：强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序，类的compareTo方法被称为它的自然比较方法。**只能在类中实现compareTo()一次，不能经常修改类的代码实现自己想要的排序**。实现此接口的对象列表（和数组）可以通过Collections.sort（和Arrays.sort）进行自动排序，对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。

**Comparator**强行对某个对象进行整体排序。**可以将Comparator 传递给sort方法（如Collections.sort或 Arrays.sort），从而允许在排序规则上实现精确控制**。还可以使用Comparator来控制某些数据结构（如有序set或有序映射）的顺序，或者为那些没有自然顺序的对象collection提供排序。

#### HashMap集合

```java
/*
    java.util.Map<k,v>集合
    Map集合的特点:
        1.Map集合是一个双列集合,一个元素包含两个值(一个key,一个value)
        2.Map集合中的元素,key和value的数据类型可以相同,也可以不同
        3.Map集合中的元素,key是不允许重复的,value是可以重复的
        4.Map集合中的元素,key和value是一一对应
    java.util.HashMap<k,v>集合 implements Map<k,v>接口
    HashMap集合的特点:
        1.HashMap集合底层是哈希表:查询的速度特别的快
            JDK1.8之前:数组+单向链表
            JDK1.8之后:数组+单向链表|红黑树(链表的长度超过8):提高查询的速度
        2.hashMap集合是一个无序的集合,存储元素和取出元素的顺序有可能不一致
   java.util.LinkedHashMap<k,v>集合 extends HashMap<k,v>集合
   LinkedHashMap的特点:
        1.LinkedHashMap集合底层是哈希表+链表(保证迭代的顺序)
        2.LinkedHashMap集合是一个【有序的集合,存储元素和取出元素的顺序是一致的】
 */

public class Day01 {
    public static void main(String[] args) {
        HashMap<String, Integer> hashMap = new HashMap<>();
        hashMap.put("a", 1);
        hashMap.put("b", 2);
        hashMap.size();
        hashMap.get("a");
        hashMap.containsKey("a");
        hashMap.containsValue(3);
        hashMap.isEmpty();
        hashMap.remove("b");
        hashMap.put("a", hashMap.get("a") + 1); // 对key = "a" 处的值进行加一操作

        // 遍历Map方式一：使用keySet()方法把所有键放入Set()集合，然后通过遍历Set()集合中的key获取Map对应的Value
        for (String key : hashMap.keySet()) {
            System.out.println(key + " = " + hashMap.get(key));
        }
        
        // 遍历Map方式二：通过在Set()集合中嵌套内部Entry类实现将键值对象对存入Set()集合, 然后遍历Set()集合中的每一个Entry对象
        Set<Map.Entry<String, Integer>> entries = hashMap.entrySet();
        for (Map.Entry entry : entries) {
            System.out.println(entry.getKey() + " = " + entry.getValue());
        }
    }
}
```

- 接口 `Map.Entry<K,V>` 映射项（键-值对）。

```java
// 遍历Map方式二：通过在Set()集合中嵌套内部Entry类实现将键值对象对存入Set()集合, 然后遍历Set()集合中的每一个Entry对象
Set<Map.Entry<String, Integer>> entries = hashMap.entrySet();
for (Map.Entry entry : entries) {
    System.out.println(entry.getKey() + " = " + entry.getValue());
}
```

- 当给HashMap中存放自定义对象时，如果自定义对象作为key存在，这时要保证对象唯一，必须复写对象的hashCode和equals方法(如果忘记，请回顾HashSet存放自定义对象)。
- 如果要保证map中存放的key和取出的顺序一致，可以使用`java.util.LinkedHashMap`集合来存放。

#### JDK9新特性：of

```java
/*
    JDK9的新特性:
        List接口,Set接口,Map接口:【里边增加了一个静态的方法of,可以给集合一次性添加多个元素】
        static <E> List<E> of (E... elements)
        使用前提:
            当集合中存储的元素的个数已经确定了,不再改变时才能使用
     注意:
        1.【of方法只适用于List接口,Set接口,Map接口】,不适用于接接口的实现类
        2.of方法的返回值是一个不能改变的集合,【集合不能再使用add,put方法添加元素,会抛出异常】
        3.【Set接口和Map接口在调用of方法的时候,不能有重复的元素】,否则会抛出异常
 */
public class Demo01JDK9 {
    public static void main(String[] args) {
        List<String> list = List.of("a", "b", "a", "c", "d");
        System.out.println(list);//[a, b, a, c, d]
        //list.add("w");//UnsupportedOperationException:不支持操作异常

        //Set<String> set = Set.of("a", "b", "a", "c", "d");//IllegalArgumentException:非法参数异常,有重复的元素
        Set<String> set = Set.of("a", "b", "c", "d");
        System.out.println(set);
        //set.add("w");//UnsupportedOperationException:不支持操作异常

        //Map<String, Integer> map = Map.of("张三", 18, "李四", 19, "王五", 20,"张三",19);////IllegalArgumentException:非法参数异常,有重复的元素
        Map<String, Integer> map = Map.of("张三", 18, "李四", 19, "王五", 20);
        System.out.println(map);//{王五=20, 李四=19, 张三=18}
        //map.put("赵四",30);//UnsupportedOperationException:不支持操作异常
    }
}
```

### 异常

#### 异常产生的过程分析

![image-20200724231545747](https://github.com/Pursue26/JavaSE/blob/master/JavaSE.assets/image-20200724231545747.png)

### 多线程

#### 并发与并行

* **并发**：指两个或多个事件在**同一个时间段内**发生。
* **并行**：指两个或多个事件在**同一时刻**发生（同时发生）。

> 你吃饭吃到一半，电话来了，你一直到吃完了以后才去接，这就说明你不支持并发也不支持并行。
> 你吃饭吃到一半，电话来了，你停了下来接了电话，接完后继续吃饭，这说明你支持并发。
> 你吃饭吃到一半，电话来了，你一边打电话一边吃饭，这说明你支持并行。
>
> 并发的关键是你有处理多个任务的能力，不一定要同时。
> 并行的关键是你有同时处理多个任务的能力。
>
> 所以我认为它们最关键的点就是：是否是『同时』。

#### 进程与线程

* **进程**：是指一个内存中运行的应用程序，每个进程都有一个独立的内存空间，一个应用程序可以同时运行多个进程；进程也是程序的一次执行过程，是系统运行程序的基本单位；系统运行一个程序即是一个进程从创建、运行到消亡的过程。

* **线程**：线程是进程中的一个执行单元，负责当前进程中程序的执行，一个进程中至少有一个线程。一个进程中是可以有多个线程的，这个应用程序也可以称之为多线程程序。 

  简而言之：一个程序运行后至少有一个进程，一个进程中可以包含多个线程 

#### 线程实现方式1（继承方式）

```java
public class MyThread extends Thread {
    public static void main(String[] args) {
        MyThread th = new MyThread();
        th.start();
        for (int i = 11; i < 21; i++) {
            System.out.println("线程B：" + i);
        }
    }

    @Override
    public void run() { // 设置线程任务（开启线程后要做什么）
        for (int i = 0; i < 10; i++) {
            System.out.println("线程A：" + i);
        }
    }
}
/*
线程B：11
线程B：12
线程A：0
线程B：13
线程A：1
...
*/
```

![image-20201007191132682](JAVA notes.assets/image-20201007191132682.png)

多线程内存空间分配：

![image-20201007191632761](JAVA notes.assets/image-20201007191632761.png)

#### 获取、设置线程的名称

获取线程名称：`getName()` 或者 `Thread.currentThread().getName()`。

```java
设置线程的名称：

1.使用Thread类中的方法setName(线程名)
    void setName(String name) 改变线程名称，使之与参数 name 相同。
2.创建一个带参数的构造方法,参数传递线程的名称;调用父类的带参构造方法,把线程名称传递给父类,让父类(Thread)给子线程起一个名字
    Thread(String name) 分配新的 Thread 对象。

public class MyThread extends Thread {
    public static void main(String[] args) {
        MyThread th = new MyThread("线程A");
        th.start();
        for (int i = 11; i < 21; i++) {
            System.out.println("线程B：" + i);
        }
    }

    public MyThread(String name) { // 方式 2
        super(name);
    }

    @Override
    public void run() {
        setName("线程C"); // 方式 1
        System.out.println(getName()); // 线程C
        System.out.println(Thread.currentThread()); // Thread[线程C,5,main]
        for (int i = 0; i < 10; i++) {
            System.out.println("线程A：" + i);
        }
    }
}
```

#### 实现多线程的方式2（实现Runnable接口）

- 创建多线程程序的第二种方式及步骤。
- 实现Runnable接口创建多线程程序的好处。

```java
创建多线程程序的第二种方式:    实现Runnable接口
java.lang.Runnable
    Runnable 接口应该由那些打算通过某一线程执行其实例的类来实现。类必须定义一个称为 run 的无参数方法。
java.lang.Thread类的构造方法
    Thread(Runnable target) 分配新的 Thread 对象。
    Thread(Runnable target, String name) 分配新的 Thread 对象。

实现步骤:
    1.创建一个Runnable接口的实现类
    2.在实现类中重写Runnable接口的run方法,设置线程任务
    3.创建一个Runnable接口的实现类对象
    4.创建Thread类对象,构造方法中传递Runnable接口的实现类对象
    5.调用Thread类中的start()方法,开启新的线程执行run方法

实现Runnable接口创建多线程程序的好处:
    1.避免了单继承的局限性
        一个类只能继承一个类(一个人只能有一个亲爹),类继承了Thread类就不能继承其他的类
        实现了Runnable接口,还可以继承其他的类,实现其他的接口
    2.增强了程序的扩展性,降低了程序的耦合性(解耦)
        实现Runnable接口的方式,把设置线程任务和开启新线程进行了分离(即解耦)
        	实现类中,重写了run方法:用来设置线程任务
        	创建Thread类对象,调用start()方法:用来开启新线程


 // public class RunnableImpl  extends Thread implements Runnable{    }
 public class RunnableImpl implements Runnable {
    public static void main(String[] args) {
        Runnable r = new RunnableImpl();
        Thread th = new Thread(r);
        th.start();
        for (int i = 11; i < 20; i++) {
            System.out.println(Thread.currentThread().getName() + " & " + i);
        }
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + " | " + i);
        }
    }
}
```

#### 线程安全问题

![image-20201008142557456](JAVA notes.assets/image-20201008142557456.png)

#### 线程同步

解决线程安全问题的方案一：**使用同步代码块**。

```java
格式：
synchronized (锁对象) { 
    //  可能会出现线程安全问题的代码(访问了共享数据的代码) 
}

// --------------------------------

public class RunnableImpl implements Runnable {
    private int ticket = 1000;
    Object obj = new Object(); // 锁对象（可以任意，this也行）

    public static void main(String[] args) {
        Runnable r = new RunnableImpl();
        Thread t1 = new Thread(r);
        Thread t2 = new Thread(r);
        Thread t3 = new Thread(r); // 开启三个线程
        t1.start(); // 线程1
        t2.start(); // 线程2
        t3.start(); // 线程3
    }

    @Override
    public void run() {
        while (true) {
            synchronized (obj) { // 同步代码块
                if (ticket > 0) {
                    System.out.println(Thread.currentThread().getName() + " | 第 " + ticket + " 张票");
                    ticket--;
                }
            }
        }
    }
}
```

- 同步代码块保证了只有一个线程在同步执行共享的数据，从而保证了线程安全。
- 当一个线程出现问题后，不会影响程序的正常执行，因为还有别的线程可以保证程序的正常运行。
- 缺点：程序频繁的判断锁、获取锁、释放锁，导致程序的效率会降低。

`synchronized` 同步的原理解释图：

![image-20201008144627734](JAVA notes.assets/image-20201008144627734.png)

解决线程安全问题的方案二：**使用同步方法（或静态同步方法）**。

- 使用同步方法的锁对象是谁？就是这个类对象（即 `this`）。

```java
// 定义同步方法的格式
修饰符 synchronized 返回值类型 方法名(参数列表){
    // 可能会出现线程安全问题的代码(访问了共享数据的代码)
}


public class RunnableImpl implements Runnable {
    private int ticket = 1000;

    public static void main(String[] args) {
        Runnable r = new RunnableImpl();
        Thread t1 = new Thread(r);
        Thread t2 = new Thread(r);
        Thread t3 = new Thread(r); // 开启三个线程
        t1.start(); // 线程1
        t2.start(); // 线程2
        t3.start(); // 线程3
    }

    @Override
    public void run() {
        payTicket();
    }

    public synchronized void payTicket() { // 定义同步方法
        while (true) {
            if (ticket > 0) {
                System.out.println(Thread.currentThread().getName() + " | 第 " + ticket + " 张票");
                ticket--;
            }
        }
    }
}
```

- 使用静态同步方法的锁对象是谁？不再是这个类对象 `this`，因为 `this` 是创建类对象之后产生的，静态方法优先于对象产生。静态同步方法的锁对象是本类的 `class` 属性（`class`文件对象：`类名.class`）。

```java
public class RunnableImpl implements Runnable {
    private static int ticket = 1000; // 静态成员变量

    public static void main(String[] args) {
        Runnable r = new RunnableImpl();
        Thread t1 = new Thread(r);
        Thread t2 = new Thread(r);
        Thread t3 = new Thread(r);
        t1.start(); // 线程1
        t2.start(); // 线程2
        t3.start(); // 线程3
    }

    @Override
    public void run() {
        payTicket2();
    }

    public static synchronized void payTicket2() { // 静态同步方法, 锁对象: RunnableImpl.class
        while (true) {
            if (ticket > 0) {
                System.out.println(Thread.currentThread().getName() + " | 第 " + ticket + " 张票");
                ticket--;
            }
        }
    }
}
```

解决线程安全问题的方案三：**使用Lock锁**。

`Lock` 实现提供了比使用 `synchronized` 方法和语句可获得的更广泛的锁定操作。

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/*
    解决线程安全问题的三种方案:使用Lock锁
    java.util.concurrent.locks.Lock接口
    Lock 实现提供了比使用 synchronized 方法和语句可获得的更广泛的锁定操作。
    Lock接口中的方法:
        void lock()获取锁。
        void unlock()  释放锁。
    java.util.concurrent.locks.ReentrantLock implements Lock接口

    使用步骤:
        1.在成员位置创建一个ReentrantLock对象
        2.在可能会出现安全问题的代码前调用Lock接口中的方法lock获取锁
        3.在可能会出现安全问题的代码后调用Lock接口中的方法unlock释放锁
 */
public class RunnableImpl implements Runnable {
    private int ticket = 1000;
    Lock l = new ReentrantLock(); // Lock锁, 接口 = 实现类

    public static void main(String[] args) {
        Runnable r = new RunnableImpl();
        Thread t1 = new Thread(r);
        Thread t2 = new Thread(r);
        Thread t3 = new Thread(r);
        t1.start(); // 线程1
        t2.start(); // 线程2
        t3.start(); // 线程3
    }

    @Override
    public void run() {
        payTicket();
    }

    public synchronized void payTicket() { // RunnableImpl.class
        l.lock(); // 获取锁
        // 锁定和取消锁定出现在不同作用范围中时，必须谨慎地确保保持锁定时所执行的所有代码
        // 用 try-finally 或 try-catch 加以保护，以确保在必要时释放锁。
        try {
            while (true) {
                if (ticket > 0) {
                    System.out.println(Thread.currentThread().getName() + " | 第 " + ticket + " 张票");
                    ticket--;
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            l.unlock(); // 释放锁（无论程序是否异常, 都会把锁释放, 提高效率）
        }
    }
}
```

#### 线程状态

当线程被创建并启动以后，它既不是一启动就进入了执行状态，也不是一直处于执行状态。在线程的生命周期中，有几种状态呢？在API中 `java.lang.Thread.State` 这个枚举中给出了**六种线程状态**：  

| 线程状态                 | 导致状态发生条件                                             |
| ------------------------ | ------------------------------------------------------------ |
| NEW(新建)                | 线程刚被创建，但是并未启动。还没调用start方法。              |
| Runnable(可 运行)        | 线程可以在java虚拟机中运行的状态，可能正在运行自己代码，也可能没有，这取决于操 作系统处理器。 |
| Blocked(锁阻 塞)         | 当一个线程试图获取一个对象锁，而该对象锁被其他的线程持有，则该线程进入Blocked状 态；当该线程持有锁时，该线程将变成Runnable状态。 |
| Waiting(无限 等待)       | 一个线程在等待另一个线程执行一个（唤醒）动作时，该线程进入Waiting状态。进入这个 状态后是不能自动唤醒的，必须等待另一个线程调用notify或者notifyAll方法才能够唤醒。 |
| Timed Waiting(计时 等待) | 同waiting状态，有几个方法有超时参数，调用他们将进入Timed Waiting状态。这一状态 将一直保持到超时期满或者接收到唤醒通知。带有超时参数的常用方法有Thread.sleep 、 Object.wait。 |
| Teminated(被 终止)       | 因为run方法正常退出而死亡，或者因为没有捕获的异常终止了run方法而死亡。 |

![image-20201008163814282](JAVA notes.assets/image-20201008163814282.png)

#### 等待唤醒状态

线程间通信：多个线程在处理同一个资源，但是处理的动作（线程的任务）却不相同。

> 比如：线程A用来生成包子的，线程B用来吃包子的，包子可以理解为同一资源，线程A与线程B处理的动作，一个是生产，一个是消费，那么线程A与线程B之间就存在线程通信问题。

**为什么要处理线程间通信**：

多个线程并发执行时, 在默认情况下CPU是随机切换线程的，当我们需要多个线程来共同完成一件任务，并且希望它们有规律的执行，那么多线程之间需要一些协调通信，以此来帮我们达到多线程共同操作一份数据。

**如何保证线程间通信有效利用资源**：

多个线程在处理同一个资源并且任务不同时，需要线程通信来帮助解决线程之间对同一个变量的使用或操作。 就是多个线程在操作同一份数据时， 避免对同一共享变量的争夺。也就是我们需要通过一定的手段使各个线程能有效的利用资源。而这种手段即—— **等待唤醒机制**。等待唤醒机制使得多个线程之间有效利用CPU资源。

![image-20201008165210150](JAVA notes.assets/image-20201008165210150.png)

```java
类 Object 下的方法：

void wait()   在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前，导致当前线程等待。 
void wait(long timeout) 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法，或者超过指定的时间量timeout前，导致当前线程等待, 超过timeout后不再等待。 
void notify()    唤醒在此对象监视器上等待的单个线程。 
void notifyAll()     唤醒在此对象监视器上等待的所有线程。 
```

等待唤醒示例：顾客告知老板要买甜甜圈，告知后等待老板做甜甜圈，老板做完后告知顾客，顾客开吃。

```java
public class Main2 {
    static int num = 0;
    public static void main(String[] args) {
        Object obj = new Object(); // wait 与 notify 需要是同一个锁对象
        new Thread() {
            @Override
            public void run() {
                num = 3;
                System.out.println("我要买 " + num + " 个甜甜圈");
                synchronized (obj) {
                    try {
                        obj.wait();
                        System.out.println("买完之后开吃...");
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("吃完了...");
                }
            }
        }.start();

        new Thread() {
            @Override
            public void run() {
                for (int i = 1; i <= num; i++) {
                    try {
                        Thread.sleep(50);
                        System.out.println("做完第 " + i + " 个甜甜圈");
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                synchronized (obj) {
                    System.out.println("给你, 一共100元...");
                    obj.notify(); // 如果有多个线程, 随机唤醒一个线程
//                    obj.notifyAll(); // 如果有多个线程, 随机唤醒一个线程
                }
            }
        }.start();
    }
}
/*
    我要买 3 个甜甜圈  // 线程1 --> obj.wait();
    做完第 1 个甜甜圈  // 线程2
    做完第 2 个甜甜圈  // 线程2
    做完第 3 个甜甜圈  // 线程2
    给你, 一共100元... // 线程2 --> obj.notify();
    买完之后开吃... // 线程1
    吃完了...      // 线程1
 */
```

**调用 `wait()` 和 `notify()`方法需要注意的细节**：

1. `wait()`方法与`notify()`方法必须要**由同一个锁对象调用**。因为：对应的锁对象可以通过`notify()`唤醒使用同一个锁对象调用的`wait()`方法后的线程。
2. `wait()`方法与`notify()`方法属于`Object`类的成员方法。因为：锁对象可以是任意对象，而任意对象的所属类都是**继承**了`Object`类的。
3. `wait()`方法与`notify()`方法必须要在同步代码块或者是同步方法中使用。因为：必须要通过锁对象调用这两个方法。

#### 线程池

> 我们使用线程的时候就去创建一个线程，这样实现起来非常简便，但是就会有一个问题：
>
> 如果并发的线程数量很多，并且每个线程都是执行一个时间很短的任务就结束了，这样频繁创建线程就会大大降低系统的效率，因为频繁创建线程和销毁线程需要时间。有没有一种办法使得线程可以复用，就是执行完一个任务，并不被销毁，而是可以继续执行其他的任务？—— 线程池。

**线程池：**其实就是一个容纳多个线程的容器，其中的**线程可以反复使用，省去了频繁创建线程对象的操作**，无需反复创建线程而消耗过多资源。

合理利用线程池能够带来三个好处：

1. 降低资源消耗。通过重用已存在的线程，降低线程创建和销毁造成的消耗；
2. 提高系统响应速度。当有任务到达时，通过复用已存在的线程，无需等待新线程的创建便能立即执行；
3. 方便线程并发数的管控。因为线程若是无限制的创建，可能会导致内存占用过多而产生OOM（每个线程大约需要1MB内存），并且会造成CPU过度切换（CPU切换线程是有时间成本的（需要保持当前执行线程的现场，并恢复要执行线程的现场））。

```java
// 线程池的使用
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/*
    线程池:JDK1.5之后提供的
    java.util.concurrent.Executors:线程池的工厂类,用来生成线程池
    Executors类中的静态方法:
        static ExecutorService newFixedThreadPool(int nThreads) 创建一个可重用固定线程数的线程池
        参数:
            int nThreads:创建线程池中包含的线程数量
        返回值:
            ExecutorService接口,返回的是ExecutorService接口的实现类对象,我们可以使用ExecutorService接口接收(面向接口编程)
    java.util.concurrent.ExecutorService:线程池接口
        用来从线程池中获取线程,调用start()方法,执行线程任务
            submit(Runnable task) 提交一个 Runnable 任务用于执行
        关闭/销毁线程池的方法
            void shutdown()
    
    
    线程池的使用步骤:
        1.使用线程池的工厂类Executors里边提供的静态方法newFixedThreadPool(x)生产一个指定线程数量x的线程池
        2.创建一个类,实现Runnable接口,重写run方法,设置线程任务
        3.调用ExecutorService中的方法submit,传递线程任务(实现类),开启线程,执行run方法
        4.调用ExecutorService中的方法shutdown销毁线程池(不建议执行)
 */
public class Main2 {
    public static void main(String[] args) {
        //1.使用线程池的工厂类Executors里边提供的静态方法newFixedThreadPool生产一个指定线程数量的线程池
        ExecutorService es = Executors.newFixedThreadPool(2);
        //3.调用ExecutorService中的方法submit,传递线程任务(实现类),开启线程,执行run方法
        es.submit(new RunnableImpl()); //pool-1-thread-1创建了一个新的线程执行
        //线程池会一直开启,使用完了线程,会自动把线程归还给线程池,线程可以继续使用
        es.submit(new RunnableImpl()); //pool-1-thread-1创建了一个新的线程执行
        es.submit(new RunnableImpl()); //pool-1-thread-2创建了一个新的线程执行

        //4.调用ExecutorService中的方法shutdown销毁线程池(不建议执行)
        es.shutdown();

//        es.submit(new RunnableImpl()); //抛异常,线程池都没有了,就不能获取线程了
    }

}
```

### Lambda表达式

#### Lambda表达式的标准格式

```java
/*
    Lambda表达式的标准格式:
        由三部分组成:
            a. 一些参数
            b. 一个箭头
            c. 一段代码
        格式:
            (参数列表) -> {一些重写方法的代码};
        解释说明格式:
            (): 接口中抽象方法的参数列表,没有参数,就空着;有参数就写出参数,多个参数使用逗号分隔
            ->: 传递的意思,把参数传递给方法体{}
            {}: 重写接口的抽象方法的方法体
 */
public class Main2 {
    public static void main(String[] args) {
        // 使用匿名内部类实现一个多线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName());
            }
        }).start();

        // 使用Lambda表达式实现一个多线程
        new Thread(() -> {
            System.out.println(Thread.currentThread().getName());
        }).start();
    }
}
```

#### Lambda表达式的省略格式

```java
/*
    Lambda表达式:是可推导,可以省略
    凡是根据上下文推导出来的内容,都可以省略书写
    可以省略的内容:
        1.(参数列表):括号中参数列表的数据类型,可以省略不写
        2.(参数列表):括号中的参数如果只有一个,那么类型和()都可以省略
        3.{一些代码}:如果{}中的代码只有一行,无论是否有返回值,都可以省略({},return,分号)
            注意:要省略({},return,分号)必须一起省略
 */
new Thread(() -> System.out.println(Thread.currentThread().getName())).start();
```

#### Lambda表达式的使用前提

1. 使用Lambda必须具有接口，且要求**接口中有且仅有一个抽象方法**。
   无论是JDK内置的`Runnable`、`Comparator`接口还是自定义的接口，只有当接口中的抽象方法存在且唯一时，才可以使用Lambda。
2. 使用Lambda必须具有**上下文推断**。
   也就是方法的参数或局部变量类型必须为Lambda对应的接口类型，才能使用Lambda作为该接口的实例。

> 备注：有且仅有一个抽象方法的接口，称为“**函数式接口**”。

### File类

#### File类字段摘要

```java
static String pathSeparator 
          与系统有关的路径分隔符，为了方便，它被表示为一个字符串。 
static char pathSeparatorChar 
          与系统有关的路径分隔符。 
static String separator 
          与系统有关的默认名称分隔符，为了方便，它被表示为一个字符串。 
static char separatorChar 
          与系统有关的默认名称分隔符。 
```

#### File类构造方法摘要

```java
File(File parent, String child) 
          根据 parent 抽象路径名和 child 路径名字符串创建一个新 File 实例。 
File(String pathname) 
          通过将给定路径名字符串转换为抽象路径名来创建一个新 File 实例。 
File(String parent, String child) 
          根据 parent 路径名字符串和 child 路径名字符串创建一个新 File 实例。 
File(URI uri) 
          通过将给定的 file: URI 转换为一个抽象路径名来创建一个新的 File 实例。 
```

#### File类方法摘要

```java
  int  compareTo(File pathname) 
          按字母顺序比较两个抽象路径名。 
  boolean  createNewFile() 
          当且仅当不存在具有此抽象路径名指定名称的文件时，不可分地创建一个新的空文件。 
  boolean  delete() 
          删除此抽象路径名表示的文件或目录。 
  boolean  equals(Object obj) 
          测试此抽象路径名与给定对象是否相等。 
  boolean  exists() 
          测试此抽象路径名表示的文件或目录是否存在。 
  File  getAbsoluteFile() 
          返回此抽象路径名的绝对路径名形式。 
  String  getAbsolutePath() 
          返回此抽象路径名的绝对路径名字符串。 
  String  getName() 
          返回由此抽象路径名表示的文件或目录的名称。 
  String  getParent() 
          返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回 null。 
  File  getParentFile() 
          返回此抽象路径名父目录的抽象路径名；如果此路径名没有指定父目录，则返回 null。 
  String  getPath() 
          将此抽象路径名转换为一个路径名字符串。 
  boolean  isAbsolute() 
          测试此抽象路径名是否为绝对路径名。 
  boolean  isDirectory() 
          测试此抽象路径名表示的文件是否是一个目录。 
  boolean  isFile() 
          测试此抽象路径名表示的文件是否是一个标准文件。  
  long  length() 
          返回由此抽象路径名表示的文件的长度。 
  String[]  list() 
          返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中的文件和目录。 
  String[]  list(FilenameFilter filter) 
          返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中满足指定过滤器的文件和目录。 
  File[]  listFiles() 
          返回一个抽象路径名数组，这些路径名表示此抽象路径名表示的目录中的文件
```

#### 文件过滤器优化

`java.io.FileFilter`是一个接口，是File的过滤器。 该接口的对象可以传递给File类的`listFiles(FileFilter)` 作为参数， 接口中只有一个方法。

`boolean accept(File pathname)  ` ：测试pathname是否应该包含在当前File目录中，符合则返回true。

**分析**：

1. 接口作为参数，需要传递实现类对象，重写其中方法。为了简便，可以省去定义实现类的操作，直接选择使用匿名内部类方式作为其参数。

2. `accept`方法，参数为File类型，表示当前File下所有的子文件和子目录。保留则返回true，过滤掉则返回false。自定义保留规则，例如：

   > 1. 要么是.java文件。
   > 2. 要么是目录，用于继续遍历。

**代码实现：**

```java
public class DiGuiDemo4 {
    public static void main(String[] args) {
        File dir = new File("D:\\aaa");
        printDir2(dir);
    }
  
    public static void printDir2(File dir) {
      	// 匿名内部类方式, 创建过滤器子类对象
        File[] files = dir.listFiles(new FileFilter() {
            @Override
            public boolean accept(File pathname) {
                return pathname.isDirectory() || pathname.getName().endsWith(".java");
            }
        });
        
      	// 循环打印
        for (File file : files) {
            if (file.isFile()) {
                System.out.println("文件名:" + file.getAbsolutePath());
            } else {
                printDir2(file);
            }
        }
    }
}
```

### I/O流

#### I/O流分类

根据数据的流向分为：**输入流**和**输出流**。

* **输入流** ：把数据从`其他设备`上读取到 `内存` 中的流。 
* **输出流** ：把数据从`内存` 中写出到 `其他设备`上的流。

根据数据的类型分为：**字节流**和**字符流**。（1字符 = 2字节）

* **字节流** ：以字节为单位，读写数据的流。
* **字符流** ：以字符为单位，读写数据的流。

|            |          **输入流**           |             输出流             |
| :--------: | :---------------------------: | :----------------------------: |
| **字节流** | 字节输入流    **InputStream** | 字节输出流    **OutputStream** |
| **字符流** |   字符输入流    **Reader**    |    字符输出流    **Writer**    |

#### 字节流 OutputStream与InputStream

```java
java.lang.Object
  继承者 java.io.OutputStream
      继承者 java.io.FileOutputStream

构造方法摘要 
FileOutputStream(File file) 
          创建一个向指定 File 对象表示的文件中写入数据的文件输出流。 
FileOutputStream(File file, boolean append) 
          创建一个向指定 File 对象表示的文件中写入数据的文件输出流。 
FileOutputStream(FileDescriptor fdObj) 
          创建一个向指定文件描述符处写入数据的输出文件流，该文件描述符表示一个到文件系统中的某个实际文件的现有连接。 
FileOutputStream(String name) 
          创建一个向具有指定名称的文件中写入数据的输出文件流。 
FileOutputStream(String name, boolean append) 
          创建一个向具有指定 name 的文件中写入数据的输出文件流。 

方法摘要 
 void close() 
          关闭此文件输出流并释放与此流有关的所有系统资源。 
protected  void finalize() 
          清理到文件的连接，并确保在不再引用此文件输出流时调用此流的 close 方法。 
 FileChannel getChannel() 
          返回与此文件输出流有关的唯一 FileChannel 对象。 
 FileDescriptor getFD() 
          返回与此流有关的文件描述符。 
 void write(byte[] b) 
          将 b.length 个字节从指定 byte 数组写入此文件输出流中。 
 void write(byte[] b, int off, int len) 
          将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此文件输出流。 
 void write(int b) 
          将指定字节写入此文件输出流。 

    
    
java.lang.Object
  继承者 java.io.InputStream
      继承者 java.io.FileInputStream

构造方法摘要 
FileInputStream(File file) 
          通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的 File 对象 file 指定。 
FileInputStream(FileDescriptor fdObj) 
          通过使用文件描述符 fdObj 创建一个 FileInputStream，该文件描述符表示到文件系统中某个实际文件的现有连接。 
FileInputStream(String name) 
          通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的路径名 name 指定。 

方法摘要 
 int available() 
          返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取（或跳过）的估计剩余字节数。 
 void close() 
          关闭此文件输入流并释放与此流有关的所有系统资源。 
protected  void finalize() 
          确保在不再引用文件输入流时调用其 close 方法。 
 FileChannel getChannel() 
          返回与此文件输入流有关的唯一 FileChannel 对象。 
 FileDescriptor getFD() 
          返回表示到文件系统中实际文件的连接的 FileDescriptor 对象，该文件系统正被此 FileInputStream 使用。 
 int read() 
          从此输入流中读取一个数据字节。 
 int read(byte[] b) 
          从此输入流中将最多 b.length 个字节的数据读入一个 byte 数组中。 
 int read(byte[] b, int off, int len) 
          从此输入流中将最多 len 个字节的数据读入一个 byte 数组中。 
 long skip(long n) 
          从输入流中跳过并丢弃 n 个字节的数据。 
```

向硬盘中写入、读取数据演示：

```java
public class Main2 { // 向硬盘中写入 --- 输出流
    public static void main(String[] args) throws IOException {
        FileOutputStream fos = new FileOutputStream(new File("1.txt"), true);
//        FileOutputStream fos2 = new FileOutputStream("2.txt", true);
        byte[] s2 = "nihao".getBytes();
        fos.write(s2);
        fos.write(97); // ASCII 97 即 a
        fos.write("\r\n".getBytes()); // windows的回车
        fos.close(); // 释放资源
    }
}

public class Main2 { // 从硬盘读入数据到内存 -- 输入流
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("1.txt");
        FileOutputStream fos = new FileOutputStream("2.txt");
        byte[] buffer = new byte[1024];
        int n = 0; // 读取的有效字节长度
        while ((n = fis.read(buffer)) != -1) { // 每次读取1024字节的
            System.out.println(new String(buffer));
            fos.write(buffer, 0, n); // 写入其他文件中
        }
        fos.close(); // 写操作完成了, 读操作一定完成, 故先释放写操作
        fis.close();

    }
}
```

#### 字符流 Reader与Writer

```java
字符输出流的使用步骤(重点):
	1.创建 FileWriter 对象, 构造方法中绑定要写入数据的目的地
	2.使用 FileWriter 中的方法 write, 把数据写入到内存缓冲区中(字符转换为字节的过程)
	3.使用 FileWriter 中的方法 flush, 把内存缓冲区中的数据,刷新到文件中(不调用flush也不调用close则不会刷新到文件中, 会从内存中消失)
	4.释放资源(会先把内存缓冲区中的数据刷新到文件中)

public class Main2 {
    public static void main(String[] args) throws IOException {
        FileReader fr = new FileReader("1.txt");
        FileWriter fw = new FileWriter("2.txt");

        char[] buffer = new char[1024];
        int n = 0;
        while ((n = fr.read(buffer)) != -1) {
            System.out.println(new String(buffer));
            fw.write(buffer, 0, n);
            fw.flush(); // 把内存缓冲区中的数据,刷新到文件中
        }
        fw.close();
        fr.close();
//        fw.write("你"); // Exception in thread "main" java.io.IOException: Stream closed
    }
}
```

#### try...catch处理IOException

- 在 JDK7 之后, 可以在 try 后边增加一个括号 () , **在括号内定义流对象**, 那么这个流对象的作用域就只在 try 大括号中有效; try 中的代码执行完之后, 会自动把流对象释放, 不用再写 finally。 

- 在 JDK9 之后, 可以**在 try 前面定义流对象**, 在try后边的**括号 () 内指出流对象是谁,** 那么这个流对象的作用域就只在 try 大括号中有效; try 中的代码执行完之后, 会自动把流对象释放, 不用再写 finally，**但是因为流对象是定义在 try 之前的，所以定义的流对象也需要处理异常情况。**

```java
格式：
    try(定义流对象A; 定义流对象B; ...){
        可能会产生异常的代码
    }catch(异常类变量 变量名){
        异常处理逻辑
    }

// JDK7
public class Main2 {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("1.txt");
             FileWriter fw = new FileWriter("2.txt")) {
            char[] buffer = new char[1024];
            int n = 0;
            while ((n = fr.read(buffer)) != -1) {
                System.out.println(new String(buffer));
                fw.write(buffer, 0, n);
                fw.flush();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

// JDK9
public class Main2 {
    public static void main(String[] args) throws IOException {
        FileReader fr = new FileReader("1.txt");
        FileWriter fw = new FileWriter("2.txt");
        try (fr; fw) {
            char[] buffer = new char[1024];
            int n = 0;
            while ((n = fr.read(buffer)) != -1) {
                System.out.println(new String(buffer));
                fw.write(buffer, 0, n);
                fw.flush();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### Properties类

`java.util.Properties ` 继承于` Hashtable` ，来表示一个持久的属性集。它使用键值结构存储数据，每个键及其对应值都是一个字符串。该类也被许多Java类使用，比如获取系统属性时，`System.getProperties` 方法就是返回一个`Properties`对象。

```java
java.util.Properties集合 extends Hashtable<k,v> implements Map<k,v>

Properties 类表示了一个持久的属性集。Properties 可保存在流中或从流中加载。
Properties 集合是一个唯一和 IO 流相结合的集合。
    可以使用 Properties 集合中的方法 store(), 把集合中的临时数据, 持久化写入到硬盘中存储。
    可以使用 Properties 集合中的方法 load(), 把硬盘中保存的文件(键值对), 读取到集合中使用。

Properties 集合是一个双列集合, 属性列表中每个键 key 及其对应值 value 都是一个字符串 String 类型。
```

方法摘要使用举例：

```java
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.IOException;
import java.util.Properties;
import java.util.Set;

public class Demo01Properties {
    /*
    使用Properties集合存储数据,遍历取出Properties集合中的数据

    Properties集合有一些操作字符串的特有方法:
        Object setProperty(String key, String value) 调用 Hashtable 的方法 put。
        String getProperty(String key) 通过key找到value值,此方法相当于Map集合中的get(key)方法
        Set<String> stringPropertyNames() 返回此属性列表中的键集，其中该键及其对应值是字符串,此方法相当于Map集合中的keySet()方法
     */
    private static void show01() {
        Properties prop = new Properties();
        prop.setProperty("赵丽颖","168");
        prop.setProperty("迪丽热巴","165");
        prop.setProperty("古力娜扎","160");

        //使用stringPropertyNames把Properties集合中的键取出,存储到一个Set集合中
        Set<String> set = prop.stringPropertyNames();
        for (String key : set) {
            String value = prop.getProperty(key);
            System.out.println(key + "=" + value);
        }
    }
    
    /*
        可以使用Properties集合中的方法store,把集合中的临时数据,持久化写入到硬盘中存储
        void store(OutputStream out, String comments)
        void store(Writer writer, String comments)
        参数:
            OutputStream out:字节输出流,不能向硬盘中写入中文
            Writer writer:字符输出流,可以向硬盘中写入中文
            String comments:注释,用来解释说明保存的文件是做什么用的
                    不能使用中文,会产生乱码,默认是Unicode编码, 一般使用""空字符串

        使用步骤:
            1.创建Properties集合对象,添加数据
            2.创建字节输出流/字符输出流对象,构造方法中绑定要输出的目的地
            3.使用Properties集合中的方法store,把集合中的临时数据,持久化写入到硬盘中存储
            4.释放资源
     */
    private static void show02() throws IOException {
        Properties prop = new Properties();
        prop.setProperty("赵丽颖","168");
        prop.setProperty("迪丽热巴","165");
        FileWriter fw = new FileWriter("09_IOAndProperties\\prop.txt");
        prop.store(fw,"save data");
        fw.close();
    }
    
    /*
        可以使用Properties集合中的方法load,把硬盘中保存的文件(键值对),读取到集合中使用
        void load(InputStream inStream)
        void load(Reader reader)
        参数:
            InputStream inStream: 字节输入流,不能读取含有中文的键值对
            Reader reader: 字符输入流,能读取含有中文的键值对
        使用步骤:
            1.创建Properties集合对象
            2.使用Properties集合对象中的方法load读取保存键值对的文件
            3.遍历Properties集合进行结果验证
        注意:
            1.存储键值对的文件中,键与值默认的连接符号可以使用等号或者空格
            2.存储键值对的文件中,可以使用 # 进行注释,被注释的键值对不会再被读取
            3.存储键值对的文件中,键与值默认都是字符串,不用再加引号
     */
    private static void show03() throws IOException {
        Properties prop = new Properties();
        prop.load(new FileReader("09_IOAndProperties\\prop.txt"));
        Set<String> set = prop.stringPropertyNames();
        for (String key : set) {
            String value = prop.getProperty(key);
            System.out.println(key+"="+value);
        }
    }
}
```

#### 缓冲流

缓冲流，也叫高效流，是对4个基本的`FileXxx` 流的增强，所以也是4个流，按照数据类型分类：

* **字节缓冲流**：`BufferedInputStream`，`BufferedOutputStream` 
* **字符缓冲流**：`BufferedReader`，`BufferedWriter`

缓冲流的基本原理：是在创建流对象时，**会创建一个内置的默认大小的缓冲区数组，通过缓冲区读写，减少系统IO次数，从而提高读写的效率**。

字节缓冲流的构造方法：

- `public BufferedInputStream(InputStream in)` ：创建一个新的缓冲输入流。 
- `public BufferedOutputStream(OutputStream out)`： 创建一个新的缓冲输出流。

```java
public class BufferedDemo {
    public static void main(String[] args) throws FileNotFoundException {
        long start = System.currentTimeMillis(); // 记录开始时间
		// 创建流对象
        try (
			BufferedInputStream bis = new BufferedInputStream(new FileInputStream("jdk9.exe"));
		 BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("copy.exe"));
        ){
          	// 读写数据
            int len;
            byte[] bytes = new byte[8*1024];
            while ((len = bis.read(bytes)) != -1) {
                bos.write(bytes, 0 , len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        long end = System.currentTimeMillis(); // 记录结束时间
        System.out.println("缓冲流使用数组复制时间:"+(end - start)+" 毫秒");
    }
}
```

字符缓冲流的构造方法：

* `public BufferedReader(Reader in)` ：创建一个新的缓冲输入流。 
* `public BufferedWriter(Writer out)`： 创建一个新的缓冲输出流。

字符缓冲流的基本方法与普通字符流调用方式一致。字符缓冲流具备的特有方法：

* BufferedReader：`public String readLine()`: 读一行文字（遇到换行\n、回车\r、回车换行\r\n ，即表示一行）。 
* BufferedWriter：`public void newLine()`: 写一行行分隔符（其实就是光标换行），由系统属性定义分隔符的符号。 

```java
public class BufferedWriterDemo throws IOException {
    public static void main(String[] args) throws IOException  {
		BufferedWriter bw = new BufferedWriter(new FileWriter("out.txt"));
        bw.write("123");
        bw.newLine(); // 换行
        bw.write("ac");
        bw.newLine();
        bw.close();
        BufferedReader br = new BufferedReader(new FileReader("out.txt"));
        String line;
        while((line = br.readline()) != null){
            System.out.println(line);
        }
    }
}
```

#### 转换流

转换流 `java.io.InputStreamReader`，是Reader的子类，**是从字节流到字符流的桥梁**。它读取字节，并使用指定的字符集将其解码为字符。它的字符集可以由名称指定，也可以接受平台的默认字符集。 

`InputStreamReader` 构造方法：

* `InputStreamReader(InputStream in)`:  创建一个使用默认字符集的字符流。 
* `InputStreamReader(InputStream in, String charsetName)`:  创建一个指定字符集的字符流。

`InputStreamReader` 读取文件时，构造方法中指定的编码表名称要和文件的编码格式相同，否则会发生乱码。

```java
public class ReaderDemo2 {
    public static void main(String[] args) throws IOException {
        String FileName = "E:\\file_gbk.txt";
      	// 创建流对象,默认UTF8编码
        InputStreamReader isr = new InputStreamReader(new FileInputStream(FileName));
      	// 创建流对象,指定GBK编码
        InputStreamReader isr2 = new InputStreamReader(new FileInputStream(FileName) , "GBK");
        int read;
        while ((read = isr.read()) != -1) {
            System.out.print((char)read); // (乱码) ��Һ�
        }
        isr.close();
      
      	// 使用指定编码字符流读取, 正常解析
        while ((read = isr2.read()) != -1) {
            System.out.print((char)read); // 大家好
        }
        isr2.close();
    }
}
```

转换流 `java.io.OutputStreamWriter` ，是Writer的子类，**是从字符流到字节流的桥梁**。使用指定的字符集将字符编码为字节。它的字符集可以由名称指定，也可以接受平台的默认字符集。

`java.io.OutputStreamWriter`  构造方法：

- `OutputStreamWriter(OutputStream in)`:  创建一个使用默认字符集的字符流。 
- `OutputStreamWriter(OutputStream in, String charsetName)`:  创建一个指定字符集的字符流。

GBK编码一个汉字占用2个字节，utf-8编码一个汉字占用3个字节。

```java
OutputStreamWriter osw2 = new OutputStreamWriter(new FileOutputStream("E:\\out2.txt"), "GBK");
osw2.write("你好"); // GBK编码一个汉字占用2个字节, "你好"为4个字节
osw2.close();
```

#### 序列化流

Java 提供了一种对象**序列化**的机制。**用一个字节序列可以表示一个对象**，该字节序列包含该 `对象的数据`、`对象的类型` 和 `对象中存储的属性`等信息。字节序列写出到文件之后，相当于文件中**持久保存**了一个对象的信息。 反之，该字节序列还可以从文件中读取回来，重构对象，对它进行**反序列化**。`对象的数据`、`对象的类型`和`对象中存储的数据`信息，都可以用来在内存中创建对象。

------

**序列化**：`java.io.ObjectOutputStream ` 类，将 Java **对象的原始数据类型**写出到文件，实现对象的持久存储。

构造方法：

* `public ObjectOutputStream(OutputStream out) `： 创建一个指定 `OutputStream` 的序列化流 `ObjectOutputStream`。

```java
public class SerializeDemo{
   	public static void main(String [] args)   {
    	Employee e = new Employee();
    	e.name = "zhangsan";
    	e.address = "beijing";
    	e.age = 20;  // 瞬态成员不会被序列化
    	try {
          ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("employee.txt"));
        	out.writeObject(e); // 写出对象
        	out.close(); // 释放资源
        } catch(IOException i)   {
            i.printStackTrace();
        }
   	}
}
```

**序列化操作**，一个对象要想序列化，必须满足两个条件：

* **该类**必须实现 `java.io.Serializable ` 接口，`Serializable` 是一个标记接口，不实现此接口的类将不会使任何状态序列化或反序列化，会抛出`NotSerializableException` 。
* 该类的所有属性必须是可序列化的。如果有一个属性不需要可序列化，则该属性必须注明是瞬态的，使用 `transient` 关键字修饰。

```java
public class Employee implements java.io.Serializable { // Employee 类实现 Serializable 接口
    public String name;
    public String address;
    public transient int age; // transient 瞬态修饰成员, 不会被序列化
    public void addressCheck() {
      	System.out.println("Address  check : " + name + " -- " + address);
    }
}
```

------

**反序列化**：`ObjectInputStream` 反序列化流，将之前使用 `ObjectOutputStream` 序列化的原始数据**恢复为对象**。 

构造方法：`public ObjectInputStream(InputStream in) `： 创建一个指定 `InputStream` 的 `ObjectInputStream`。

成员方法：`public final Object readObject ()` : 读取一个对象。

**对于JVM可以反序列化对象，它必须是能够找到class文件的类。如果找不到该类的class文件，则抛出一个 `ClassNotFoundException` 异常。**  

```java
public class DeserializeDemo {
   public static void main(String [] args)   {
        Employee e = null;
        try {		
             FileInputStream fileIn = new FileInputStream("employee.txt");
             ObjectInputStream in = new ObjectInputStream(fileIn);
             e = (Employee) in.readObject();
             in.close();
             fileIn.close();
        }catch(IOException i) {
             i.printStackTrace();
             return;
        }catch(ClassNotFoundException c)  {
        	// 找不到捕获类异常
             c.printStackTrace();
             return;
        }
        System.out.println("Name: " + e.name);	// zhangsan
    }
}
```

**另外，当JVM反序列化对象时，能找到class文件，但是现在修改class类中的内容，即class文件在序列化对象之后发生了修改，那么再次反序列化操作会失败，抛出一个`InvalidClassException`异常**。发生这个异常的原因如下：

* 该类的序列版本号与从流中读取的类描述符的**版本号 `serialVersionUID` 不匹配** 。
* 该类包含未知数据类型。
* 该类没有可访问的无参数构造方法。

`Serializable` 接口给需要序列化的类，提供了一个序列版本号 `serialVersionUID` 。该版本号的目的在于验证序列化的对象和对应类是否版本匹配。

```java
public class Employee implements java.io.Serializable {
     // 加入序列版本号 必须是 static final long
     private static final long serialVersionUID = 42L;
     public String name;
     public String address;
     // 添加新的属性 ,重新编译, 可以反序列化,该属性赋为默认值.
     public int eid; // 添加新的属性

     public void addressCheck() {
         System.out.println("Address  check : " + name + " -- " + address);
     }
}
```

### 网络编程

TCP协议中客户端与服务器进行一次数据传输。

注意：使用 `while ((n = inputStream.read(bytes)) != -1)`  从客户端上传数据给服务器时，并不会上传结束标记，那么自然服务器端收到的客户端的数据也不会带有结束标记，若此时使用 `while ((n = inputStream.read(bytes)) != -1)` 读取客户端的数据，会无法跳出 `while` 循环，故**需要在客户端发送数据末尾加入结束标记。**

- **因为 `read()` 方法在输入数据可用、检测到流末尾或者抛出异常前，此方法一直阻塞。** 

- **可以使用 `Socket` 类的 `shutdownOutput()` 方法。禁用此套接字的输出流。（**对于 TCP 套接字，任何以前写入的数据都将被发送，并且后跟 TCP 的正常连接终止序列。 如果在套接字上调用 `shutdownOutput()` 后写入套接字输出流，则该流将抛出 `IOException`。）

```java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.Socket;

public class MyClient {
    public static void main(String[] args) {
        try (Socket socket = new Socket("127.0.0.1", 8998)) {
            // 客户端使用自己的网络字节输出流给服务器端发送数据
            OutputStream outputStream = socket.getOutputStream();
            outputStream.write("服务器你好".getBytes());
            socket.shutdownOutput(); // 后跟 TCP 的正常连接终止序列

            // 客户端使用自己的网络字节输入流获取服务器端的数据
            InputStream inputStream = socket.getInputStream();
            byte[] bytes = new byte[1024];
            int n = 0; // 读取的有效字节长度
            while ((n = inputStream.read(bytes)) != -1) {
                System.out.println(new String(bytes, 0, n));
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


public class TCPServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8998);
             Socket socket = serverSocket.accept()) {
            // 获取客户端的网路字节输入流, 读取客户端的输入数据
            InputStream inputStream = socket.getInputStream();
            byte[] bytes = new byte[1024];
            int n = 0; // 读取的有效字节长度
            while ((n = inputStream.read(bytes)) != -1) {
                System.out.println(new String(bytes, 0, n));
            }

            // 获取客户端的网络字节输出流, 给客户端发送数据
            OutputStream outputStream = socket.getOutputStream();
            outputStream.write("收到, 你好客户端".getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

使用 TCP Socket 从客户端传输图片到服务器端并进行保存，服务器端回应客户端上传并保存成功，由于多个客户端会同时访问服务器，故在服务器端使用线程池开启多线程提高效率。

服务端程序：

```java
import java.io.*;
import java.net.*;
import java.util.Random;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class TCPServer {
    public static void main(String[] args) throws IOException {
        // 存储路径, 若路径不存在, 则创建
        String savePath = "D:\\TCPServer";
        File file = new File(savePath);
        if (!file.exists()) file.mkdirs();

        ServerSocket serverSocket = new ServerSocket(8998); // 服务端套接字
        // 使用线程池提高多客户端访问服务器的效率
        ExecutorService executorService = Executors.newFixedThreadPool(3);

        while (true) {
            executorService.submit(new Runnable() {
                @Override
                public void run() {
                    String fileName = savePath + "\\" + System.currentTimeMillis() + new Random(9999).nextInt() + ".jpg";
                    
                    try (Socket socket = serverSocket.accept();
                         FileOutputStream fos = new FileOutputStream(fileName);
                         InputStream inputStream = socket.getInputStream();
                         OutputStream outputStream = socket.getOutputStream()
                    ) {
                        // 读取客户端文件并保存在服务器
                        byte[] buffer = new byte[1024 * 8];
                        int n;
                        while ((n = inputStream.read(buffer)) != -1) {
                            fos.write(buffer, 0, n);
                        }
                        System.out.println("从 " + InetAddress.getLocalHost().getHostAddress() + " 接收数据完成");

                        // 回传给客户端确认数据
                        outputStream.write(("上传并保存成功").getBytes());
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            });
        }
    }
}
```

客户端程序：

```java
import java.io.*;
import java.net.Socket;

public class MyClient {
    public static void main(String[] args) {
        String filePath = "C:\\Users\\Administrator\\Desktop\\a.jpg";
        try (FileInputStream fis = new FileInputStream(filePath);
             Socket socket = new Socket("172.21.15.167", 8998);
             InputStream inputStream = socket.getInputStream();
             OutputStream outputStream = socket.getOutputStream()
        ) {
            byte[] buffer = new byte[1024 * 8];
            int n;
            while ((n = fis.read(buffer)) != -1) { // 读取本地文件并上传
                outputStream.write(buffer, 0, n);
            }
            socket.shutdownOutput(); // 后跟 TCP 的正常连接终止序列

            while ((n = inputStream.read(buffer)) != -1) { // 接收服务器回传的数据
                System.out.println(new String(buffer, 0, n));
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 函数式接口

#### 函数式接口与Lambda表达式

函数式接口在Java中指的是：**有且仅有一个抽象方法的接口**。当然接口中可以包含（默认方法、静态方法、私有方法）。`java.lang.Runnable` 接口就是一个函数式接口。

函数式接口，即适用于函数式编程场景的接口。而**Java中的函数式编程体现就是Lambda，所以函数式接口就是可**
**以适用于Lambda使用的接口**。只有确保接口中有且仅有一个抽象方法，Java中的Lambda才能顺利地进行推导。  

注解：`@FunctionlInterface` 注解可以检测接口是不是一个函数式接口。

函数式接口的使用：一般可以作为方法的**参数类型**或者**返回值类型**。

如果一个成员方法的参数**是一个函数式接口**，那么该接口可以接受一个Lambda表达式作为其参数。

Lambda表达式：有些场景的代码执行后，有些结果不一定会被使用，从而造成性能浪费。而**Lambda表达式是延迟执行的**，这正好可以
作为解决方案，提升性能。（lambda表达式相当于一个方法 / 函数，只有在程序使用这个方法 / 函数时，才会执行lambda表达式，即所谓的延迟执行。）

#### 常用的函数式接口

JDK提供了大量常用的函数式接口以丰富Lambda的典型使用场景，它们主要在 `java.util.function` 包中被提供。  

`java.util.function.Supplier<T>` 接口仅包含一个无参的方法： `T get()` 。用来获取一个泛型参数指定类型的对
象数据。由于这是一个函数式接口，这也就意味着对应的 Lambda 表达式需要“对外提供”一个符合泛型类型的对象
数据。  

`java.util.function.Consumer<T>` 接口则正好与 `Supplier<T>` 接口相反，它不是生产一个数据，而是消费一个数据，
其数据类型由泛型决定。  `Consumer` 接口中包含抽象方法 `void accept(T t) `，意为消费一个指定泛型的数据。  

```java
import java.util.function.Supplier;

public class Demo {
    private static String getString(Supplier<String> supp) {
        return supp.get();
    }
    public static void main(String[] args) {
        String msgA = "Hello";
        String msgB = "World";
        System.out.println(getString(() ‐> msgA + msgB));
    }
}
```

### Stream流

使用 Stream 流的方式，遍历集合、对集合中的数据进行过滤；Stream 关注的是做什么，而不是怎么做。

```java
public class Main2 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.stream() // 使用stream过滤掉不是以张开头的 && 且长度不是3的名字, 然后输出过滤后的结果
                .filter((name) -> name.startsWith("张"))
                .filter(name -> name.length() == 3)
                .forEach((name) -> System.out.println(name));
        list.stream();
    }
}
```

`java.util.Stream.Stream<T>` 是 Java 8 新加入的最常用的流接口。获取Stream流的两种方式：其一，即所有 Collection 集合都可以使用默认方法 `default Stream<E> stream()` 获取流（即上述程序的 `list.stream()`）；其二，使用 Stream 类的静态成员方法 `static <T> Stream<T> of(T ...values)` 获取流对象，参数为可变参数（即 `Stream.of(nums)`）。



流的常用 API 可以被分为两类：

- **延迟方法**：返回值类型仍然是 `Stream` 接口自身类型的方法，因此支持**链式调用**。除了终结方法外，其余方
  法均为延迟方法。常用延迟方法有：`filter`（按条件过滤集合），`map`（将某一类型映射的输入为另一个类型的输出），`limit`（取前n个对象），`skip`（跳过前n个对象）。
- **终结方法**：返回值类型不再是 `Stream` 接口自身类型的方法，因此不再支持类似 StringBuilder 那样的链式调
  用。本小节中，终结方法包括 `count` 和 `forEach` 方法。

Stream流属于管道流，只能被消费（使用）一次。第一个Stream流调用完毕方法，数据就会流转到下一个Stream流上，而这时第一个Stream流已经被消费完毕，就会关闭，第一个Stream流就不能再次调用方法了。

```java
public class Main2 {
    public static void main(String[] args) {
        List<String> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        Stream<String> stream1 = list1.stream();
        Stream<String> stream2 = list2.stream();
        stream1.forEach((name) -> System.out.println(name)); // 可以消费
//        stream1.forEach((name) -> System.out.println(name)); // 不再能被消费  
    }
}
```

Stream流的静态方法 `concat()`可以用于将两个流组合为一个新的流。

```java
public class Main2 {
    public static void main(String[] args) {
        List<String> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        Stream<String> stream1 = list1.stream();
        Stream<String> stream2 = list2.stream();
        Stream<String> stream3 = Stream.concat(stream1, stream2); // 组合两个流
    }
}
```

------

### 单元测试

**测试分类**：

1. 黑盒测试：不需要写代码，给输入值，看程序是否能够输出期望的值。
2. 白盒测试：需要写代码的。关注程序具体的执行流程。

**Junit使用：白盒测试**：

* 步骤：
	1. 定义一个测试类(测试用例)
		* 建议：
			* 测试类名：被测试的类名Test		`CalculatorTest`
			* 包名：xxx.xxx.xx.test		`cn.itcast.test`

	2. 定义测试方法：可以独立运行
		* 建议：
			* 方法名：test测试的方法名		`testAdd()`
			* 返回值：void
			* 参数列表：空参

	3. 给方法加注解 `@Test`
	4. 导入 `junit` 依赖环境

* 判定结果：
	* 红色：失败
	* 绿色：成功
	* 一般我们会使用**断言操作**来处理结果
		* `Assert.assertEquals(期望的结果, 运算的结果);`

* 补充：
  * `@Before`：修饰的方法会在测试方法之前被自动执行。
  * `@After`：修饰的方法会在测试方法执行之后自动被执行。

------

### 反射

**反射：将类的各个组成部分封装为其他对象，这就是反射机制**。好处：

1. 可以在程序运行过程中，操作这些对象。
2. 可以解耦，提高程序的可扩展性。

#### Java代码在计算机中经历的三个阶段

![image-20201014163551458](JAVA notes.assets/image-20201014163551458.png)

#### 获取Class对象的方式

1. `Class.forName("全类名")`：将字节码文件加载进内存，返回Class对象。
	* 多用于配置文件，将类名定义在配置文件中。读取文件，加载类。
2. `类名.class`：通过类名的属性class获取。
	* 多用于参数的传递。
3. `对象.getClass()`：getClass()方法在Object类中定义着。
	* 多用于对象获取字节码的方式

* 结论：同一个字节码文件(*.class)在一次程序运行过程中，只会被加载一次，**不论通过哪一种方式获取的Class对象都是同一个（同一个即地址相同）**。

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Main main = new Main();
        System.out.println(main.getClass()); // class com.company.Main
        System.out.println(Main.class); // class com.company.Main
        System.out.println(Class.forName("com.company.Main")); // class com.company.Main
    }
}
```

#### Class类对象的获取功能

- 获取成员变量**们**：
  - `Field[] getFields()` ：获取**所有`public`修饰的**成员变量。
  - `Field getField(String name)`   获取**指定名称** `name` 且被 `public` 修饰的成员变量。
  - `Field[] getDeclaredFields()`  获取**所有的**成员变量，不考虑修饰符。
  - `Field getDeclaredField(String name)`  获取**指定名称** `name` 且不考虑修饰的成员变量。

- 获取构造方法们：
  - `Constructor<?>[] getConstructors()`  
  - `Constructor<T> getConstructor(类<?>... parameterTypes)`  

  - `Constructor<T> getDeclaredConstructor(类<?>... parameterTypes)`  
  - `Constructor<?>[] getDeclaredConstructors()`  

- 获取成员方法们：
  - `Method[] getMethods()`  
  - `Method getMethod(String name, Class<?>... parameterTypes)`  

  - `Method[] getDeclaredMethods()`  
  - `Method getDeclaredMethod(String name, Class<?>... parameterTypes)`  

- 获取全类名：	
  - `String getName()`  

------

#### Field：成员变量的操作

1. 设置值：`void set(Object obj, Object value)`  
2. 获取值：`get(Object obj)` 
3. 忽略访问权限修饰符的安全检查：暴力反射 `setAccessible(true)`

------

#### Constructor：构造方法的操作

* 创建对象：`T newInstance(Object... initargs)`  
  * 如果使用空参数构造方法创建对象，操作可以简化：直接使用Class类对象中的`newInstance()`方法。

------

#### Method：方法对象的操作

* 执行方法：`Object invoke(Object obj, Object... args)`  

* 获取方法名称：`String getName`

------

#### 实例演示

定义一个`Person`类：

```java
package com.company;

public class Person {
    private int age = 10;
    private String name = "小三";

    public int a = 20;
    protected int b = 30;
    int c = 40;
    private int d = 50;

    public Person() {
    }

    public Person(int age, String name, int a, int b, int c, int d) {
        this.age = age;
        this.name = name;
        this.a = a;
        this.b = b;
        this.c = c;
        this.d = d;
    }

    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                ", name='" + name + '\'' +
                ", a=" + a +
                ", b=" + b +
                ", c=" + c +
                ", d=" + d +
                '}';
    }

    public void eat() {
        System.out.println("eat...");
    }

    private void eat(String what) {
        System.out.println("eat..." + what);
    }
}
```

**Class类对象**获取成员变量：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Class<Person> personClass = Person.class; // class类对象

        // 获取所有public修饰的成员变量
        Field[] fields = personClass.getFields();
        for (Field field : fields) {
            System.out.println(field); // public int com.company.Person.a
        }

        // 获取指定名称且被public修饰的成员变量
        Field a = personClass.getField("a");
        System.out.println(a); // public int com.company.Person.a

        // 获取所有的成员变量，不考虑修饰符
        Field[] declaredFields = personClass.getDeclaredFields();
        for (Field declaredField : declaredFields) {
            System.out.println(declaredField);
//            private int com.company.Person.age
//            private java.lang.String com.company.Person.name
//            public int com.company.Person.a
//            ...
        
        //获取变量值 && 设置变量值
        Person person = new Person();
        a.set(person, 1234);
        System.out.println(a); // public int com.company.Person.a
        int value = (int) a.get(person);
        System.out.println(value); // 1234
        }
    }
}
```

**Class类对象**获取构造方法：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Class<Person> personClass = Person.class; // class类对象

        // 获取全部的构造方法
        Constructor<Person>[] constructors = (Constructor<Person>[]) personClass.getConstructors();
        for (Constructor<Person> constructor : constructors) {
            System.out.println(constructor);
//            public com.company.Person()
//            public com.company.Person(int,java.lang.String,int,int,int,int)
        }

        // 获取无参构造方法
        Constructor<Person> constructor = personClass.getConstructor();
        System.out.println(constructor); // public com.company.Person()

        // 获取指定类型的构造方法
        Constructor<Person> constructor2 = personClass.getConstructor(int.class, String.class, int.class, int.class, int.class, int.class);
        System.out.println(constructor2); // public com.company.Person(int,java.lang.String,int,int,int,int)

        // 创建对象
        Person person = constructor2.newInstance(100, "小四", 200, 300, 400, 500);
        System.out.println(person); // Person{age=100, name='小四', a=200, b=300, c=400, d=500}
    }
}
```

**Class类对象**获取成员方法：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Class<Person> personClass = Person.class; // class类对象
		
        // 获取的方法包括Object类下的方法
        Method[] methods = personClass.getMethods();
        for (Method method : methods) {
            System.out.println(method); // public void com.company.Person.eat()
            System.out.println(method.getName()); // eat
        }

        // 执行方法
        Person person = new Person();
        Method eatMethod = personClass.getMethod("eat");
        eatMethod.invoke(person); // 执行并输出 eat...
        person.eat(); // 执行并输出 eat...
    }
}
```

---

#### 反射思想实例

**反射：将类的各个组成部分封装为其他对象，这就是反射机制**。思想的案例演示：

> 	* 需求：写一个"框架"，不改变该类的任何代码的前提下，可以帮我们创建任意类的对象，并且执行其中任意方法。
> 		* 实现：
> 			1. 配置文件  (pro.properties)
> 			2. 反射 (定义的Main类)
> 		* 步骤：
> 			1. 将需要创建的对象的全类名和需要执行的方法定义在配置文件中
> 			2. 在程序中加载读取配置文件
> 			3. 使用反射技术来加载类文件进内存
> 			4. 创建对象
> 			5. 执行方法

配置文件的定义：

```
# 文件 pro.properties

className=com.company.Person
methodName=sleep
```

反射类“框架”：

```java
package com.company;

import java.io.InputStream;
import java.lang.reflect.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        // 创建Properties对象
        Properties properties = new Properties();

        // 加载配置文件, 转换为一个集合
        ClassLoader classLoader = Person.class.getClassLoader();
        InputStream is = classLoader.getResourceAsStream("pro.properties");
        properties.load(is);

        // 获取配置文件中定义的数据(类名, 方法名)
        String className = properties.getProperty("className");
        String methodName = properties.getProperty("methodName");

        Class cls = Class.forName(className); // 创建Class类对象
        Object obj = cls.getDeclaredConstructor().newInstance(); // 创建该类的对象obj
        Method method = cls.getMethod(methodName); // 获取Class类的方法对象
        method.invoke(obj); //执行obj类内特定的方法
    }
}
```

---

### 注解

#### 注解的概念

注解（Annotation）定义：也叫元数据。一种代码级别的说明。它是JDK1.5及以后版本引入的一个特性，**与类、接口、枚举是在同一个层次**。它可以声明在包、类、字段、方法、局部变量、方法参数等的前面，用来对这些元素进行说明，注释。

注解：说明程序的，给计算机看的。注释：用文字描述程序的，给程序员看的。

使用注解：`@注解名称` 。

注解的作用分类：

- 编写文档：通过代码里标识的注解生成文档【生成文档doc文档】
- 代码分析：通过代码里标识的注解对代码进行分析【使用反射】
- 编译检查：通过代码里标识的注解让编译器能够实现基本的编译检查【如Override】

#### JDK预定义的注解

JDK中预定义的一些注解：
* `@Override`：检测被该注解标注的方法是否是继承自父类(接口)的。
* `@Deprecated`：该注解标注的内容，为已过时的，但仍可以使用。
* `@SuppressWarnings`：压制警告。一般传递参数`all`，即 `@SuppressWarnings("all")`。

#### 自定义注解

* 格式：
	
	```java
	元注解
	public @interface 注解名称{
	属性列表;
	}
	```
	
* **本质：注解本质上就是一个接口，该接口默认继承Annotation接口**。
	
* `public interface MyAnno extends java.lang.annotation.Annotation { // 属性 }`
	
* **属性：即接口中的抽象方法**。属性中一些必要的要求：

  1. 属性的返回值类型仅限于以下类型：
  	* 基本数据类型，String，枚举，注解，前面的类型的数组类型。
  	
  2. 定义了属性，在使用时需要给属性赋值：
    - 如果定义属性时，使用`default`关键字给属性默认初始化值，则使用注解时，可以不进行该属性的赋值。

    - 如果只有一个属性需要赋值，并且属性的名称是`value`，则`value`可以省略，直接定义值即可。

    - 数组赋值时，值使用`{ }`包裹。如果数组中只有一个值，则`{ }`可以省略。

#### 元注解

元注解：用于描述注解的注解。

* `@Target`：描述注解能够作用的位置。
	* `ElementType`取值：
		* `TYPE`：可以作用于类上
		* `METHOD`：可以作用于方法上
		* `FIELD`：可以作用于成员变量上
* `@Retention`：描述注解被保留的阶段。
	* `@Retention(RetentionPolicy.RUNTIME)`：当前被描述的注解，会保留到class字节码文件中，并被JVM读取到。
	* `@Retention(RetentionPolicy.CLASS)`：当前被描述的注解，会保留到class字节码文件中。
	* `@Retention(RetentionPolicy.SOURCE)`：当前被描述的注解，不会保留到class字节码文件中。
* `@Documented`：描述注解是否被抽取到api文档中。
* `@Inherited`：描述注解是否被子类继承。

#### 程序中解析注解

在程序使用（解析）注解：获取注解中定义的属性值
1. 获取注解定义位置的对象（Class、Method、Field）。

2. 获取指定的注解：通过本类的字节码文件对象调用 `getAnnotation(Class)`方法获取指定 `Class` 类字节码对象的注解。
  * `getAnnotation(Class)  // 其实就是在内存中生成了一个该注解(注解的本质即接口)的子类实现类对象。`

  ```java
    public class ProImpl implements Pro { // 获取指定的注解的本质
        @Override
        public String getClassName() {
            return "com.company.Person" //返回注解中的属性值
        }
    
        @Override
        public String getMethodName() {
            return "eat" //返回注解中的属性值
        }
    }
  ```

3. 调用注解中的抽象方法（即属性）获取配置的属性值。

---

在程序中使用（解析）注解的演示：

```java
package com.company;

import java.lang.reflect.*;

// 注: Person类即反射章节中定义的Person类
@Pro(getClassName = "com.company.Person", getMethodName = "eat")
public class Main {
    public static void main(String[] args) throws Exception {
        Class<Main> mainClass = Main.class; // 获取该类的字节码文件

        /* 通过本类的字节码文件对象 mainClass 调用 `getAnnotation(Class)` 方法获取指定 `Class` 类的注解 */
        // 下面一行的本质就是在内存中生成该Main类的注解(注解本质即接口)的子类实现类对象
        Pro annotation = mainClass.getAnnotation(Pro.class); // 接口Pro = 实现类
        /* 即:
          public class ProImpl implements Pro{
            @Override
            public String getClassName(){
                return "com.company.Person" //返回注解中的属性值
            }
            @Override
            public String getMethodName(){
                return "eat" //返回注解中的属性值
            }
          }
         */

        String className = annotation.getClassName();
        String methodName = annotation.getMethodName();
        System.out.println(className); // com.company.Person
        System.out.println(methodName); // eat

        Class cls = Class.forName(className); // 创建Class类对象
        Object obj = cls.getDeclaredConstructor().newInstance(); // 创建该类的对象obj
        Method method = cls.getMethod(methodName); // 获取Class类的方法对象
        method.invoke(obj); //执行obj类内特定的方法
    }
}
```

#### 简单的测试框架

使用注解对测试方法的测试结果进行日志记录，输出有bug的方法的异常信息到控制台。

注解文件定义：

```java
package com.company;

import java.lang.annotation.*;

@Target(ElementType.METHOD) // 可以作用于方法上
@Retention(RetentionPolicy.RUNTIME)
public @interface Check {
}
```

测试类及主方法定义：

```java
package com.company;

import java.lang.reflect.Method;

public class Main2 {
    public Main2() {

    }

    public static void main(String[] args) throws Exception {
        Class<Main2> main2Class = Main2.class;
        Class<Check> checkClass = Check.class;
        Method[] methods = main2Class.getMethods();
        for (Method method : methods) {
            if (method.isAnnotationPresent(checkClass)) { // 仅执行带有@Chech注解的成员方法
                try {
                    method.invoke(main2Class.getDeclaredConstructor().newInstance());
                } catch (Exception e) {
                    System.out.println(method + " 方法出现了异常；");
                    System.out.println("异常的原因是：" + e.getCause().getClass().getSimpleName());
                    System.out.println("异常的名称是：" + e.getCause().getMessage());
                } finally {
                    System.out.println("------------------");
                }
            }
        }
    }

    @Check
    public void add() {
        System.out.println("1 + 2 = " + (1 + 2));
    }

    @Check
    public void demo() {
        String s = null;
        System.out.println(s.equals("hhh"));
    }

    @Check
    public void div() {
        System.out.println("1 / 0 = " + (1 / 0));
    }

    public void demo2() {
        System.out.println("hhh, 我执行了吗？");
    }
}


/*
1 + 2 = 3
------------------
public void com.company.Main2.div() 方法出现了异常；
异常的原因是：ArithmeticException
异常的名称是：/ by zero
------------------
public void com.company.Main2.demo() 方法出现了异常；
异常的原因是：NullPointerException
异常的名称是：null
------------------
*/
```

小结：注解不是程序的一部分，可以理解为注解就是一个标签。注解是给编译器使用的，用来解析程序。

---










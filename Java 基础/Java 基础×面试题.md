## Java基础 × 面试题

### 什么是面向对象？

面向对象思想是一种试图降低代码间的依赖（如静态变量），应对复杂性，从而解决代码重用的软件设计思想。

OOP具有以下优点：

- 代码开发模块化，更易于维护和修改
- 代码复用性强
- 增强代码的可靠性和灵活性
- 增加代码的可读性

### 面向对象的特征有哪些？

#### 封装

封装，给对象提供了隐藏内部特性和行为的能力，不需要让外部知道具体实现细节。在java中，4种访问修饰符：`public`、`protected`、`default`、`private`限制访问权限。

封装的好处：

- 通过隐藏对象的属性来保护对象内部的状态
- 提高了代码的可用性和可维护性，因为对象的行为可以被单独的改变或者是扩展
- 禁止对象之间的不良交互提高模块化

#### 继承

继承，给对象提供了从基类获取字段和方法的能力。继承提供了代码的重用性，也可以再不修改类的情况下给现存的类添加新特性。

#### 多态

多态，是编程语言给不同的底层数据类型做相同的接口展示的一种能力。一个多态类型上的操作，可以应用到其他类型的值上面。**事物在运行过程中存在不同的状态。**

> 父类引用指向子类对象，调用方法时会调用子类的实现，而不是父类的实现，这叫多态。

- 静态多态性
    - 编译时的多态性 `重载`
- 动态多态性
    - 运行时的多态性 `重写`
        - 只有`非静态`的成员方法，在编译时绑定父类，在运行时绑定子类。
- 静态绑定
    - 在编译时绑定
    - 方法只有final，static，private和构造方法是编译绑定
- 动态绑定
    - 在运行状态时根据具体对象的类型进行绑定
        - 父类保存子类对象
        - 接口保存现实类对象
    - 动态绑定的过程
        - 虚拟机提取对象的实际类型的方法表；
        - 虚拟机搜索方法签名；
        - 调用方法
- 缺点
    - 不能使用子类特有的成员属性和子类特有的成员方法

#### 抽象

抽象，是把想法从具体的实例中分离出来的步骤，因此，要根据他们的功能而不是实现细节来创建类。

- 把类的行为和实现细节分离

**🦅抽象类和接口有什么区别**？

从设计层面来说，抽象是对类的抽象，是一种模板设计，接口是行为的抽象，是一种行为的规范。

- Java 提供和支持创建抽象类和接口。它们的实现有共同点，不同点在于：接口中所有的方法都是抽象的，而抽象类则可以同时包含抽象和非抽象的方法。
- 类可以实现很多个接口，但是只能继承一个抽象类。类可以不实现抽象类和接口声明的所有方法，当然，在这种情况下，类也必须得声明成是抽象的。
- 抽象类可以在不提供接口方法实现的情况下实现接口。
- Java 接口中声明的变量默认都是 `final` 的。抽象类可以包含非 `final` 的变量。
- Java 接口中的成员函数默认是 `public` 的。抽象类的成员函数可以是 `private`，`protected` 或者是 `public` 。
- 接口是绝对抽象的，不可以被实例化。抽象类也不可以被实例化，但是，如果它包含 `#main(String[] args)` 方法的话是可以被调用的。

🦅**继承和组合的区别在哪？**

- 继承：指的是一个类（称为子类、子接口）继承另外的一个类（称为父类、父接口）的功能，并可以增加它自己的新功能的能力，继承是类与类或者接口与接口之间最常见的关系。在 Java 中，此类关系通过关键字 `extends` 明确标识，在设计时一般没有争议性。
- 组合：组合是关联关系的一种特例，他体现的是整体与部分、拥有的关系，即 has-a 的关系，此时整体与部分之间是可分离的，他们可以具有各自的生命周期，部分可以属于多个整体对象，也可以为多个整体对象共享。
    - 比如，计算机与 CPU 、公司与员工的关系等。
    - 表现在代码层面，和关联关系是一致的，只能从语义级别来区分。

### 面向对象和面向过程的区别？

#### 面向过程

- 优点：性能比面向对象高，因为类调用时需要实例化，开销比较大，比较消耗资源。比如，单片机、嵌入式开发、Linux/Unix 等一般采用面向过程开发，性能是最重要的因素。
- 缺点：没有面向对象易维护、易复用、易扩展。

#### 面向对象

- 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护。
- 缺点：性能比面向过程低。

### 重载和重写的区别？

#### 重写 `override`

- 方法名、参数、返回值相同。
- 子类方法不能缩小父类方法的访问权限。
- 子类方法不能抛出比父类方法更多的异常(但子类方法可以不抛出异常)。
- 存在于父类和子类之间。
- 方法被定义为 `final` 不能被重写。

#### 重载 `overload`

- 参数类型、个数、顺序至少有一个不相同。
- 不能重载只有返回值不同的方法名。
- 存在于父类和子类、同类中。

### 什么是构造方法？什么是构造方法重载？什么是拷贝构造方法？

**构造方法**

当新对象被创建的时候，构造方法会被调用。每一个类都有构造方法。如果程序员没有给类提供构造方法的，Java 编译器才会为这个类创建一个默认的构造方法。

**构造方法重载**

Java 中构造方法重载和方法重载很相似。可以为一个类创建多个构造方法。每一个构造方法必须有它自己唯一的参数列表。

**拷贝构造方法**

Java 不支持像 C++ 中那样的[拷贝构造方法](http://www.runoob.com/cplusplus/cpp-copy-constructor.html)，这个不同点是因为如果你不自己写构造方法的情况下，Java 不会创建默认的拷贝构造方法。

### JDK、JRE、JVM 分别是什么关系？

#### JDK

JDK 即为 Java 开发工具包，包含编写 Java 程序所必须的编译、运行等开发工具以及 JRE。开发工具如：

- 用于编译 Java 程序的 javac 命令。
- 用于启动 JVM 运行 Java 程序的 Java 命令。
- 用于生成文档的 Javadoc 命令。
- 用于打包的 jar 命令等等。

> 简单说，就是 JDK 包含 JRE 包含 JVM。

####  JRE

JRE 即为 Java 运行环境，提供了运行 Java 应用程序所必须的软件环境，包含有 Java 虚拟机（JVM）和丰富的系统类库。系统类库即为 Java 提前封装好的功能类，只需拿来直接使用即可，可以大大的提高开发效率。

> 简单说，就是 JRE 包含 JVM。

####  JVM

JVM 即为 Java 虚拟机，提供了字节码文件(`.class`)的运行环境支持。

#### 为什么 Java 被称作是“平台无关的编程语言”？

> 因为Java编译后的字节码文件由JVM执行，而JVM不能跨平台，由于 JVM 屏蔽了与各个计算机平台相关的软件或者硬件之间的差异，使得与平台相关的耦合统一由 JVM 提供者来实现。

Java 虚拟机是一个可以执行 Java 字节码的虚拟机进程。

- Java 源文件( `.java` )被编译成能被 Java 虚拟机执行的字节码文件( `.class` )。
- Java 被设计成允许应用程序可以运行在任意的平台，而不需要程序员为每一个平台单独重写或者是重新编译。Java 虚拟机让这个变为可能，因为它知道底层硬件平台的指令长度和其他特性。

### 什么是字节码？采用字节码的最大好处是什么？

#### 字节码

Java 中引入了虚拟机的概念，即在机器和编译程序之间加入了一层抽象的虚拟的机器。这台虚拟的机器在任何平台上都提供给编译程序一个的共同的接口。

编译程序只需要面向虚拟机，生成虚拟机能够理解的代码，然后由解释器来将虚拟机代码转换为特定系统的机器码执行。**在 Java 中，这种供虚拟机理解的代码叫做字节码（即扩展名为 `.class` 的文件），它不面向任何特定的处理器，只面向虚拟机。**

每一种平台的解释器是不同的，但是实现的虚拟机是相同的。Java 源程序经过编译器编译后变成字节码，字节码由虚拟机解释执行，虚拟机将每一条要执行的字节码送给解释器，解释器将其翻译成特定机器上的机器码，然后在特定的机器上运行。**这也就是解释了 Java 的编译与解释并存的特点**。

> Java 源代码=> 编译器 => JVM 可执行的 Java 字节码(即虚拟指令)=> JVM => JVM 中解释器 => 机器可执行的二进制机器码 => 程序运行

#### 采用字节码的好处

Java 语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以 Java 程序运行时比较高效，而且，由于字节码并不专对一种特定的机器，因此，Java程序无须重新编译便可在多种不同的计算机上运行。

### 介绍一下Java的基本数据类型

**Java 中的几种基本数据类型是什么？各自占用多少字节？**

Java 支持的数据类型包括8种基本数据类型和引用类型。

**基本数据**类型如下：

- 整数值型：

    - `byte`：1 *byte*
    - `short`：2 *byte*
    - `int`：4 *byte*
    - `long`：8 *byte*

- 字符型：`char`：2 *byte*

- 浮点类型：`float`：4 *byte*；`double`：8 *byte*

- 布尔型：`boolean`：

    > JVM规范中，`boolean`变量当作`int`处理，也就是4字节；而`boolean数组`当做`byte数组`处理，即boolean类型的数组里面的每一个元素占1个字节。

- 整数型：默认 `int` 型，小数默认是 `double` 型。Float 和 Long 类型的必须加后缀。比如：`float f = 100f` 

> void也是Java的基本类型之一，其对应的包装类是不可实例化的，

**引用类型**声明的变量是指该变量在内存中实际存储的是一个引用地址，实体在堆中。

- 引用类型包括类、接口、数组等。
- 特别注意，String 是引用类型不是基本类型。

🦅 **什么是自动拆装箱？**

自动装箱和拆箱，就是基本类型和引用类型之间的转换。

> Java 5中集合的容器要求元素是Object类型，无法将int、double之类基础数据类型放置进去，而包装类让基本数据类型有对象的性质

- 装箱：调用 *.valueOf(*) 方法；
- 拆箱：调用 *.xxxValue()* 方法；
- 缓存范围：
    - `Interger`、`Byte`, `Short`, `Long`： -128 - 127
    - `Character`： 0 - 127
    - `Integer`的缓存范围可改变

🦅 **char 型变量中能不能存贮一个中文汉字？为什么？**

- 在 C 语言中，char 类型占 1 个字节，而汉字占 2 个字节，所以不能存储。
- 在 Java 语言中，char 类型占 2 个字节，而且 Java 默认采用 Unicode 编码，一个 Unicode 码是 16 位，所以一个 Unicode 码占两个字节，Java 中无论汉字还是英文字母，都是用 Unicode 编码来表示的。所以，在 Java 中，char 类型变量可以存储一个中文汉字。

### switch的参数

- 基本数据类型：byte, short, char, int

    > char，byte和short类型可以自己转化（宽化）为int类型，最后操作的还是int类型

- 枚举类型：Enum  `JDK 5`

- 字符串类型：String `JDK 7`

    > 通过`equals()`和`hashCode()`方法来实现的，先case判定hash值，再equals对比；

### 什么是值传递和引用传递？

- 值传递，是对基本型变量而言的，传递的是该变量的一个副本，改变副本不影响原变量。
- 引用传递，一般是对于对象型变量而言的，传递的是该对象地址的一个副本，并不是原对象本身。

一般认为，Java 内的传递都是值传递，Java 中实例对象的传递是引用传递（实际是引用地址值的拷贝）。

### 是否可以在 static 环境中访问非 static 变量？

`static` 变量在 Java 中是属于类的，它在所有的实例中的值是一样的。当类被 Java 虚拟机载入的时候，会对 `static` 变量进行初始化。

如果你的代码尝试不用实例来访问非 `static` 的变量，编译器会报错，因为这些变量还没有被创建出来，还没有跟任何实例关联上。

### String

🦅 **String、StringBuffer、StringBuilder 的区别？**

Java 平台提供了两种类型的字符串：String 和 StringBuffer/StringBuilder，它们可以储存和操作字符串。

- String ，是只读字符串，也就意味着 String 引用的字符串内容是不能被改变的。

    > 每次对 String 类型进行改变的时候，都会生成一个新的 String 对象，然后将指针指向新的 String 对象。

- StringBuffer/StringBuilder 类，表示的字符串对象可以直接进行修改。StringBuilder 是 Java 5 中引入的，它和 StringBuffer 的方法完全相同，区别在于它是在单线程环境下使用的，因为它的所有方面都没有被 `synchronized` 修饰，因此它的效率也比 StringBuffer 要高。

    > StringBuffer 每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象并改变对象引用。
    >
    > 相同情况下使用 StirngBuilder 相比使用 StringBuffer 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

🦅 **对于三者使用的总结？**

- 操作少量的数据 = String 。

    > 这个也是实际编码较为经常使用的方式。

- 单线程操作字符串缓冲区下操作大量数据 = StringBuilder 。

    > 甚至有时，我们为了避免每个线程重复创建 StringBuilder 对象，会通过 ThreadLocal + StringBuilder 的方式，进行对 StringBuilder 的重用。具体可以参考 [《StringBuilder 在高性能场景下的正确用法》](http://nathanchen.github.io/14596982516208.html) 文章。

- 多线程操作字符串缓冲区下操作大量数据 = StringBuffer

    > 实际场景下，我们基本不太会出现，多线程操作同一个 StringBuffer 对象。


**🦅 String s = new String("xyz") 在运行时涉及几个String实例？**

两个，一个是**字符串字面量**"xyz"所对应的、驻留（intern）在一个全局共享的**字符串常量池**中的实例，另一个是通过new String(String)创建并初始化的、内容与"xyz"相同的实例

- 首先，在 String 池内找，找到 `"xyz"` 字符串，不创建 `"xyz"` 对应的 String 对象，否则创建一个对象。
- 然后，遇到 `new` 关键字，在内存上创建 String 对象，并将其返回给 `s` ，又一个对象。

🦅 **String 为什么是不可变的？**

简单的来说，String 类中使用 `final` 关键字字符数组保存字符串。代码如下：

```java
// String.java
private final char[] value;
```

- 所以 String 对象是不可变的。

而 StringBuilder 与 StringBuffer 都继承自 AbstractStringBuilder 类，在 AbstractStringBuilder 中也是使用字符数组保存字符串 `char[] value` ，但是没有用 `final` 关键字修饰。代码如下：

```java
// AbstractStringBuilder.java
char[] value;
```

- 所以这两种对象都是可变的。

🦅 **String 类能被继承吗，为什么？**

不能，因为 String 是 `final` 修饰。

🦅 **StringTokenizer 是什么？**

StringTokenizer ，是一个用来分割字符串的工具类。

### equals 与 == 的区别？

- 基本数据类型：都是用 `== `判断相等性。
- 对象引用：
    - `== `判断引用所指的对象是否是同一个。
    - *equals* 方法，是 *Object* 的成员函数，有些类会覆盖`(override)` 这个方法，用于判断对象的等价性。
        - *String* 中 *equals* 方法判断值是否相等

🦅 **说一说你对 java.lang.Object 对象中 hashCode 和 equals 方法的理解。在什么场景下需要重新实现这两个方法？**

父类的 equals ，一般情况下是无法满足子类的 equals 的需求。

- 比如所有的对象都继承 Object ，默认使用的是 Object 的 equals 方法，在比较两个对象的时候，是看他们是否指向同一个地址。但是我们的需求是对象的某个属性相同，就相等了，而默认的 equals 方法满足不了当前的需求，所以我们要重写 equals 方法。
- 如果重写了 equals 方法，就必须重写 hashCode 方法，否则就会降低 Map 等集合的索引速度。

*equals* 方法，一般用于比较对象的内容是否相等。

> 当覆盖了 equals 方法时，比较对象是否相等将通过覆盖后的 equals 方法进行比较（判断对象的内容是否相等）。

*hashCode* 方法，大多在集合中用到。

> 将对象放入到集合中时，首先判断要放入对象的 hashCode 值与集合中的任意一个元素的 hashCode 值是否相等，如果不相等直接将该对象放入集合中。
>
> 如果 hashCode 值相等，然后再通过 equals 方法判断要放入对象与集合中的任意一个对象是否相等，如果 equals 判断不相等，直接将该元素放入到集合中，否则不放入。

🦅 **有没有可能 2 个不相等的对象有相同的 hashCode？**

可能会发生，这个被称为**哈希碰撞**。当然，相等的对象，即我们重写了 equals 方法，一定也要重写 hashCode 方法，否则将出现我们在 HashMap 中，相等的对象作为 key ，将找不到对应的 value 。

所以说，equals 和 hashCode 的关系会是：

- equals 不相等，hashCode 可能相等。
- equals 相等，请重写 hashCode 方法，保证 hashCode 相等。

### final、finally、finalize 的区别？

#### final

`final` ，是修饰符关键字。

**1. 类**

声明类不允许被继承。因此一个类不能既被声明为 `abstract` 的，又被声明为 `final` 的。

**2. 数据**

声明数据为常量，可以是编译时常量，也可以是在运行时被初始化后不能被改变的常量。

- 对于基本类型，`final` 使数值不变，必须在声明时给定初值；
- 对于引用类型，`final` 使引用不变，也就不能引用其它对象，但是被引用的对象本身是可以修改的。

**3. 方法**

声明方法不能被子类重写。

***private* 方法隐式地被指定为 `final**`，如果在子类中定义的方法和基类中的一个 *private* 方法签名相同，此时子类的方法不是重写基类方法，而是在子类中定义了一个新的方法。

#### finally

在异常处理时提供 `finally` 块来执行任何清除操作。如果抛出一个异常，那么相匹配的 `catch` 子句就会执行，然后控制就会进入 `finally` 块（如果有的话）。

在以下 4 种特殊情况下，finally块不会被执行：

- 在 `finally` 语句块中发生了异常。
- 在前面的代码中用了 `System.exit()` 退出程序。
- 程序所在的线程死亡。
- 关闭 CPU 。

#### finalize

`finalize` ，是方法名。

Java 允许使用 `finalize()` 方法，在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的。

- 它是在 Object 类中定义的，因此所有的类都继承了它。
- 子类覆盖 `finalize()` 方法，以整理系统资源或者执行其他清理工作。
- `finalize()` 方法，是在垃圾收集器删除对象之前对这个对象调用的。

### 讲讲类的实例化顺序？

初始化顺序如下：

- 父类静态变量
- 父类静态代码块
- 子类静态变量
- 子类静态代码块
- 父类非静态变量（父类实例成员变量）
- 父类构造函数
- 子类非静态变量（子类实例成员变量）
- 子类构造函数

### 什么是内部类？

简单的说，就是在一个类、接口或者方法的内部创建另一个类。

🦅 **内部类的作用是什么？**

内部类提供了更好的封装，除了该外围类，其他类都不能访问。

🦅 **Anonymous Inner Class(匿名内部类)是否可以继承其它类？是否可以实现接口？**

可以继承其他类或实现其他接口，在 Java 集合的流式操作中，我们常常这么干。

🦅 **内部类可以引用它的包含类（外部类）的成员吗？有没有什么限制？**

一个内部类对象可以访问创建它的外部类对象的成员，包括私有成员。

### 什么是 Java IO ？

Java IO 相关的类，在 `java.io` 包下，具体操作分成面向字节(Byte)和面向字符(Character)两种方式。如下图所示：

![Java IO×字符×字节](..\Resources\Java IO×字符×字节.png)

![Java IO×操作对象](..\Resources\Java IO×操作对象.png)

#### IO流的分类

- 按照流的流向分，可以分为输入流和输出流；
- 按照操作单元划分，可以划分为字节流和字符流；
- 按照流的角色划分为节点流和处理流。

- **InputStream/Reader**: 所有的输入流的基类，前者是字节输入流，后者是字符输入流。
- **OutputStream/Writer**: 所有输出流的基类，前者是字节输出流，后者是字符输出流。

### 什么是 Java 序列化？

序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。

- 可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。
- 序列化是为了解决在对对象流进行读写操作时所引发的问题。

反序列化的过程，则是和序列化相反的过程。

> 另外，我们不能将序列化局限在 Java 对象转换成二进制数组，例如说，我们将一个 Java 对象，转换成 JSON 字符串，或者 XML 字符串，这也可以理解为是序列化。

🦅 **如何实现 Java 序列化？**

> 如下的方式，就是 Java 内置的序列化方案，实际场景下，我们可以自定义序列化的方案，例如说 Google Protobuf 。

将需要被序列化的类，实现 Serializable 接口，该接口没有需要实现的方法，`implements Serializable` 只是为了标注该对象是可被序列化的。

- 序列化
    - 然后，使用一个输出流(如：FileOutputStream)来构造一个 *ObjectOutputStream(*对象流)对象
    - 接着，使用 *ObjectOutputStream* 对象的 `#writeObject(Object obj)` 方法，就可以将参数为 `obj` 的对象写出(即保存其状态)。
- 反序列化
    - 要恢复的话则用输入流。

🦅 **Java 序列话中，如果有些字段不想进行序列化怎么办？**

对于不想进行序列化的变量，使用 `transient` 关键字修饰。

- 当对象被序列化时，阻止实例中那些用此关键字修饰的的变量序列化。
- 当对象被反序列化时，被 `transient` 修饰的变量值不会被持久化和恢复。
- `transient` 只能修饰变量，不能修饰类和方法。

### 如何实现对象克隆？

一般来说，有两种方式：

- 1、实现 *Cloneable* `标识接口`，并重写 *Object* 类中的 `#clone()` 方法。可以实现**浅克隆**，也可以实现**深克隆**。
- 2、实现 *Serializable* `标识接口`，通过对象的序列化和反序列化实现克隆。可以实现真正的**深克隆**。

### 说说异常的分类？

![Throwable](..\Resources\Throwable.png)

**error 和 exception 有什么区别？CheckedException 和 RuntimeException 有什么区别？**

- Error（错误），表示系统级的错误和程序不必处理的异常，是 Java 运行环境中的内部错误或者硬件问题。
    - 例如：内存资源不足等。
    - 对于这种错误，程序基本无能为力，除了退出运行外别无选择，它是由 Java 虚拟机抛出的。
- Exception（异常），表示需要捕捉或者需要程序进行处理的异常，它处理的是因为程序设计的瑕疵而引起的问题或者在外的输入等引起的一般性问题，是程序必须处理的。Exception 又分为运行时异常，受检查异常。
    - RuntimeException(运行时异常)，表示无法让程序恢复的异常，导致的原因通常是因为执行了错误的操作，建议终止逻辑，因此，编译器不检查这些异常。
    - CheckedException(受检查异常)，是表示程序可以处理的异常，也即表示程序可以修复（由程序自己接受异常并且做出处理），所以称之为受检查异常。

🦅 **异常的使用的注意地方？**

神作`Effective Java`中对异常的使用给出了以下指导原则：

- 不要将异常处理用于正常的控制流（设计良好的 API 不应该强迫它的调用者为了正常的控制流而使用异常）。
- 对可以恢复的情况使用受检异常，对编程错误使用运行时异常。
- 避免不必要的使用受检异常（可以通过一些状态检测手段来避免异常的发生）。
- 优先使用标准的异常。
- 每个方法抛出的异常都要有文档。
- 保持异常的原子性
- 不要在 `catch` 中忽略掉捕获到的异常。

🦅 **Throwable 类常用方法？**

- `#getMessage()` 方法：返回异常发生时的详细信息。
- `#getCause()` 方法：获得导致当前 Throwable 异常的 Throwable 异常。
- `#getStackTrace()`方法：获得 Throwable 对象封装的异常信息。
- `#printStackTrace()` 方法：在控制台上打印。

🦅 **请列出 5 个运行时异常？**

- 空指针引用：*NullPointerException*
- 下标越界：*IndexOutOfBoundsException*
- 类型强制转换：*ClassCastException*
- 数字转换：*NumberFormatException*
- 运算错误：*AirthmeticException*

🦅 **throw 与 throws 的区别 ？**

- `throw` ，用于在程序中显式地抛出一个异常。
- `throws` ，用于指出在该方法中没有处理的异常。**每个方法必须显式指明哪些异常没有处理，以便该方法的调用者可以预防可能发生的异常**。最后，多个异常用逗号分隔。

🦅 **异常处理中 finally 语句块的重要性?**

不管程序是否发生了异常, `finally` 语句块都会被执行，甚至当没有`catch` 声明但抛出了一个异常时, `finally` 语句块也会被执行。

`finally` 语句块通常用于释放资源, 如 I/O 缓冲区, 数据库连接等等。

🦅 **异常被处理后异常对象会发生什么?**

异常对象会在下次 GC 执行时被回收。

🦅 **UnsupportedOperationException 是什么？**

UnsupportedOperationException ，是用于表明操作不支持的异常。

在 JDK 类中已被大量运用，在集合框架`java.util.Collections.UnmodifiableCollection` 将会在所有 add 和 remove 操作中抛出这个异常。

### 说说反射的用途及实现？

Java 反射机制主要提供了以下功能：

- 在运行时构造一个类的对象。
- 判断一个类所具有的成员变量和方法。
- 调用一个对象的方法。
- 生成动态代理。

反射的应用很多，很多框架都有用到：

- Spring 框架的 IoC 基于反射创建对象和设置依赖属性。
- Spring MVC 的请求调用对应方法，也是通过反射。
- JDBC 的 `Class#forName(String className)` 方法，也是使用反射。

不了解 Java 反射的同学，可以看看 [《什么是反射、反射可以做些什么》](http://www.cnblogs.com/zhaopei/p/reflection.html) 。

> 对于大多数 Java 萌新，包括艿艿在内。不过后来发现，再难的 Java 知识，未来都需要变成我们的基础知识，嘻嘻。

🦅 **反射中，Class.forName 和 ClassLoader 区别？**

这两者，都可用来对类进行加载。差别在于：

- `Class#forName(...)` 方法，除了将类的 `.class` 文件加载到JVM 中之外，还会对类进行解释，执行类中的 `static` 块。

- ClassLoader 只干一件事情，就是将 `.class` 文件加载到 JVM 中，不会执行 `static` 中的内容，只有在 newInstance 才会去执行 `static` 块。

    > `Class#forName(name, initialize, loader)` 方法，带参函数也可控制是否加载 `static` 块，并且只有调用了newInstance 方法采用调用构造函数，创建类的对象。

详细的测试，可以看看 [《Java 反射中，Class.forName 和ClassLoader 的区别(代码说话)》](https://blog.csdn.net/qq_27093465/article/details/52262340) 文章。

### Java 对象创建的方式？

1. 使用 `new` 关键字创建对象。
2. 使用 Class 类的 newInstance 方法(反射机制)。
3. 使用 Constructor 类的 newInstance 方法(反射机制)。
4. 使用 clone 方法创建对象。
5. 使用(反)序列化机制创建对象。

## 参考

[知乎 × 如何用一句话说明什么是面向对象思想？](https://www.zhihu.com/question/19854505)
# Java 基础

> Java基于C++、Simula-67、SmallTalk等语言开发；

## 一、面向对象

> 面向对象程序设计：Object-Oriented Programming（OOP）

### 类和对象

- 类是对象的抽象，对象是类的具体
- 类是定义了对象的模板
- 类成为对象——实例化
    - 栈保存名字和堆地址
    
    - 堆保存分配后的对象数据
    
    - 通过栈的引用取到值，值为堆地址，因此可取得分配的对象
    
    - *new* 强制分配内存空间
    
    - 类成为对象
      
        - 类先被编译成字节码文件(.class)
            - 前4位 模数 检测是否是java的.class文件
            - 再后4位 版本号
        - 加载到JVM
            - 系统类加载
            - 扩展类加载
            - 自定义类加载
        - 连接
        - 初始化
        - 实例化

### 类

#### 变量

##### 属性（成员变量）

在类里，但在所有方法之外定义的变量，被所有方法共享的变量

- 类属性：静态变量&类名调用
- 实例属性：非静态变量&引用名调用
- 成员变量在声明时如果没有定义值，则JVM会默认赋值；但局部变量不会

    - Boolean false
    - Char '\u0000'(null)
    - byte (byte)0
    - short (short)0
    - int 0
    - long 0L
    - float 0.0f
    - double 0.0d
- 类变量在方法区的静态池，成员变量在堆内存，局部变量在栈内存

##### 局部变量

在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。

#### 方法

> [访问修饰符] {其他修饰符} <方法返回值的类型> <方法名> ([args]){}

- 在有返回值声明的方法中return的值的类型必须与声明类型一致
- 在void方法上，可以使用return；可以直接中断当然方法，继续执行

##### 访问修饰符

- private: 仅对本类可见
- protected: 对本包和所有子类可见
- public: 对所有类可见
- 默认: 对本包可见

##### 特殊方法

- 主方法(mian方法): 程序的入口，一个Class只能有一个
- 如果声明了一个带参数的构造方法，那么JVM不会再自动产生无参的构造器
- 代码域{}: 实例化以后才被加载
- 静态域static{}: 常用于初始化，类加载的时候进行加载

## 二、特性

### 封装

封装是面向对象的核心思想，将对象的属性和行为封装起来，不需要让外界知道具体实现细节，这就是封装思想。**开放功能使用，封闭实现的细节**

### 继承

继承性主要描述的是类与类之间的关系，通过继承，可以在无需重新编写原有类的情况下，对原有类的功能进行扩展。**Java为单根继承**

- 降低代码冗余 `实例方法`
- 规范子类行为 `抽象方法`
- 超类必须有无参构造器
- 依次递归调用上层的构造器
- *abstract*不能和*final*、*static*同时出现
- 重写（OverRide）时访问修饰符不可缩小

### 多态

可以把一个父对象设置为一个或者多个他的子对象的技术（一个对象的多种表现形态）

- 静态多态性
    - 编译时的多态性 `重载`
- 动态多态性
    - 运行时的多态性 `重写`
    - 动态绑定
        - 父类保存子类对象
        - 接口保存现实类对象

#### 动态绑定与静态绑定

> 绑定指的是一个方法的调用与方法所在的类(方法主体)关联起来。

##### 静态绑定：在程序执行前方法已经被绑定

java当中的方法只有final，static，private和构造方法是前期绑定

##### 动态绑定：在运行时根据具体对象的类型进行绑定。

动态绑定的过程：

- 虚拟机提取对象的实际类型的方法表；
- 虚拟机搜索方法签名；
- 调用方法

## 三、数据类型

### 内存

- 最小单位：byte字节
- 最小单元：bit位
- 1 byte = 8 bit

### 数据类型

#### 基本数据类型

- 整数
    - short : 2 byte
    - int : 4 byte
    - long : 8 byte
    - byte : 1 byte 不作数学运算
- 浮点数
   - float : 4 byte 单精度浮点
   - double : 8 byte 双精度浮点
- 非数字型
      - boolean： true / false
- 字符型
              - char : 2 byte 可以保存文字可以保存数字没有符号

#### 引用数据类型

- String
- 类
- 对象

### 运算

- 如果整数型保存浮点数类型，那么小数点后数据全部舍弃。
- 相对更大的类型与相对更小的类型运算，获得相对更大的类型
- 负数原码--反码--补码 **不要将负数交给没有符号位的数据类型保存**
- 当char 单独打印时会把所存放的数字当做ASCII码表的键，打印相应的值；
    但如果两个char值进行运算，无论是否为数字都会将两个char转成ASCII码
    中对应的数字进行运算

### 自动装箱与拆箱

- 集合的容器要求元素是Object类型，无法将int、double之类基础数据类型放置进去，而包装类让基本数据类型有对象的性质

- 装箱：将基本类型用它们对应的引用类型包装起来；调用.valueOf()方法；
- 拆箱：将包装类型转换为基本数据类型；调用xxxValue()方法；
- 包装类的缓存节省内存和提高性能；
- `Interger`、`Byte`, `Short`, `Long`的缓存范围: -128 到 127。对于`Character`, 范围是 0 到 127。除了`Integer`以外，这个范围都不能改变。

## 二进制码

### 机器数

一个数在计算机中的二进制表示形式,  叫做这个数的机器数。机器数是带符号的，在计算机用一个数的最高位存放符号, 正数为0, 负数为1.

```
比如，十进制中的数 +3 ，计算机字长为8位，转换成二进制就是00000011。如果是 -3 ，就是 10000011 。
```

### 真值

因为第一位是符号位，所以机器数的形式值就不等于真正的数值，将带符号位的机器数对应的真正数值称为机器数的真值。

```
例如上面的有符号数 10000011，其最高位1代表负，其真正数值是 -3 而不是形式值131（10000011转换成十进制等于131）
```

### 原码

原码就是符号位加上真值的绝对值, 即用第一位表示符号, 其余位表示值. 

- 原码不能进行减法运算

### 反码

- 正数的反码是其本身
- 负数的反码是在其原码的基础上, 符号位不变，其余各个位取反.
- 反码减法运算会存在±0，故进一步开发了补码			

### 补码

- 正数的补码就是其本身

- 负数的补码是在其原码的基础上, 符号位不变, 其余各位取反, 最后+1. (即在反码的基础上+1)

    - 负数以补码保存


### 移码

对真值补码的符号位取反

- 一般用作浮点数的阶码，引入的目的是便于浮点数运算时的对阶操作。

### 转换

- 长字节类型转化为短字节类型时，直接剪去超出的字节
- 短字节类型转化为长字节类型时
    - 正整数向少的bit位填充0
    - 负整数向少的bit位填充1

## IEEE754浮点数

> 以下Java代码为JDK 1.8的Float包装类源码

### 浮点数的存储格式

IEEE754标准中规定

- float单精度浮点数在机器中表示用 1 位表示数字的符号，用 8 位表示指数，用 23 位表示尾数，即小数部分。
- double双精度浮点数，用 1 位表示符号，用 11 位表示指数，52 位表示尾数，其中指数域称为阶码。
- IEEE754浮点数的格式如下图所示：

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/General_floating_point_frac.svg/490px-General_floating_point_frac.svg.png)

float的指数偏移值为$$2^7-1=127$$
double的指数偏移值为$$2^{10}-1=1023$$

IEEE754标准中，一个规格化32位的浮点数$$x$$的真值表示为：
$$
x=(-1)^S*(1.M)*2^e
$$
其中，S为符号值，M为尾数，e为真实指数值，即减去偏移值后的值。

### 指数位的特殊情况

##### 当指数位全为1时，即$[11111111]_2$

- 当尾数位全为0，则表示为±∞。

    ```java
        /**
         * A constant holding the positive infinity of type
         * {@code float}. It is equal to the value returned by
         * {@code Float.intBitsToFloat(0x7f800000)}.
         */
        public static final float POSITIVE_INFINITY = 1.0f / 0.0f;
    
        /**
         * A constant holding the negative infinity of type
         * {@code float}. It is equal to the value returned by
         * {@code Float.intBitsToFloat(0xff800000)}.
         */
        public static final float NEGATIVE_INFINITY = -1.0f / 0.0f;
    ```

- 当尾数位不全为0，则表示这不是一个数（NaN）。

    ```java
        /**
         * A constant holding a Not-a-Number (NaN) value of type
         * {@code float}.  It is equivalent to the value returned by
         * {@code Float.intBitsToFloat(0x7fc00000)}.
         */
        public static final float NaN = 0.0f / 0.0f;
    ```

- 所以最大指数值为$$[1111 1110] = 254 - 127 = 127$$ 

    ```java
        /**
         * Maximum exponent a finite {@code float} variable may have.  It
         * is equal to the value returned by {@code
         * Math.getExponent(Float.MAX_VALUE)}.
         *
         * @since 1.6
         */
        public static final int MAX_EXPONENT = 127;
    ```

    

##### 当指数位为0时，即$[00000000]_2$

- 真值表示为
    $$
    x=(-1)^S*(0.M)*2^{-126}
    $$
    例：
    $$
    [1 0000 0000 000 0000 0000 0000 0000 0001]_2 = (-1)^1*(0.000 0000 0000 0000 0000 0001)_2*2^{-126}=-2^{-149}
    $$

    ```java
        /**
         * A constant holding the smallest positive nonzero value of type
         * {@code float}, 2<sup>-149</sup>. It is equal to the
         * hexadecimal floating-point literal {@code 0x0.000002P-126f}
         * and also equal to {@code Float.intBitsToFloat(0x1)}.
         */
        public static final float MIN_VALUE = 0x0.000002P-126f; // 1.4e-45f
    ```

    正常浮点值下，正数最小值为
    $$
    0X00800000 = [0 0000 0001 000 0000 0000 0000 0000 0000] = (-1)^0*(1.0)*2^{1-127} = 2^{-126}
    $$

    ```java
        /**
         * A constant holding the smallest positive normal value of type
         * {@code float}, 2<sup>-126</sup>.  It is equal to the
         * hexadecimal floating-point literal {@code 0x1.0p-126f} and also
         * equal to {@code Float.intBitsToFloat(0x00800000)}.
         *
         * @since 1.6
         */
        public static final float MIN_NORMAL = 0x1.0p-126f; // 1.17549435E-38f
    ```

    指数位全为0时，指数值为$$-126$$，而不是$$0-127 = -127$$，以下为个人猜测：

    当$$M$$取最大值[111 1111 1111 1111 1111 1111]时，若$$e = -127$$。则
    $$
    x = (-1)^0*(0.M)*2^{-127} ≈ 2^{-127}
    $$
    而，正常最小值为$$2^{-126}$$，这会导致$$2^{-126}$$与$$2^{-127}$$之间的值无法表示。

    ```
        /**
         * Minimum exponent a normalized {@code float} variable may have.
         * It is equal to the value returned by {@code
         * Math.getExponent(Float.MIN_NORMAL)}.
         *
         * @since 1.6
         */
        public static final int MIN_EXPONENT = -126;
    ```

## 四、String

- 值不可以被改变，一旦改变则表示重新生成新的对象
- .substring(<start>[,<end>]): 返回strat下标以后(到end结束)的字符串
- substring在jdk1.6中因为返回的String对象仍然引用分割前的字符串数组，可能导致内存泄露

### 字符串连接

#### `+`拼接字符串

实际为先new一个StringBuilder对象，再用append方法扩展

```
String saito = "saito";
String asuka = saito + ",";
//编译后
String asuka = (new StringBuilder()).append(saito).append(",");
```

#### concat（）

新建一个字符串数组并拷贝需要连接的字符串，再返回一个新的String对象

```java
public String concat(String str) {
    int otherLen = str.length();
    if (otherLen == 0) {
        return this;
    }
    int len = value.length;
    char buf[] = Arrays.copyOf(value, len + otherLen);
    str.getChars(buf, len);
    return new String(buf, true);
}
```

#### StringBuffer和StringBuilder

- 内部字符数组默认长度为给定字符长度**+16**，无参即为16；

- append会直接拷贝字符到内部的字符数组中，如果字符数组长度不够，会进行扩展。

- `StringBuffer`是线程安全的，而`StringBuilder`则不是线程安全的。

用时从短到长的对比是：`StringBuilder`<`StringBuffer`<`concat`<`+`

### 常量折叠

- 常量折叠是一种`编译器优化`技术。字符串字面量
- 常量折叠主要指的是`编译期常量`加减乘除的运算过程会被折叠

> Java语言规范15.28](http://java.sun.com/docs/books/jls/third_edition/html/expressions.html#15.28)规定了Java的常量表达式可以表示原始类型或者字符串；它们不但可以由纯粹的字面量构成，还可以包含能在编译时确定结果的运算，包括+、-、~、!、*、/、%、<<、>>、>>>、<、>、<=、>=、==、!=、&、|、^、&&、||、? :，还有指向上述类型的常量（final变量）的表达式。 

#### 常量折叠发生的条件

- 必须是**编译期常量之间**进行运算才会进行常量折叠。
- 编译期常量就是**编译的时候就可以确定其值的常量**
    - 首先：字面量是`编译期常量`。（数字字面量，字符串字面量等）
    - 其次：编译期常量进行`简单运算的结果`也是`编译期常量`，如1+2，"a"+"b"。
    - 最后：被编译器常量`赋值的 final 的基本类型和字符串变量`也是编译期常量。

```java
    public static void main(String[] args) {
        String a = "a";
        String bc = "bc";
        String s1 = "a" + "bc";
        String s2 = a + bc;
        System.out.println(s1 == s2);//false
    }
    public static void main(String[] args) {
        final String a = "a";
        final String bc = "bc";
        String s1 = "a" + "bc";
        String s2 = a + bc;
        System.out.println(s1 == s2);//true
    }
    public static void main(String[] args) {
        String x ="a";
        final String a = x;
        final String bc = "bc";
        String s1 = "a" + "bc";
        String s2 = a + bc;
        System.out.println(s1 == s2);//false
    }
    public static void main(String[] args) {
        String x ="a";
        final String a = x;
        final String bc = "bc";
        String s1 = "a" + "bc";
        String s2 = a + bc;
        System.out.println(s1 == s2.intern());//true
    }
```

## 五、分支结构

- switch语句可以接受32位一下整型 ，String ，Enum ，char类型
- for in 在jdk1.5之后才支持

- **其实switch只支持一种数据类型，那就是整型，其他数据类型都是转换成整型之后在使用switch的。**

- 字符串的switch是通过`equals()`和`hashCode()`方法来实现的，先case判定hash值，再equals对比；

## 六、关键字

### final

**1. 数据**

声明数据为常量，可以是编译时常量，也可以是在运行时被初始化后不能被改变的常量。

- 对于基本类型，final 使数值不变；
- 对于引用类型，final 使引用不变，也就不能引用其它对象，但是被引用的对象本身是可以修改的。

**2. 方法**

声明方法不能被子类重写。

private 方法隐式地被指定为 final，如果在子类中定义的方法和基类中的一个 private 方法签名相同，此时子类的方法不是重写基类方法，而是在子类中定义了一个新的方法。

**3. 类**

声明类不允许被继承。

### static

**1. 静态变量**

- 静态变量：又称为类变量，也就是说这个变量属于类的，类所有的实例都共享静态变量，可以直接通过类名来访问它。静态变量在内存中只存在一份。
- 实例变量：每创建一个实例就会产生一个实例变量，它与该实例同生共死。

**2. 静态方法**

静态方法在类加载的时候就存在了，它不依赖于任何实例。所以静态方法必须有实现，也就是说它不能是抽象方法。

只能访问所属类的静态字段和静态方法，方法中不能有 this 和 super 关键字。

**3. 静态语句块**

静态语句块只在类初始化时运行一次。

**4. 静态内部类**

非静态内部类依赖于外部类的实例，而静态内部类不需要。

静态内部类不能访问外部类的非静态的变量和方法。

**5. 静态导包**

在使用静态变量和方法时不用再指明 ClassName，从而简化代码，但可读性大大降低。

**6. 初始化顺序**

静态变量和静态语句块优先于实例变量和普通语句块，静态变量和静态语句块的初始化顺序取决于它们在代码中的顺序。

```
public static String staticField = "静态变量";
static {
    System.out.println("静态语句块");
}
public String field = "实例变量";
{
    System.out.println("普通语句块");
}
```

最后才是构造函数的初始化。

```
public InitialOrderTest() {
    System.out.println("构造函数");
}
```

存在继承的情况下，初始化顺序为：

- 父类（静态变量、静态语句块）
- 子类（静态变量、静态语句块）
- 父类（实例变量、普通语句块）
- 父类（构造函数）
- 子类（实例变量、普通语句块）
- 子类（构造函数）



### transient

阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被transient修饰的变量值不会被持久化和恢复。transient只能修饰变量，不能修饰类和方法。

instanceof、volatile、synchronized、const 原理及用法。

## 七、泛型

## 八、异常

Throwable 可以用来表示任何可以作为异常抛出的类，分为两种： **Error** 和 **Exception**。其中 Error 用来表示 JVM 无法处理的错误，Exception 分为两种：

- **受检异常** ：需要用 try...catch... 语句捕获并进行处理，并且可以从异常中恢复；
- **非受检异常** ：是程序运行时错误，例如除 0 会引发 Arithmetic Exception，此时程序崩溃并且无法恢复。


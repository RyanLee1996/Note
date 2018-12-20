# 第2章 Java内存区域与内存溢出异常

## 运行时数据区域

> Java虚拟机在执行Java程序的过程中会把它所管理的内存划分为若干个不同的数据区域。这些区域都有各自的用途，以及创建和销毁的时间，有的区域随着虚拟机进程的启动而存在，有些区域则依赖用户线程的启动和结束而建立和销毁。

Java 虚拟机的内存模型分为两部分：一部分是线程共享的，包括 Java `堆`和`方法区`；另一部分是线程私有的，包括`虚拟机栈`和`本地方法栈`，以及`程序计数器`这一小部分内存。

![](D:\Github\Note\Resources\JVM运行时数据区.png)

![](D:\Github\Note\Resources\JVM.png)

### 程序计数器（Program Counter Register）

1. 如果线程正在执行的是Java 方法，则这个计数器记录的是正在执行的虚拟机字节码指令地址
2. 如果正在执行的是Native 方法，则这个技术器值为空（Undefined）
3. 此内存区域是唯一一个在Java虚拟机规范中没有规定任何OutOfMemoryError情况的区域
4. 线程隔离性，每个线程工作时都有属于自己的独立计数器。

### 虚拟机栈（Java Virtual Machine Stacks）

> 生命周期与线程相同。
>
> 虚拟机栈描述的是Java方法执行的内存模型：每个方法在执行的同时都会创建一个栈帧(**Stack Frame**; 是方法运行时的基础数据结构) 用于存储局部变量表（**Array of local variables**）、操作数栈（**Operand stack**）、动态链接（**Reference to runtime constant pool (Dynamic linking)**）、方法出口等信息。




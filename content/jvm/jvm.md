**第一章 JVM与JAVA体系结构**

  

**JVM生命周期：**

﻿

14-JVM的生命周期 P14 - 00:05

﻿

**1.虚拟机的启动**

java虚拟机的启动是通过引导类加载器（bootstrap class loader） 创建一个初始类（initial class）来完成的，这个类是有虚拟机的集体实现指定的

**2.虚拟机的执行**

一个运行中的java虚拟机有着一个清晰的任务：执行java程序。

程序开始执行时他才运行，程序结束时他就停止

执行一个所谓的java程序的时候，真真正正在执行的是一个叫做java虚拟机的进程

**3.虚拟机的退出**

程序正常执行结束

程序在执行过程和总遇到了异常或者错误而异常终止

由于操作系统出现错误而导致java虚拟机进程终止

某线程调用Runtime类或者System类的exit方法，或者Runtime类的halt方法，并且java安全管理器也允许这次exit或者halt操作 （System.exit方法实际上也是去调用了Runtime类的halt方法（Runtime是一个饿汉式加载的运行时数据区（Runtime Data Area）每个运行时的虚拟机独有一份 包含了 方法区、java栈、本地方法栈、堆、程序计数器））


  

除此之外，JNT（Java Native Interface）规范描述了用JNT Invocation APi来加载或卸载Java虚拟机时，Java虚拟机的退出情况

  

**JVM的发展历程**﻿

**1.Sun Classis VM** 世界第一款商用java虚拟机 1.4被淘汰 内部只提供解释器（不提供JIT即时编译器）效率底下。

﻿

15-SUN Classic VM的介绍 P15 - 00:06

﻿

**2.Exact V****M**准确式内存管理（可以知道内存中某个位置的数据具体是什么类型的数据）热点探测，编译器和结束器混合工作模式

﻿

16-Exact VM的介绍 P16 - 00:02

﻿

**3.HotSpot V****M**（目前正在使用中）JDK3之后到目前一直是作为默认虚拟机，Oracle JDK/Open JDK的默认虚拟机，服务器，桌面，移动端，嵌入式都有使用，拥有热点探测技术 （方法区的概念只有HotSpot虚拟机有，jRock/J9都没有方法去概念）

﻿

17-HotSpot VM的介绍 P17 - 00:02

﻿

**4.JRockit V****M**（BEA（已经被Oracle收购）） 内部不包含解释器实现，全部代码都靠即时编译器编译之后执行，世界上最快的JVM

﻿

18-JRockit VM的介绍 P18 - 00:03

﻿

**5.J9 VM（IBM）** 执行IBM公司的产品速度快，定位接近HotSpot 其他产品优化不及IBM公司产品，不稳定

﻿

19-IBM J9 VM的介绍 P19 - 00:03

﻿

**6.KVM和CDC /CLDC HotSpot** （CDC /CLDC HotSpot java ME产品线上的两款虚拟机）KVM是进军移动端的JVM用量小（android 和IOS占据）

﻿

20-KVM、CDC、CLDC的介绍 P20 - 00:02

﻿

**7.Azul VM** 特定硬件平台绑定，软硬件配合的专有虚拟机（每个Auzl vm实例都可以管理至少数十个CPU和数百GB内存的硬件资源，并提供在巨大内存范围内，实现可控的GC时间的垃圾收集器，专有硬件优化的线程调度等优秀特性）

﻿

21-Azul VM和BEA Liquid VM的介绍 P21 - 00:01

﻿

**8.Liquid VM**和Azul VM类似 特定平台性能优异

﻿

21-Azul VM和BEA Liquid VM的介绍 P21 - 00:03

﻿

**9.Apache Harmony VM** IBM和intel联合开发开元的JVM,受到同样开源的OpenJDK的压制，Sun坚决不让Harmony获得JCP认证，最终与2011年退役，IBM转而参与开发OpenJDK，没有大规模商用，但是他的java类库被吸纳进Android SDK中

﻿

22-Apache Harmony的介绍 P22 - 00:01

﻿

**10 Microsoft JVM** windows xp 之前在windows平台下最好的JVM，后期被抹除

﻿

23-Microsoft JVM和TaobaoJVM P23 - 00:04

﻿

**11 Taobao JVM** 基于OpenJDK自己定制的ALIBABA JDK 应用在阿里产品上性能高，硬件严重依赖intel的cpu,损失了兼容性，但是提高了性能

﻿

23-Microsoft JVM和TaobaoJVM P23 - 00:13

﻿

创新的GCIH（GC invisible heap）技术实现了off-heap,即将生命周期较长的java对象从heap（堆）中移到heap之外，并且GC不唔唔管理GCIH内部的java对象，以此达到降低GC的回收频率和提升GC的回收效率目的

GCIH中的对象还能在多个Java虚拟机进程中实现共享

使用crc32指令实现JVM intrinsic 降低JNT的调用开销

PMU headware和Java profiling tool 和诊断协助功能

针对大数据场景的ZenGC

**12 Dalvik VM （不是java虚拟机的虚拟机）**google开发应用Android 没有遵循java虚拟机规范 执行文件是dex格式文件，基于寄存器架构

﻿

24-Dalvik VM及其他虚拟机的介绍 P24 - 00:01

﻿

**13.Graal VM（Oracle 新虚拟机）**在HotSpot vm基础上增强而成的跨语言全栈虚拟机，可以作为任何语言的运行平台使用，语言包括（Java、Scala、Groovy、Kotlin、C、C++、JavaScript、Ruby、Python、R等）

﻿

25-Graal VM的介绍 P25 - 00:03

﻿

支持不同语言中混用对方的借口和对象，支持这些语言使用已经编译好的本地库文件

工作原理时间爱那个这些语言的源代码或者源代码编译后的中间格式，通过解释器转换为能被Graal VM接受的中间表示，GraalVM 提供Truffle工具集快速构建面向一种新语言的解释器，在运行时还能进行即使编译优化，获得比原生编译器更加优秀的执行效率

如果说HotSpot有一天真的被取代，Graal VM希望最大，但是Java的软件生态没有丝毫变化


  

**第二章 类加载子系统**

**1.Class Loader SubSystem 类加载子系统**

**Class Files->Loading->Linking->Initialization**

**1.1.Loading 区域 （负责从文件系统或者网络中加载Class文件，class文件在文件开头有特定的文件标识，只负责加载，是否能运行则由执行引擎决定）**

﻿

28-类的加载过程一：Loading P28 - 00:01



  

Boolstrap Class Loader 引导类加载器、Extension ClassLoader 扩展类加载器、System ClassLoader 应用类/系统类加载器

方法区域（7之前永久代，7之后源空间）

加载方式：

1.从本地系统直接加载

2.通过我网络获取，典型场景：Web Applet

3.从zip压缩包中独去，成为日后jar.war格式的基础

4.运行时计算产生，使用最多的，动态代理技术

5.有其他文件身成 典型场景，jsp应用

6.从专有数据库中提取.class文件，比较少见

7.从加密文件中获取，典型的放class文件被反编译的保护措施

  

**1.1.1 类加载器的分类**

JVM支持两种类型的类加载器，分别为引导类加载器（bootstrap ClassLoader）和自定义类加载器（User-Defined ClassLoader） 这里的自定义类加载器指的是将所有派生于抽象类ClassLoader的类加载器都划分为自定义加载器，不是指有开发人员自定义的类加载器（Extension Class Loader#扩展类加载器、System Class Loader#系统类加载器都属于自定义加载器）

  

**BootstrapClassLoader**

﻿

32-引导类、扩展类、系统类加载... P32 - 00:17

﻿

BootstrapClassLoader 由c/c++编写，嵌套在jvm内部 只加载java的核心类库 （/JAVA_HOME/jre/lib/rt.jar、resources.jar、或者sun.boot.class.path路径下的内容），用于提供jvm自身需要的类，并不是继承自java.lang.Classloader 没有父加载器，加载扩展类加载器和程序类接载其，并指定为他们的父类，处于安全考虑，Bootstrap启动类加载器只加载包名为java、javax、sun等开头的类

  

**ExtensionClassLoader**

﻿

32-引导类、扩展类、系统类加载... P32 - 03:59

﻿

由java编写，由sun.misc.Launcher$ExtClassLoader内部类实现，派生于ClassLoader类，父类加载器为BootstrapClassLoader 启动类加载器，从java.ext.dirs系统属性所指定的目录中加载类库，或从JAVA_HOME/jre/lib/ext子目录（扩展目录）下加载类库，如果用户创建的JAR放在此目录下，也会自动由扩展类加载器加载

  

**AppClassLoader**

﻿

32-引导类、扩展类、系统类加载... P32 - 05:04

﻿

java语言编写，由sun.misc.Launcher$AppClassLoader实现，派生与ClassLoader，父类加载器为扩展类加载器，它负责加载环境变量classpath或者系统属性，java.class.path指定下的类库，该类是程序中的默认加载器，一般来说，java应用的类都是由它来加载完成，通过classLoader#getSystemClassLoader（）方法可以获取到该类

  

**用户自定义类加载器**

﻿

33-为什么需要用户自定义类加载... P33 - 00:05

﻿

一般用不到，可能的情况

隔离加载类、修改加载的方式、扩展加载源、防止源码泄露

步骤

1.继承抽象类java.lang.ClassLoader 实现自己的类加载器

2.在JDK1.2之前，在自定义类加载器之前，总会去继承ClassLoader类并重写loadClass（）方法，从而实现自定义的类加载器，但是在JDK1.2之后，不在建议用户覆盖loadClass()方法，二十建议把自定义的类加载逻辑卸载findClass方法中

3.如果没有太过于负责的需求，可以直接继承URLClassLoader类，这样就可以避免自己去编写findClass（）方法及获取字节码流的方式。

  

**双亲委派机制**

﻿

35-双亲委派机制的工作原理及演示 P35 - 00:00

﻿

1.如果一个类的加载器收到类加载请求，它并不会自己先去加载，而是把这个请求委托给父类去执行加载，

2.如果父类加载器还存在其父类加载器，则进一步向上委托，依此递归，请求最终将达到顶层类加载器

3.如果父类加载器可以完成类加载任务，就成功返回，倘若父类加载器无法完成此加载任务，子加载器才会尝试自己去加载，这就是双亲委派机制


﻿

36-双亲委派机制的优势 P36 - 01:54

﻿

**双亲委派机制的优势**：

1.避免类的重复加载

2.保护程序安全，防止核心api被随意篡改

  

**沙箱安全机制**

﻿

37-沙箱安全机制 P37 - 00:28

﻿

eg：自定义String类，但是在加载自定义的String类的时候会率先使用引导类加载器加载，而引导类加载器在加载过程中，会先加载JDK自带的文件，（rt.jar包中的java\lang\String.class）报错信息说没有main方法就是因为加载的rt.jar中的String类，这样保证对java核心源代码的保护，这就是沙箱安全机制

  

**其他：**

﻿

38-类的主动使用与被动使用等 P38 - 00:14

﻿

在JVM中，表示两个class对象是否为同一个类存在两个必要条件：

类的完整类名必须一致，包括包名

加载这个类的ClassLoader（指ClassLoader实例对象）必须相同

换句话说，在jvm中，即使这两个类对象（class对象）来源同一个Class文件，被同一个虚拟机所加载，但只要他们的ClassLoader实力对象不同，那么这两个类对象也是不相等的

JVM必须知道一个类型是由启动类加载器加载的还是由用户类加载器加载的，如果一个类型是用户类加载器加载的，那么JVM会将这个类的加载器的一个引用作为类型信息的一部分保存在方法区中，当解析一个类的另一个类型的引用的时候，JVM需要保证这两个类型的类加载器是相同的

类的主动使用和被动使用

Java程序对类的使用方式分为，主动使用和被动使用

主动使用，又分为7种情况

1.创建类的实例

2.访问某个类或接口的静态资源，或者对该静态变量赋值

3.调用类的静态方法

4.反射（比如：Class.forName("xxx.xxx.xxx")）

5.初始化一个类的子类

6.Java虚拟机启动时被标名为启动类的类

7.JDK7开始提供的动态语言支持：Java.lang.invoke.MethodHandle实例的解析结果，REF_getStatic、Ref_putStatic、REF_invokeStatic句柄对应的类没有初始化，则初始化

除了以上的七种情况，其他使用java类的方式都被看做是对类的被动使用，都不会导致类的初始化

  

  

**1.2.Linking 区域**

﻿

29-类的加载过程二：Linking P29 - 00:01

﻿

**verify验证**

目的在于确保class文件的字节流中包含信息符合当前虚拟机要求，包含在呢个被加载类的正确性，不会危害虚拟机本身

主要有四种验证，文件格式验证，元数据验证，字节码验证，符号引用验证

**Prepare准备**

为类变量分配内存并设置该类的默认初始值，即零值

这里不包含用final修饰的static,因为final在变异的时候就会分配了，准备阶段会显式初始化

这里不会为实力变量分配初始化，类变量会分配在方法区中，而实力变量是会随着对象一起分配到java堆中

**Resolve解析**

将常量池内的符号引用转换为直接引用的过程

事实上，解析操作往往会伴随着JVM在执行初始化之后再执行

符号引用就是一族符号来描述所引用的目标，符号引用的字面量形式明确定义在《java虚拟机规范》的class文件格式中，直接引用就是窒息那个目标的指针，相对片量或一个间接定位到目标的句柄

解析动作主要针对类或接口，字段，类方法，接口方法，方法类型等，对影响量池中的CONSTANT_Class_info、CONSTANT_Fieldref_info、CONSTANT_Methodref_info等。

  

**1.3.Initialization 区域 初始化 静态变量显式初始化**

﻿

30-类的加载过程三：Initialization P30 - 02:00

﻿

初始化阶段就是执行类构造器方法<clinit>()的过程

此方法不需要定义，是有javac编译器自动收集类中的所有类变量的赋值动作和静态代码块中的语句合并而来

构造方法中指令按照语句在源文件中出现的顺序执行

<clinit>()不同于类的构造器。（构造器是虚拟机视角下的<init>()）

若该类具有父类，JVM会保证子类的<clinit>()执行前，父类的<clinit>()已经执行完毕

虚拟机必须保证一个类的<clinit>()方法在多线程下被同步加锁。

  

**2. Runtime Data Areas 运行时数据区**

﻿

39-运行时数据区内部结构 P39 - 07:27

﻿

  

**2.1 Method Area 方法区**

**2.2 Heap Area 堆区 多个线程共享**

**2.3 Stack Area 栈区 每个线程独一份**

**2.4 PC Registers pc寄存器（程序计数器） 每个线程独一份**

**2.5 Native Method Stack 本地方法栈**

**2.6 Metaspace（元数据区域）//v8之后才有的之前是永久代**

java虚拟机定义了若干中程序运行期间会使用到的运行时数据区，其中有一种会随着虚拟机启动而创建，随着随你及推出而销毁，另一些则是与线程一一对应的，这些与线程对应的数据区域会随着线程开始和结束而创建和销毁，

即：每个线程，独立包括程序计数器，虚拟机栈，本地方法栈;线程间共享：堆，堆外内存、方法区（永久代或者元空间、代码缓存）

  

  

**3.Execution Engine 执行引擎**

**3.1Interpreter 解释器**

**3.2 JIT Compiler 即时编译器 （中间代码生成器、代码优化器、目标代码生成器）**

**3.3 Garbage Collection GC垃圾回收器**

  

  

**如果自己手写虚拟机 需要考虑 类加载子系统以及执行引擎**

-   1
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIzODE4NTg2MywtNjc1MjM4ODk4XX0=
-->
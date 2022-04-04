---
layout: post
title: 服务端@Java@JVM@ClassFormat
date: 2022-03-20 09:00:00 +0800
categories: 【服务端】
tag: 【Java】
---

- [Java语言规范](https://docs.oracle.com/javase/specs/index.html)


### Class文件结构

- magic 
	- CAFEBABE
- minor version
	- 
- major version
	- 
- constant_pool_count
	- 
- constant_pool
	- 1 CONSTANT_Utf8_info
		- 1字节
			- 标识符
		- length
			- 
		- bytes
			- 

	- 3 CONSTANT_Integer_info
		- 4字节
			- Big-Endin(高位在前)
			- int

	- 4 CONSTANT_Float_info
		- 4字节
			- Big-Endin(高位在前)
			- float

	- 5 CONSTANT_Long_info
		- 8字节
			- Big-Endin(高位在前)
			- long

	- 6 CONSTANT_Double_info
		- 8字节
			- Big-Endin(高位在前)
			- double

	- 7 CONSTANT_Class_info
		- 2字节
			- 指向类的全限定名项的索引

	- 8 CONSTANT_String_info
		- 2字节
			- 指向字符串字面量的索引

	- 9 CONSTANT_Fieldref_info
		- 2字节
			- 指向申明字段的类或者接口描述符
			- CONSTANT_Class_info的索引项
		- 2字节
			- 指向字段描述符号
			- CONSTANT_NameAndType_info的索引项

	- 10 CONSTANT_Methodref_info
		- 2字节
			- 指向声明方法的类或者接口描述符
			- CONSTANT_Class_info的索引项
		- 2字节
			- 指向字段描述符号
			- CONSTANT_NameAndType_info的索引项
		
	- 11 CONSTANT_InterfaceMethodref_info
		- 2字节
			- 指向声明方法的类或者接口描述符
			- CONSTANT_Class_info的索引项
		- 2字节
			- 指向字段描述符号
			- CONSTANT_NameAndType_info的索引项

	- 12 CONSTANT_NameAndType_info
		- 2字节
			- 指向该字段或方法名称常量项的索引
		- 2字节
			- 指向该字段或方法描述符常量项的索引

	- 15 CONSTANT_MethodHandle_info
		- 1字节
			- reference_kind 1-9之间的值
			- 决定了方法句柄的类型
			- 方法句柄类型的值表示方法句柄的字节码行为

	- 16 CONSTANT_MethodType_info
		- 2字节
			- descriptor_index
			- 指向Utf8_info结构表示的方法描述符

	- 18 CONSTANT_InvokeDynamic_info
		- 2字节
			- bootstrap_method_attr_index
			- 当前Class文件中引导方法表的bootstrap_methods[] 数组的有效索引
		- 2字节
			- 指向NameAndType_info表示的方法名和方法描述符

- access_flags
	- ACC_PUBLIC 0x0001 是否是public 
	- ACC_FINAL 0x0010 是否是final
	- ACC_SUPER 0x0020 必须为真
	- ACC_INTERFACE 0x0200 是否是接口
	- ACC_ABSTRACT 0x1000 接口或抽象类
	- ACC_SUNTHETIC 0x1000 编译器自动生成
	- ACC_ANNOTATION 0x2000
	- ACC_ENUM 0x4000
- this_class
	- 当前类
- super_class
	- 父类
- interface_count
	- 
- interfaces
- filds_count
- fields
	- 
- methods_count 
	- 
- method_info
- attribute_count
- attribute

### Class加载过程

- load
	- 
- Link：静态变量赋默认值
	1. Verification
	2. Preparation
		- 
		- 
	3. Resolution 
		- 符号引用解析为直接引用
		- 常量池里面的符号解析为指针、偏移量的内存的直接引用
- Initializing
	1. 调用类初始化代码

### New对象的过程

- 申请内存
	- 赋默认值
- 构造方法
	- 设置初始值

### 类加载器层次
- 自顶而下：进行实际查找和加载child方向
- 自底向上：惊醒检查该类是否已经加载parent方向

- 加载层级(Launcher源码)
	- Bootstrap
		- 加载lib/rt.jar charset.jar等核心类：C++实现
		- sun.boot.class.path
	- Extension
		- 加载拓展jar包，jre/lib/ext/*.jar
		- 或由-Djava.ext.dirs指定
		- java.ext.dirs
	- App
		- 加载classpath指定内容
		- java.class.path
	- Custom ClassLoader
		- 自定义ClassLoader
- 加载机制
	- 双亲委派
		-
	- 为什么用双亲委派？
		- 主：安全机制
		- 次：资源节约

### Java并发操作

- Java并发内存模型
	- Java线程--工作内存--Save和Load操作 <===> 主内存
	- Java线程--工作内存--Save和Load操作 <===> 主内存

- volatile
	- 字节码层面
		- ACC_VOLATILE
	- JVM层面： volatile内存区的读写都加屏障
		- 写
			- StoreStoreBarrier
			- 写操作
			- StoreLoadBarrier
		- 读
			- LoadLoadBarrier
			- 读操作
			- LoadStoreBarrier
	- [OS和硬件层面](https://blog.csdn.net/qq_26222859/article/details/52235930)
		- hsdis-HotSpot Dis Assembler
			- windows lock指令实现

- synchronized
	- 字节码层面
		- ACC_SYNCHRONIZED
		- monitorenter
		- monitorexit
	- JVM层面
		- C/C++调用了系统提供的同步机制
		- 
	- [OS和硬件层面](https://blog.csdn.net/21aspnet/article/details/88571740)
		- X86: lock comxchg xxx

### JVM重排序规则

- hanppens-before原则
	- JLS17.4.5

- as if serial
	- 

### 对象的内存布局

- 对象的创建过程？
	1. class loading
	2. class linking()
	3. class initializing
	4. 申请对象内存
	5. 成员变量赋默认值
	6. 调用构造方法<init>
		1. 成员变量顺序赋初始值
		2. 执行构造方法语句

- 对象在内存中的存储布局？ 
	- 虚拟机配置
	- 普通对象
		1. 对象头 markword 8
		2. ClassPointer指针
		3. 实例数据
			- 引用类型：-XX:+UseCompressedOops为4字节，不开启8字节
				- ordinary object pointers
		4. Padding对齐，8的倍数
	- 数组对象
		1. 对象头 markword 8
		2. ClassPointer指针 
			- -XX:+UseCompressedOops为4字节，不开启8字节
		3. 数组长度：4字节
		4. 数组数据
		4. 对齐，8的倍数

-  对象头具体包括什么？
	- 通过JavaAgent机制获取
		- Instrumentation
			- getObjectSize
	- markword
		- 无锁态
		- 轻量级锁
		- 重量级锁
		- GC标记
		- 偏向锁

- 对象怎么定位？
	- [参考](https://blog.csdn.net/clover_lily/article/details/80095580)
	- 句柄池
		- 间接指针: GC占优
			- Object
			- Class
	- 直接指针: 执行占优
		- Object 

- 对象怎么分配？
	- GC相关内容

- 对象大小的实例
	- new Object()对象占多少个字节？
		- 16字节
			- 对象头头8字节
			- ClassPointer指针 4字节

### Hotspot开启内存压缩的规则
1. 4G以下，直接砍掉
2. 4G-32G,默认开启内存压缩 ClassPointers Oops
3. 32G，压缩无效，使用64位


### JVM Runtime Data Area and JVM Instructions

- Data Area 
	- Program Counter
		- 存放执行位置
		- 虚拟机的运行类似while循环
	- JVM stacks
		1. Frame:栈桢
			- Local Variable Table 
			- Operated Stacks
			- Dynamic Linking
			- Return Address
		2. 一个方法对应一个栈帧	
			- 
			- 

	- Heap
		- 
	- Native Method stacks
		- C/C++
		- JNI
	- Direct Memory
		- NIO，zero copy
		- JVM可以直接访问的内核的内存
	- Method Area
		- run-time constant pool 
		- Content
			1. Perm Space(< 1.8)
				- 字符串常量位于此
				- FGC不会清理
				- 大小启动的时候指定，不能变
			2. Meta Space(>=1.8)
				- 字符串常量位于堆区
				- 会触发FGC清理
				- 不设定的话，最大就是物理内存

### JVM Instruction Set

- store
- load
- pop
- mul
- sub
- add 
- invoke
	- invokestatic
	- invokevirtual
		- 
	- invokeinterface
	- invokespecial
		- 可以直接定位，不需要多台的方法
			- private 方法
			- 构造方法
	- invokedynamic:最难
		- lambda表达式
		- 反射
		- 其他动态语言：scala kotlin 
		- CGLib ASM
		- 动态产生的Class 

### Garbage Collector GC turninig
- 熟悉GC常用算法，熟悉常见垃圾收集器，具有实际JVM调优经验
- Garbage
	- 没有引用指向的对象
	- 
	- root searching
		- GC roots
			- 线程栈变量
			- 静态变量
			- 常量池
			- JNI指针
	- GC Algorithms
		- Mark-Sweep
			- 两次
			- 
		- Copying
			- 一次
			- 
		- Mark-Compact
			- 两次
			- 
- 堆内存逻辑分区（不适合不分代垃圾收集器）
	- ⚠️
		- 除了Epsilon ZGC Shenandoah 之外的GC都是使用逻辑分代模型
		- G1是逻辑分代，物理不分代
		- 除此之外不仅逻辑分代，而且物理分代
	- 新生代： MinorGC/YGC
		- eden: 8
		- survivor: 1
		- survivor: 1
			- Copying
		- 复制年龄超过限制时，进入old区。通过参数：-XX:MaxTenuringThreshold配置
	- 老年代: MajorGC/FullGC
		- 

- 内存详解
	- 栈上分配
		- 线程私有小对象
		- 无逃逸
		- 支持标量替换
		- 无需调整
	- 线程本地分配TLAB
		- 占用eden,默认1%
		- 多线程的时候不用竞争eden就可以申请空间，提高效率
		- 小对象
		- 无需调整
	- 老年代
		- 










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

### 常见

- volatile
	- JVM层面
		- 写
			- StoreStoreBarrier
			- 写操作
			- StoreLoadBarrier
		- 读
			- LoadLoadBarrier
			- 读操作
			- LoadStoreBarrier
- 







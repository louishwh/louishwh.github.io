---
layout: post
title:  百度超级链-XuperChain
date: 2019-06-16 18:50:00 +0800
categories: 【区块链】
tag: 六月
---


### 内容概要
	
	- 介绍
	- 编译
	- 文件结构介绍
	- 基本操作


#### 介绍

XuperUion是超级链体系下的第一个开源项目，是构建超级联盟网络的底层方案。

- 核心特点

	- 高性能
		- 原创的XuperModel模型，真正实现了智能合约的并发执行和验证。
		- TDPOS算法确保大规模节点下的快速共识。
		- 使用AOT加速的WASM虚拟机，合约运行速度接近native程序。
	
	- 更安全
		- 多私钥保护的账户体系。
		- 鉴权支持权重累计、集合运算等灵活的策略。

	- 易扩展
		- 鲁棒的P2P网络，支持广域网超大规模节点。
		- 底层账本支持分叉管理，自动收敛一致性，实现真正全球化部署。
		- 多语言开发智能合约
		- 通过原创的XuperBridge技术，可插拔多语言虚拟机。

	- 高灵活性
		- 可插拔、插件化的设计使得用户可以方便选择适合自己业务场景的解决方案。

#### 编译

1. 系统配置
	- 操作系统：支持Linux以及Mac OS
	- 开发语言：Go 1.12.x及以上
	- 编译器：GCC 4.8.x及以上
	- 版本控制工具：Git

2. 获取代码
	> git clone https://github.com/xuperchain/xuperunion

3. 生成执行文件
	> cd xuperunion
	> 
	> make

4. 编译完成
	- 在output文件夹内部


#### 文件结构介绍

```
output
│
├── conf  	// 创始的共识采用tdpos模式，指定单一地址有权利出块
│  	│
│   ├── plugins.conf 		// 插件的配置信息
│  	│
│   ├── xchain.yaml.   		// xchain服务的配置信息
│  	│
│   └── xchain.yaml.sample 	// 防止冲突，部署时根据需要修改端口号
│  	
│  	
├── contractCall.sh
│
├── createAccount.sh
│
├── data  // 数据的存放目录,创世块信息，以及共识和合约的样例
│   │
│   ├── blockchain	// 账本目录
│   │   │
│   │   └── xuper
│   │       ├── ledger
│   │       │   ├── 000001.log
│   │       │   │
│   │       │   ├── CURRENT
│   │       │   │
│   │       │   ├── LOCK
│   │       │   │
│   │       │   ├── LOG
│   │       │   │
│   │       │   └── MANIFEST-000000
│   │       │   
│   │       ├── utxoVM
│   │       │   │
│   │       │   ├── 000001.log
│   │       │   │
│   │       │   ├── CURRENT
│   │       │   │
│   │       │   ├── LOCK
│   │       │   │
│   │       │   ├── LOG
│   │       │   │
│   │       │   └── MANIFEST-000000
│   │       │  	
│   │       └── xuper.json
│   │   	
│   ├── config	// 创始的共识采用tdpos模式，指定单一地址有权利出块
│   │  	│  	
│   │   ├── decay_demo.json
│   │  	│  	
│   │   ├── pmroot.json
│   │  	│  	
│   │   ├── pow.json
│   │  	│  	
│   │   ├── root_demo.json
│   │  	│  	
│   │   └── xuper.json
│   │  	
│   │  	
│   ├── keys // 此节点的地址，唯一性
│   │  	│  	
│   │   ├── address
│   │  	│  	
│   │   ├── private.key
│   │  	│  	
│   │   └── public.key
│   │  	
│   └── netkeys // 此节点的网络标识ID，唯一性
│      	│  	
│       └── net_private.key
│   
│   
├── deployContract.sh
│   
│   
├── dump_chain
│   
│   
├── logs  // 程序日志目录
│   │  	
│   ├── pluginmgr.log
│   │  	
│   ├── pluginmgr.log.wf
│   │  	
│   ├── xchain.log
│   │  	
│   └── xchain.log.wf
│   
│   
├── plugins	// so的存放目录
│   │   
│   ├── consensus
│   │   │   
│   │   ├── consensus-pow.so.1.0.0
│   │   │   
│   │   ├── consensus-single.so.1.0.0
│   │   │   
│   │   └── consensus-tdpos.so.1.0.0
│   │   
│   ├── contract
│   │   
│   ├── crypto
│   │   │   
│   │   └── crypto-default.so.1.0.0
│   │   
│   └── kv
│       │   
│       ├── kv-badger.so.1.0.0
│       │   
│       ├── kv-ldb-multi.so.1.0.0
│       │   
│       └── kv-ldb-single.so.1.0.0
│   
│   
├── testnet.conf
│       
├── transfer.sh
│       
├── wasm2c	// wasm工具
│       	
├── xchain  // 服务的二进制文件
│       
└── xchain-cli	// 客户端工具
```

#### 链的操作

1. 创建链
	> ./xchain-cli createChain

2. 启动服务
	> nohup ./xchain &

3. 观察区块
	> ./xchain-cli status -H 127.0.0.1:37101

4. 创建账号
	> ./xchain-cli account newkeys --output data/accounts/louis

5. 创建合约账号
	> ./xchain-cli account new --desc account.des
	> 合约内容如下: 
	> ```
	{
    "module_name": "xkernel",
    "method_name": "NewAccount",
    "args" : {
        "account_name": "1111111111111111",  //说明：16位数字组成的字符串
        "acl": "{
        		\"pm\": {\"rule\": 1,\"acceptValue\": 0.6},
        		\"aksWeight\": {\"AK1\": 0.3,\"AK2\": 0.3}}"
    }
	}```

6. 

#### 资源链接

[官网](https://xchain.baidu.com/)
[白皮书](https://xuperchain.baidu.com/whitepaper)
[Github](https://github.com/xuperchain/xuperunion)
[贡献指南](https://github.com/xuperchain/xuperunion/blob/master/CONTRIBUTING_CN.md)


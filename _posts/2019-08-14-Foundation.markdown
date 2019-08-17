---
layout: post
title: Foundation
date: 2019-08-14 00:00:00 +0800
categories: 【iOS】
tag: 【移动端】
---

[参考一](https://www.jianshu.com/p/495f5f8045ee)
[参考二](https://www.cnblogs.com/kenshincui/p/3885689.html)

### NSObject

- 值类型:
	- NSAffineTransform
	- NSCalendar
	- NSCache
	- NSValue
		- NSValue
		- NSNumber
		- NSDecimalNumber
	- NSData
		- NSMutableData
		- NSPurgeableData
	- NSDate
	- NSDateComponents
	- NSDecimalNumberHandler
	- NSLocale
	- NSNull
	- NSTimeZone
	- NSValueTransformer

- XML
	- NSXMLParser

- Strings
	- NSAttributedString
	- NSCharacterSet
	- NSString
	- NSFormatter
		- NSDateFormatter
		- NSNumberFormatter
	- NSScanner
	- NSSortDescriptor

- Collections
	- NSArray
		- NSMutableArray
	- NSDictionary
		- NSMutableDictionary
	- NSNumerator
		- NSDirectoryEnumerator
	- NSHashTable
	- NSIndexPath
	- NSIndexSet
		- NSMutableIndexSet
	- NSMapTable
	- NSPointerArray
	- NSPointerFunctions
	- NSSet
		- NSMutableSet
		- NSCountedSet

- Predicates
	- NSExpression
	- NSPredicate
		- NSComparisonPredicate
		- NSCompoundPredicate

- Operating-System Services
	- NSError
	- NSHost
	- NSNetService
	- NSNetServiceBrowser
	- NSOrthography
	- NSProcessInfo
	- NSRunLoop
	- NSSpeliServer
	- NSTextCheckingResult
	- NSTimer
	- NSUserDefaults

- File System
	- NSBundle
	- NSFileHandler
	- NSFileManager
	- NSMetadataItem
	- NSMetadataQuery
	- NSMetadataQueryAttributeValueTuple
	- NSMetadataQueryResuleGroup
	- NSStream
		- NSInputStream
		- NSOutputStream

- URL
	- NSCachedURLResponse
	- NSHTTPCookie
	- NSHTTPCookieStorage
	- NSURL
	- NSURLAuthorizationChallenge
	- NSURLCache
	- NSURLSession
	- NSURLCredential
	- NSURLCredentialStorage
	- NSURLDownload
	- NSURLProtectionSpace
	- NSURLProtocol
	- NSURLRequest
		- NSMutableURLRequest
	- NSURLResponse
		- NSHTTPURLResponse

- Interprocess Communication
	- NSPipe
	- NSPort
		- NSMachPort
		- NSMessagePort
		- NSSockerPort
	- NSPortMessage
	- NSPortNameServer
		- NSMachBootstrapServer
		- NSMessagePortNameServer
		- NSSockerPortNameServer

- Locking-Threading
	- NSConditionLock
	- NSDistributedLock
	- NSLock
	- NSOperation
		- NSBlockOperation
		- NSInvocationOperation
	- NSOperationQueue
	- NSRecursiveLock
	- NSTask
	- NSThread

- Notifications
	- NSNotification
	- NSNotificationCenter
		- NSNotificationQueue

- Archiving and Serialization
	- NSCoder
		- NSArchiver
		- NSKeyedArchiver
		- NSKeyedUnArchiver
		- NSPortCoder
		- NSUnarchiver
	- NSPropertyListSerialization

- Objective-C Language Service
	- NSSeertionHandler
	- NSAutoreleasePool
	- NSClassDescription
	- NSException
	- NSInvocation
	- NSMethodSignature
	- NSUndoManager


### NSProxy
	- [NSProxy1](https://blog.csdn.net/shubinniu/article/details/80895450)
	- [消息转发](https://blog.csdn.net/liyanjun201/article/details/82620485)
	- [NSProxy1](https://juejin.im/post/5afbca7bf265da0b8c25251d)

	- NSProxy可以帮助Objective-C间接的实现多重继承的功能。
	- OC 中一个类只有一个父类, 这就是单一继承, 但是我们可以用协议和 NSProxy 实现多继承





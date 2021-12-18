---
layout: post
title: CocoaPods
date: 2021-10-02 22:00:00 +0800
categories: 代码管理工具
tag: Objective-C/Swift
---

#### [官网](https://cocoapods.org/)
- Swift 和 Objective-C Cocoa 项目的包管理工具
- iOS 开发的必备工具

#### 安装 
1. CocoaPods 是用 Ruby 构建的,可以用 macOS 上的默认 Ruby 进行安装
2. ```sudo gem install cocoapods```

⚠️ ERROR: While executing gem ... (Gem::FilePermissionError).
	You don't have write permissions for the /usr/bin directory.
- ```sudo gem install -n /usr/local/bin fastlane```
- ```sudo gem install -n /usr/local/bin cocoapods```


#### [管理依赖](https://guides.cocoapods.org/syntax/podfile.html)
- 创建 Podfile 文件（XXXX.xcodeproj 所在文件夹）
- Podfile内容：

```
platform :ios, '10.0'
use_frameworks!

target 'Target Name' do
  pod 'AFNetworking', '~> 2.6'
  pod 'ORStackView', '~> 3.0'
  pod 'SwiftyJSON', '~> 2.3'

  target 'MyAppTests' do
    inherit! :search_paths
    pod 'OCMock', '~> 2.0.1'
  end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    puts "#{target.name}"
  end
end

end
```
- ```pod init```
- ```pod install```


#### [创建CocoaPods包](https://guides.cocoapods.org/syntax/podspec.html)
- ```
pod spec create LouisProject
edit Peanut.podspec
pod spec lint Peanut.podspec
```


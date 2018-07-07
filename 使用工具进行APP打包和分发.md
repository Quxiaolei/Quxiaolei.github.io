# 使用工具进行APP打包和分发

<!-- TOC -->

- [使用工具进行APP打包和分发](#%E4%BD%BF%E7%94%A8%E5%B7%A5%E5%85%B7%E8%BF%9B%E8%A1%8Capp%E6%89%93%E5%8C%85%E5%92%8C%E5%88%86%E5%8F%91)
    - [常见的xcodebuild命令](#%E5%B8%B8%E8%A7%81%E7%9A%84xcodebuild%E5%91%BD%E4%BB%A4)
        - [编译打包](#%E7%BC%96%E8%AF%91%E6%89%93%E5%8C%85)
        - [导出ipa包](#%E5%AF%BC%E5%87%BAipa%E5%8C%85)
        - [其他常见命令](#%E5%85%B6%E4%BB%96%E5%B8%B8%E8%A7%81%E5%91%BD%E4%BB%A4)
    - [IPA包的处理](#ipa%E5%8C%85%E7%9A%84%E5%A4%84%E7%90%86)
    - [使用xcrun命令重签名生成新的IPA包](#%E4%BD%BF%E7%94%A8xcrun%E5%91%BD%E4%BB%A4%E9%87%8D%E7%AD%BE%E5%90%8D%E7%94%9F%E6%88%90%E6%96%B0%E7%9A%84ipa%E5%8C%85)
    - [其他相关资料](#%E5%85%B6%E4%BB%96%E7%9B%B8%E5%85%B3%E8%B5%84%E6%96%99)

<!-- /TOC -->

## 常见的xcodebuild命令

### 编译打包

编译打包,产出archive包

```sh
# configuration参数一般为Debug和Release
xcodebuild [-project projectname] [-target targetname ...] [-configuration configurationname]
           [-sdk [sdkfullpath | sdkname]] [buildaction ...] [setting=value ...]
           [-userdefault=value ...]
xcodebuild -workspace workspacename -scheme schemename [-destination destinationspecifier]
          [-destination-timeout value] [-configuration configurationname]
          [-sdk [sdkfullpath | sdkname]] [buildaction ...] [setting=value ...]
          [-userdefault=value ...]
```

可以使用`-project`替换掉`-workspace`来对应project工程.

> 构建project工程时,可以指定对应的target.不指定时默认为第一个.  
构建workspace工程时,必须指定workspace和scheme参数.

### 导出ipa包

从编译过的archive包中导出ipa包

```sh
xcodebuild -exportArchive -archivePath <xcarchivepath> -exportPath <destinationpath> -exportOptionsPlist <plistpath>
```

需要在`plistpath`中手动进行ipa包的配置,其中`app-store`可以替换为`ad-hoc`,`enterprise`,`package`,`development`等.

```xml
<!-- exportOptionsPlist -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>method</key> <string>app-store</string>
        <key>uploadBitcode</key> <false/>
        <!-- 是否上传符号文件 -->
        <key>uploadSymbols</key> <false/>
    </dict>
</plist>
```

### 其他常见命令

```sh
# 列出当前工程的所有 Targets , Configurations 和 Schemes
xcodebuild -list
# clean当前编译目录
xcodebuild clean -workspace ${TARGET_NAME}.xcworkspace -scheme ${TARGET_NAME} -configuration ${BUILD_TYPE}

# 获取bundle_version
/usr/libexec/PlistBuddy -c 'Print CFBundleShortVersionString' ${plistPath}
# 设置bundle_version
/usr/libexec/PlistBuddy -c 'Set :CFBundleShortVersionString "${newValue}"' ${plistPath}
```

参考:

* [xcodebuild官方文档](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/xcodebuild.1.html)
* [xcodebuild命令简单使用](https://www.jianshu.com/p/88d9f2e57004)
* [xctool(facebook)](https://github.com/facebook/xctool)  
[Facebook xctool 的使用](https://www.jianshu.com/p/23646d85cfa1)
* [PlistBuddy简单使用](https://www.jianshu.com/p/2167f755c47e)

## IPA包的处理

可以使用altool命令对IPA进行验证和上传App Store.

altool命令路径:`/Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Versions/A/Support/altool`

```sh
# IPA包的验证
${altoolpath} --validate-app -f ${file} -t ${platform} -u ${username} [-p ${password}]
# IPA包的上传
${altoolpath} --upload-app -f ${file} -u ${username} [-p ${password}]
```

> 为了方便使用altool命令,可以命名别名:
> ```sh
> vim ~/.bash_profile
> # 指定altool别名
> alias altool="/Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Versions/A/Support/altool"
> source ~/.bash_profile
> ```
> 也可以建立 altool 命令的软链接：
>
> ```sh
> ln -s /Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Versions/A/Support/altool altool
> ```

还可以使用命令行上传至蒲公英和fir.im平台.

```sh
fir p '${ipaPath}' -T '${firToken}'
```

参考:

* [通过altool上传App的二进制文件](http://help.apple.com/itc/apploader/#/apdATD1E53-D1E1A1303-D1E53A1126)
* [Xcode一键发布到AppStore(使用Automator和altool)](http://blog.csdn.net/gukong/article/details/51578618)  
[workflow和BuildScript下载](https://github.com/Quxiaolei/Quxiaolei.github.io/tree/master/resources/Xcode%E4%B8%80%E9%94%AE%E5%8F%91%E5%B8%83%E5%88%B0AppStore(%E4%BD%BF%E7%94%A8Automator%E5%92%8Caltool))

## 使用xcrun命令重签名生成新的IPA包

支持在修改了app包的签名信息,相关资源后重签名生成ipa包.

```sh
/usr/bin/xcrun -sdk iphoneos PackageApplication -v ${appPath} -o ${ipaPath} --sign ${signInfo} --embed ${mobileprovisionPath}
```

参考:

[对app包重签名打包为ipa包](http://www.cnblogs.com/yesun/archive/2013/08/16/3261839.html)

## 其他相关资料

* [使用python脚本实现一键全自动打包](https://github.com/Quxiaolei/iOSAutoPackage)
* [iOS自动打包并发布脚本](https://github.com/carya/Util)
* [iOS项目自动打包脚本](https://github.com/hades0918/ipapy)
* [关于持续集成打包平台的Jenkins配置和构建脚本实现细节](http://debugtalk.com/post/iOS-Android-Packing-with-Jenkins-details/)
* [iOS：使用jenkins实现xcode自动打包](http://blog.csdn.net/u014641783/article/details/50866196)
* [iOS Shell脚本自动构建打包、发布、部署jenkins](https://www.jianshu.com/p/ad4a9c40ae59)
* [iOS--脚本配置Xcode Project（打包）](http://blog.csdn.net/chsadin/article/details/61192923)
* [xctool(facebook)](https://github.com/facebook/xctool)
* [fastlane](https://github.com/fastlane/fastlane)
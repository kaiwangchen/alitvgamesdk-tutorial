# 演示程序

本节介绍客户端工程。

> 由[支付流程](../tutorial/pay.md)可知单机游戏和网游的客户端接口差别不大。

除了 Eclipse 配置外， Demo 工程里只有 `AndroidManifest.xml`, 主 Activity 类 `com.example.alitvandroidsdk.DemoMainActivity` 和 Demo 专用的资源文件。

```
AliTvAndroidSDKDemo
  |-- libs/android-support-v4.jar
  |-- src/com/example/alitvandroidsdk
  |     |-- utils/TestConstants.java
  |     `-- DemoMainActivity.java
  |-- res
  |    |-- drawable-*/ic_launcher.png
  |    |-- layout/alidemo_activity_demo_main.xml
  |    `-- values/alidemo_strings.xml
  `-- AndroidManifest.xml
```

也就是说，你只需把 Lib 工程展开为游戏工程的平级目录，照抄 Demo 的 `project.properties` 这两项，就完成了游戏工程配置：

* AliTvAndroidSDKDemo/project.properties
```
manifestmerger.enabled=true
android.library.reference.1=../AliTvAndroidSDKLib
```

> 平台集成演示程序的应用凭据如下

| 参数    | 值
|---------|----------
| APP_KEY | 23167735
| APP_SECRET | 613ce365bdbc115677c013759c00ce55
| BAODIAN_SECRET | 23af0482e52bfa5073fe97893a8d0d00

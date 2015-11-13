# 工程配置

在 SDK 包里有 AliTvAndroidSDKDemo （简称 Demo ） 和 AliTvAndroidSDKLib （简称 Lib ）两个 Eclipse 工程。

将 Lib 工程展开为游戏工程的平级目录，照抄 Demo 工程的 `project.properties` 那两项，就完成了工程配置。

* AlitvSDKDemo/project.properties
```
manifestmerger.enabled=true
android.library.reference.1=../AlitvSDKLib
```

你没看错，这是 Android Manifest Merger 带来的便利。Lib 工程的 manifest 会被自动合并到 Demo 工程中。

否则，就要手工完成这个过程了（泪奔）。

附录中有 [Demo 工程](../appendix/demo.md)和 [Lib 工程](../appendix/lib.md)的结构说明，请自行参考。





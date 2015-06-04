# Lib 工程

除了 Eclipse 配置外，Lib 工程里只有`AndroidManifest.xml`（定义各种权限、Activity 、Service 和 Broadcast Receiver 等）、类库和 UI 资源。

```
AliTvAndroidSDKLib
  |-- libs/AliTvAndroidSDK-1.0.0.0.jar
  |-- res
  |    |-- drawable-*/*
  |    |-- layout/ali_de_bd_*.xml
  |    `-- values/ali_de_bd_*.xml
  `-- AndroidManifest.xml
```

事实上，Lib 中是类库工程：

* AliTvAndroidSDKLib/project.properties
```
android.library=true
```

虽然内容比较多，但是可以通过 Android Manifest Merger 自动地合并到主工程中（请参考 [Demo 工程](demo.md)用法）。

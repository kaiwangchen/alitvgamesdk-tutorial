# 初始化与清理

> 这里假设你的是单 Activity 游戏，不是的话，请在合理的地方调用这两个方法。

在 Main Activiy 类的 `onCreate` 和 `onDestroy` 方法里进行 SDK 初始化和清理：

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    AliTvSdk.init(APPKEY, APPSECRET, this);
    // ...
}
protected void onDestroy() {
    super.onDestroy();
    AliTvSdk.destroy();
    // ...
}
```

> `APPKEY` 和 `APPSECRET` 是**阿里电视游戏开放平台**分配给游戏的凭据，在开放平台创建游戏即可获得。不同的游戏用不同的凭据，若接入前期分配流程未走完，可以暂用[演示程序](appendix/demo.md)的凭据

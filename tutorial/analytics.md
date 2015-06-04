# 数据上报

阿里电视游戏平台支持两种数据的上报。第一种用于平台统计，第二种用于游戏行为分析。

## 平台统计

第一种用于平台统计。在进入/继续游戏和退出/暂停游戏时分别调用 `AliTvSdk.Report.enter()` 和 `AliTvSdk.Report.leave()` 。

> 这俩操作必须在 [SDK 初始化](bootstrap.md)完成后发起。

对于单 Activity 游戏而言，在主 Activity 类中定义：

```java
@override
protected void onStart() {
    super.onStart();
    AliTvSdk.Report.enter();
    // ...
}
@override
protected void onStop() {
    super.onStop();
    AliTvSdk.Report.leave();
    // ...
}
```

## 行为分析

游戏行为数据通过 submitLeaderboardScore 方法汇报给平台数据化运营支持系统，用于分析关卡难度、道具付费率等指标，支持深度运营。

```java
   // LeaderboardScoreType type = 某类行为。
   // String name 和 double value 是该行为分类下的开发者自定义参数
   // 注意，name 必须在平台运营系统里配置，请与阿里运营联系
   AliTvSdk.Report.submitLeaderboardScore(type, name, value);
```
> 注意，这里的 name 必须在平台运营支持系统里配置，否则上报的数据会被丢弃。

LeaderboardScoreType 枚举定义

| 枚举值              | 含义
|---------------------|-------------------
| METHOD_CUSTOMS_PASS | 关卡
| METHOD_LEVEL        | 等级
| METHOD_RESULT       | 进度
| METHOD_PROP         | 道具
| METHOD_STATE        | 状态
| METHOD_OTHER        | 其他

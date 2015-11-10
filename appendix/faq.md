# 常见问题

## 我能在安卓机上调试 YunOS 应用吗？

虽然 YunOS 应用开发和安卓应用开发非常相似，但一个应用的运行通常是依赖于系统服务的，安卓系统上没有这些服务，所以安卓机上几乎必然是无法调试 YunOS 应用的。在安卓机或模拟器上运行 YunOS 应用，除非该应用同时兼容 YunOS 和安卓（极少有这种情况），否则就会闪退。若遇到闪退，请务必仔细检查调试日志，日志里会给出具体原因或线索。


## 如何在 YunOS 盒子上安装/卸载游戏，查看日志？

YunOS TV 系统是兼容安卓的，用 `adb connect` 就可以连上设备。在“系统设置”/“网络设置” 里可以查到设备 IP ，在“系统设置”/“通用设置”里可以开启远程调试模式，剩下的你们都懂的。

adb 和 Eclipse 都可以安装 apk 。但如果 apk 太大的话，建议将开发机和设备都接入有线网络， 或者拿 U 盘拷过去装（在桌面的多媒体菜单进去可以找到 U 盘）。

## 如何识别 YunOS 环境？

千万不要基于 `android.os.Build.MODEL` 检测系统是否为 YunOS 。正确的方法是调用 `com.yunos.mc.utils.McUtil` 的 `isYunosSystem()` 方法。

## 如何在运行时唯一识别 YunOS 设备？

终端用户可以在“应用中心”里搜索 VIP ，安装 `YunOS VIP` 应用程序，启动它就可以看到 *32 个字符*的完整设备编号（短横线用于视觉分组，不是设备编号的组成字符）。注意， 在“系统设置”/“通用设置”/“系统信息”/“设备号”中显示的是 16 个字符的设备号，是不完整的。

开发人员也可以用这个函数来获取设备编号

```java
public static String getUuid(){
    try {
        Class<?> cloudUuid = Class.forName("com.yunos.baseservice.clouduuid.CloudUUID"); 
        Method m = cloudUuid.getMethod("getCloudUUID");
        String result = (String)m.invoke(null);
        return result;
    }
    catch (Exception e) { return "false"; }
}

```

## 集成支付回调时遇到 SIGNATURE_EXPIRED

首先，请确认已经阅读[支付流程](../tutorial/pay.md)。

这个响应是这样的吧：

```
 {"app_order_id":"...","error_code":"SIGNATURE_EXPIRED","is_success":"F","msg":"请 求签名过期"} 
 
 ```

注意，请求参数中有个 `ts` 参数表示请求时间戳。阿里服务器会检查这个时间戳（*毫秒*）， 如果与当前时间相差太大的话（几分钟），它就会报这个错误。
出现这种问题的情况一般有两种：其一是你的服务器时间漂移了，这时要提醒运维人员保持服务器时钟同步。其二是你可能正在手工模拟请求，这时你就得选个合适的 ts 值了，别和发出请求的时间点偏差太大。


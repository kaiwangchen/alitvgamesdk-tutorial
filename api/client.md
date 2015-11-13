## 客户端 API

```java
public class AliTvSdk {

    // 初始化与释放
    public static void init(Context context, String appKey, String appSecret, IInitListener initListener, IAuthListener authListener);
    public static void destroy();

    // 支付
    public static void pay(String title, int amount, IPayListener payListener);
    public static void payFromServer(String title, int amount, String orderId, String notifyUrl, IPayListener payListener);

    // 数据上报
    public class Report {
        public static void submitLeaderboardScore(LeaderboardScoreType type, String categoryName, double amount);
        public static void enter();
        public static void leave();
    }
    
    //账号相关
    public static class Account {
        //检查当前用户是否已经授权
        public static boolean isAuth();
        //检查当前用户是否已经授权，如果没有授权，会拉起扫码授权页面
        public static boolean checkAuthAndLogin();
        //切换账号。拉起扫码登陆页面，不论当前是否已经有用户登陆
        public static void changeAccount() ;
        //获取当前授权的用户信息 如果当前用户没有授权，会返回“未授权”的错误
        public static void getUserInfo(IGetUserinfoListener infoListener) ;
        //检查当前设备是否已授权
        public static void checkDeviceAuth(IdeviceAuthListener infoListener) ;
        //获取yunOS盒子的uuid
        public static String getUUID() ;

    }
    
    //WEB相关
    public static class Web {
        // 启动时打开推广页，需要阻塞游戏，等到onWebClose的回调后再继续
        public static boolean openWebviewOnStart(IWebListener listener, HashMap<String, String> params) ;
        // 退出时打开推广页，需要阻塞游戏，等到onWebClose的回调后再继续
        public static boolean openWebviewOnExit(IWebListener listener, HashMap<String, String> params)  ;
        //商品外露二维码的URL
        public static String getQRUrl() ;
    }
    
    // 其他
    public static String getSdkVersion();
    public static void logSwitch(boolean on);
}

public interface IPayListener {
	public void onSuccess(String title, int amount);
	public void onCancel(String title, int amount);
	public void onError(String title, int amount, String errMsg);
}

public enum LeaderboardScoreType {
    METHOD_CUSTOMS_PASS("customs pass"), // 关卡类
    METHOD_LEVEL("level"), // 等级类
    METHOD_RESULT("result"), // 进度类
    METHOD_PROP("prop"), // 道具类
    METHOD_STATE("state"), // 状态类
    METHOD_OTHER("other"); // 其他
}

```




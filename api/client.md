## 客户端 API

```java
public class AliTvSdk {

    // 初始化与释放
    public static void init(String appKey, String appSecret, Context applicationContext);
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




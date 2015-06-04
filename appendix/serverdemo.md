# 服务端 Demo

本节介绍[服务端附加流程](../tutorial/pay.md#服务端附加流程)的 Java 实现逻辑。

> 由[支付流程](../tutorial/pay.md)可知服务端附加流程只有特定条件下才触发。

> `BAODIAN_SECRET` 是应用凭据的组成部分，由阿里电视游戏开放平台分配。

```java
protected void doGet(HttpServletRequest request,
                HttpServletResponse response) throws ServletException, IOException {
        String responseBody;
        try {
                BaodianConsumptionNotification notification = BaodianConsumptionNotification.buildFrom(request);

                if (notification.verify(BAODIAN_SECRET)) {
                        throw new RuntimeException("Illegal signature");
                }

                boolean isSuccess = notification.isSuccess();
                String appOrderId = notification.getAppOrderId();

                if (isSuccess) {
                        // find the order by appOrderId and verify state
                        // find item by appOrderId
                        // deliever the item to the player
                }
                else {
                        // handle the failure
                }
                // responseBody = notification.reject("custom message");
                responseBody = notification.accept();
        } catch (IllegalArgumentException e) {
                responseBody = BaodianConsumptionNotification.reject(request, e.getMessage());
        }

        request.setAttribute("result", responseBody);
        RequestDispatcher dispatcher = request.getRequestDispatcher("result.jsp");
        dispatcher.forward(request, response);
}

```

XMLHttpRequest (**XHR**) is **a JavaScript API to create AJAX requests**.

1. doPreFailBackCheck:https://csgdisqa.qa.webex.com/gfc/failover/doPreFailBackCheck
2. getCheckTypes:https://csgdisqa.qa.webex.com/gfc/failover/getCheckTypes
3. doFailoverback
3. searchByComponentIds
3. getFOBOperations:https://csgdisqa.qa.webex.com/gfc/failover/getFOBOperations?sessionIdStr=bc4b90f3174d40c88efb928106bf6dfb617230,&componentIdsStr=359,181,183,185&failoverbackMark=failover&firstVisit=false
4. report: https://csgdisqa.qa.webex.com/gfc/failover/report?sessionIdStr=bc4b90f3174d40c88efb928106bf6dfb617230,



PayLoad:

{userName: "senwan", componentIDs: "s", isfailover: 0, reason: "test",…}

1. 1. componentIDs: "7922,7923,7924,7925"
   2. dcName: ""
   3. estFailbackTime: "2022-03-15 01:48 am"
   4. isDcFailOut: false
   5. isMaintain: 0
   6. isMct: 0
   7. isPoolHealthCheck: 1
   8. isSVTA: 1
   9. isfailover: 0
   10. planId: -1
   11. planType: 1
   12. reason: "test"
   13. userName: "senwan"
   14. woInfo: "{\"2715\":\"%undefined\"}"







- **Shareplex Delay Check** 
+ **Change Window Check** 
- **Peak Time Check** 
+ **Repeat Failover Check **
+ **Maintain Status Check //  L286**
- **Plugin Check** 
- **Change Process Status Check** 
+ **Backup/GSB Status Check** 
+ **Vip Check** 
+ **Different Ticket Number Check** 
+ **Change Status Check** 



![image-20220316095201632](/Users/jason/Library/Application Support/typora-user-images/image-20220316095201632.png)

pre-check :

press **failover/failback** button - kafka works(KafkaConsumerListener.preCheckMessage)



precheck 报500, 确实是kafka消费太长造成的, 现在pre-check的逻辑就是先将pre-check的信息发送到kafka, 然后由wos-gfc-failover去做precheck, 然后将precheck的状态写入到redis里面,

前端点击go/precheck 按钮都只是触发

在获取precheck status时回去redis里面查询precheck的状态, redis里没有, 就会报500



```
public static final String INVA = "INVA";
public static final String MANUAL = "MANU";
public static final String AUTO = "AUTO";
public static final String PRIM = "PRIM";
public static final String STICK_AUTO = "MANP";
public static final String PARTLY = "PARTLY";
```

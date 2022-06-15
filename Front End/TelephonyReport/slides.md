### Telephony Failover/Failback Components

**MACC --**  **M**ulti-media **A**dvance **C**luster **C**ontroller

**TAS** --  **T**elephone **A**nswering **S**ystem. 

**TS** --  **T**elephone **S**erver



---

### Failover PayLoad




•componentIDs: "7922,7923,7924,7925"

•dcName: ""

•estFailbackTime: "2022-03-15 01:48 am"

•isDcFailOut: false

•isMaintain: 0

•isMct: 0

•isPoolHealthCheck: 1

•isSVTA: 1

•isfailover: 0

•planId: -1

•planType: 1

•reason: "test"

•userName: "senwan"

•woInfo: "{"2715":"%undefined"}"



---



### **XMLHttpRequest** **process**

•doPreFailBackCheck

•getCheckTypes

•doFailoverback

•searchByComponentIds

•getFOBOperations

•report      

<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220407130642628.png" alt="image-20220407130642628" style="zoom:67%;" />



---



### Failover Process

- Trigger: Front-end click ”PreChech” or “Go”



- Preckeck(kafka.send) : 

  - New precheck for checkManager - Do 11 types check

  - PreCheckWorkThread()



- Failover operation(kafka.send)
  - Report 



---



### **Prechck Types**



- Shareplex Delay Check 

  - *validate* *shareplex* *delay to plugin:J2EE/J2EE_GCN* 

  - *within 30mins*

- Change Window Check – process should be inCkeckTime

  - *getChangeWindowTime* *–* *byLocation**/**byClusterId*

  - *inCheckTime*

- Peak Time Check 
  - start-now-end

- Repeat Failover Check 
  - isOngoing? Failover&onGSB? Failback&PRI?

- Change Status Check
  - callSnowApiForChangeChecking - ci_item.name, task.sys_id, task.number are not null

- Maintain Status Check

  - matchedRuleWith("J2EE", "J2EE_GCN", "PHP_GCN", "PHP")?

  - isVerifyGsb?

  - checkFloatVip, pingable?





---



- Plugin Check

  - failback && _isOnPrim?

  - oldLogic? 

  - isMACCTAS? 

  - Check shh(server, port, command…)

  - check ts(ts.ssh.failoverCommand,…)

  - runCommmandBySSH()

- Change Process Status Check
  - validateWOFromSNOW(): call SNOW restful API

- Backup/GSB Status Check
  - operationType = Failover?

- Vip Check

  - zoneCheckRule.matchedRule

  - "GSLB_NEWGCN" =pluginName?

  - PingTool.isTcpable?

- Different Ticket Number Check
  - Compare failback with lastestOperationType, not failover = pass



---



### PreCheckWorkThread

#### Put components into PreCheckWorkThread

```java
    public List<PreCheckDetail> findCheckResultsBySessionIdAndComponentId (String runId, String componentId) {
        QueryObject query = QueryObject.getInstance()
                .addFilter("runId", runId)
                .addFilter("componentId", componentId)
                .addFilter("level", MatchType.GT, 0)
                .orderBy("componentName,createTime", "asc");
        return this.list(query);
    }
```



---

### Failoverback operation process

- _setComponentOrder

  - telephony.failover.order=TS:TAS:MACC:CMS:ASR

  - telephony.failback.order=MACC:TAS:CMS:TS:ASR

- new FailoverbackWorkThread – call() return (callable)
  - IControlPlugin controlPlugin = ControlPluginManager.getInstance().findPluginByName(pluginName);
  - telephonyPlugin.doProcess()
  - TAS,TS,MACC interval
- telephonyTaskExecutor.submit(callable)
- _checkOperationOK
  - operationService.update(entity)

- mctServiceMaintain

- latch.await :
  - telephony.failover.session.timeout

- _shutdownTask
```java
public GcnServerStorage jsonToMap(String params){
    GcnServerStorage gcnServerStorage = new GcnServerStorage() ;
    Map<String,Object> paraMap = gson.fromJson(params,Map.class);
    Map<String,String> gcnServerMap = (Map<String, String>) paraMap.get("gcnServer");
    String gcnIp = gcnServerMap.get("gcnIp");
    String serverId = gcnServerMap.get("id");
    String path = (String) paraMap.get("path");
    String storagePath = (String) paraMap.get("storagePath");
    log.info("serverId:{},path:{},storagePath{},gcnIp{}:",serverId,path,storagePath,gcnIp);
    if (serverId != null){
        gcnServerStorage.setGcnServerId(serverId);
        gcnServerStorage.setStoragePath(storagePath);
        gcnServerStorage.setPath(path);
        gcnServerStorage.setStatus("unknow");
    }else {
        log.error("Not found gcnIp{} in Gcn Server",gcnIp);
    }
    return gcnServerStorage;
}
```
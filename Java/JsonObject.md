JSON

{} 双括号表示对象

[] 中括号表示[数组](https://so.csdn.net/so/search?q=数组&spm=1001.2101.3001.7020)



```javascript
{"filesystem_detail": [{"fs_name": "test_filesystem", "client": "10.131.79.0/24", "size": 1}, 
                       {"fs_name": "test_fs_001", "client": "10.131.79.0/24", "size": 10}, 
                       {"fs_name": "test_fs_002", "client": "10.131.79.0/24", "size": 2}, 
                       {"fs_name": "test_fs_0025", "client": "10.131.79.0/24", "size": 1}, 
                       {"fs_name": "test_fs_003", "client": "10.131.79.0/24", "size": 2}, 
                       {"fs_name": "test_fs_bts_v1_terminate", "client": "10.131.79.0/24", "size": 1}, 
                       {"fs_name": "test_fs_clients", "client": "10.131.79.0/24", "size": 1},
                       {"fs_name": "test_fs_without_client", "client": "10.131.79.0/24", "size": 1},
                       {"fs_name": "test_fs_without_client1", "client": "10.131.79.0/24", "size": 1}, 
                    	 {"fs_name": "test_migration_filesystem", "client": "10.131.79.0/24", "size": 1},
                       {"fs_name": "test_sjcl1_filesystem", "client": "10.131.79.0/24", "size": 2}, 
                       {"fs_name": "test_synthetic_123454321", "client": "10.131.79.0/24", "size": 5}, 
                       {"fs_name": "test_vol_no_clients", "client": "10.131.79.0/24", "size": 1024}, 
                       {"fs_name": "testxxx001", "client": "10.131.79.0/24", "size": 1},
                       {"fs_name": "to_increase_utilization", "client": "10.131.79.0/24", "size": 300},
                       {"fs_name": "wap_elk", "client": "10.131.79.0/24", "size": 8192}],
 "mount_fqdn": ["sjcl1fbld01-nfs01.webex.com"]}
```

方法一： private Gson gson = new GsonBuilder().disableHtmlEscaping().create();

```java
        JsonObject jsonObject = gson.fromJson(content, JsonObject.class);
        String mountFqdn = jsonObject.get("mount_fqdn").getAsString();
        logger.info("GFC mount fqdn:", mountFqdn);
        JsonArray fileSystemObject = jsonObject.get("filesystem_detail").getAsJsonArray();
        JsonObject row = null;
        for (int i = 0; i < fileSystemObject.size(); i++) {
            row = fileSystemObject.get(i).getAsJsonObject();
            Map<String,String> map = new HashMap<>();
            map.put("fsName",row.get("fs_name").getAsString());
            map.put("size",row.get("size").getAsString());
            results.add(map);
        }
```



方法二：

```java
String content = response.get("RESULT_CONTENT");

content = content.replace("[","").replace("]","");//去除[]字符
JSONObject jsonObject = new JSONObject(content);

String clientSubnet = jsonObject.getString("network");
String service = jsonObject.getBoolean("service");
String dcName = jsonObject.getInt("dc");
```
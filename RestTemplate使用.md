```java
public static <T> T  deleteByIds(String path, Object entity, Class<T> clazz) {
    try {
            try {
                ResponseEntity<ServiceResult<JsonNode>> rsp = restTemplate.exchange(path, HttpMethod.DELETE, null,
                        new ParameterizedTypeReference<ServiceResult<JsonNode>>() {
                        });
                Integer results = Objects.requireNonNull(rsp.getBody()).getCode();
                return (T) results;
            } catch (Exception e) {
                logger.error("Failed call api {}", path, e);
                throw e;
            }
    } catch (Exception e) {
        logger.error("Failed call api {}", path, e);
        throw e;
    }
}
```

```java
public static <T> T post(String path, Object entity, Class<T> clazz) {
    try {
        ResponseEntity<ServiceResult<JsonNode>> rsp = restTemplate.exchange(path, HttpMethod.POST, new HttpEntity<>(entity),
                new ParameterizedTypeReference<ServiceResult<JsonNode>>() {
                });
        JsonNode results = Objects.requireNonNull(rsp.getBody()).getResults();
        return JsonUtils.readValue(results, clazz);
    } catch (Exception e) {
        logger.error("Failed call api {}", path, e);
        throw e;
    }
}
```



Path: 指api的url

entity：把需要传过去的参数放进去，需要跟api的request参数类型保持i一致，如果没有参数，可以为NULL，比如

Class<T> clazz : 指返回值类型 ： 如，Integer a = XXX.post()

**Delete**:

```java

​		requestUrl: localhost:8080/XXX/XXX/{ids}
​		entity: null
​		class: Integer.class
Integer deleteResult = ServiceInvoke.deleteByIds(deleteAllProdLogonRoles,null,Integer.class);

@DeleteMapping("/deleteByIds/{ids}")
@ResponseBody
public Object deleteByIds(@PathVariable String ids) {
    List<String> stringList = Arrays.asList(ids.split(","));
    this.service.deleteAllById(stringList);
    return RestUtils.ok();
}
```



**POST**: 如果有请求参数，注意！！！ 要在controller方法上加**@RequestBody**注解

```jade
@PostMapping("")
@ResponseBody
public Object save(@RequestBody String body) {
    return super.save(body);
}
```
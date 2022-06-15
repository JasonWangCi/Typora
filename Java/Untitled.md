```
@Transient: 被注解的内容，不被序列化，也就是创建的对象不会被变成字节。
```

```
@JsonIgnore: 被注解的内容，不在Json中出现
```



```
@NotFound(action = NotFoundAction.IGNORE)
使用hibernate 注解配置实体类的关联关系，在many-to-one,one-to-one等关联中，一边引用自另一边的属性，如果属性值为某某的数据在数据库不存在了，hibernate默认会抛出异常。解决此问题，加上如下注解就可以了： 
意思是找不到引用的外键数据时忽略，NotFound默认是exception 
```

hibernate
---
title: PG && MyBatis中使用TypeHandler导致json字段异常赋值的线程安全问题
slug: 
date: 2023-11-10 00:00:00+0000
# image: BWeLyHqW.jpg
categories:
    - 技术分享
tags:
    - PostgreSQL
weight: 2       # You can add weight to some posts to override the default sorting (date descending)
---

在新手时期不知道哪里抄来的代码，在低并发的时候没事，在高并发的下出问题了，浪费了不少时间记录下

```java
public class JsonTypeHandler<T extends Object> extends BaseTypeHandler<T> {

    // ... 其他代码省略

    private static final PGobject jsonObject = new PGobject();

    public JsonTypeHandler() {
    }

    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, T parameter, JdbcType jdbcType) throws SQLException {
        
        jsonObject.setType("json");
        ObjectMapper mapper = new ObjectMapper();
        // ... 省略其他操作
        ps.setObject(i, jsonObject);
    }

    // ... 省略其他方法
}
```
在上面的代码中，创建了一个静态的PGobject对象jsonObject，并在setNonNullParameter方法中对其进行操作。然而，静态变量在多线程环境中可能会导致线程安全问题，因为多个线程可能会同时访问和修改这个静态变量。

解决方法是将PGobject对象的创建和操作放在setNonNullParameter方法内部，这样每次调用setNonNullParameter方法时都会创建一个新的PGobject对象，避免多线程共享同一个对象导致的线程安全问题。
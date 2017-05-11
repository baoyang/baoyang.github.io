---
layout: post
title: java应用中避免NPE技巧
categories: Java
description: java 避免NullPointerException技巧
keywords: NullPointerException , java
---

## 为什么避免java空指针的几点思考:

 1. Java应用中抛出的空指针异常是解决空指针的最好方式，也是写出能顺利工作的健壮程序的关键。
 2. 减少代码中非空判断数量。
 3. 返回null容易混淆业务意图。
 
## 常用技巧及实践

 1. [Java中有关Null的9件事](http://www.importnew.com/14229.html)
 
 2. [技巧和最佳实践](http://www.importnew.com/7268.html)
 
 3. 使用工具类优化代码
 
    * 使用common.lang3包中String相关判断
    * 使用Objects类（Java 7中原有的）
    * [使用Optional类型（Java 8中新引入的）](https://teakki.com/p/57df78e01201d4c1629bad49)  
        包含Optional<T>、OptionalDouble、OptionalInt、OptionalLong
---
layout: post
title: 深入理解java异常
categories: Java
description: java异常机制分析。
keywords: exception , java
---
## [Java异常简介及使用](http://www.runoob.com/java/java-exceptions.html)

## Java异常类层次结构图:

![Java异常类层次结构图](/images/posts/exception.jpg)

## Java异常使用注意事项

1. finally 块：无论是否捕获或处理异常，finally块里的语句都会被执行。当在try块或catch块中遇到return语句时，finally语句块将在方法返回之前被执行。注意以下情况：
    * 在前面的代码中用了System.exit()退出程序，finally块不会被执行
    * 程序所在的线程死亡，finally块不会被执行
    * 关闭CPU，finally块不会被执行
    * finally语句块不应该出现return和throw语句(出现会将覆盖try和catch中的中止)
    * 有时为了简单会忽略掉catch语句后的代码，一旦try运行过程中出现了异常，并且finally也出现异常，程序异常就会忽略，try中异常信息丢失。

2. catch 关键字后面括号中的Throwable -> Exception类型的参数e，通常异常处理常用3个函数来获取异常的有关信息:
    * e.getMessage()：用于输出错误性质
    * e.getCause()：返回抛出异常的原因,如果 cause 不存在或未知，则返回 null
    * e.getMessage()：返回异常的消息信息
    * e.printStackTrace()：对象的堆栈跟踪输出至错误输出流，作为字段 System.err的值
    
3. 在继承了某个类时，如果父类中某个方法（public或者protected）有异常说明，子类在覆盖方法时，异常说明只能是父类的一样的异常说明或者无异常说明，不能添加父类方法没有的异常说明。

4. JDK1.7新特性补充
    * 同时捕获多个异常,这种情况不能将RuntimeException放在首位，编译不能通过。
    ```
    try {
        Integer.parseInt("Hello");
    } catch (NumberFormatException | RuntimeException e) {

    }
    ```
    * try-with-resources它可以实现自动释放功能
    ```
    public String read(String filename) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
             StringBuilder builder = new StringBuilder();
             String line = null;
             while((line=reader.readLine())!=null){
                 builder.append(line);
                 builder.append(String.format("%n"));
             }
             return builder.toString();
        }
    }
    
    ```
     
## Java异常性能

![Java异常性能影响](/images/posts/exception2.jpg)
    
    仅在异常情况下使用异常,在可恢复的异常情况下使用异常.
    异常处理的性能成本非常高，每个Java程序员在开发时都应牢记这句话.
    创建一个异常非常慢，抛出一个异常又会消耗1~5ms，当一个异常在应用的多个层级之间传递时，会拖累整个应用的性能.
    

## 异常处理建议

[《Effective Java》中关于异常处理的几条建议](http://www.cnblogs.com/skywang12345/p/3544287.html)

[《Java Puzzles》中关于异常的几个谜题](http://www.cnblogs.com/skywang12345/p/3544353.html)
---
title: 学习mybatis的记录初体验
date: 2019-01-22 17:39:26
tags: 学习经历
categories: SSM学习ing
---
今天刚开始学习mybatis，听了mybatis和hibernate之间的比较，大致是这样的：
一、灵活性：mybatis可以直接使用SQL语句，灵活性较高
二、效率性：mybatis直接用SQL，效率高（hibernate使用hql语句，底层需要转换成
SQL来操作数据库，时间上有消耗）

<!--more-->

三、移植性：hibernate更好，因为hibernate用配置文件关联数据库，用hql语句与
数据库无直接关系

听完课学了大概一个小时，弄懂了mybatis开发的大致流程，但是轮到我自己动手操
作的时候，一直保空指针异常，初学者总是遇到这个问题，弄了我将近2个多小时，
最后才知道原来要使用SQL语句的时候，SqlSession.insert(1,2)传的参数弄错了，
第一个参数要传的是mapper.xml的命名空间加定义的id来定位，第二个参数就是你
要传的值。

总的来说，我还是觉得学习编程，理论固然重要，但是动手能力也很重要，编码能力
也很重要，这就是我学习mybatis的初次体验。
---
title: Spring（一）
copyright: true
date: 2020-04-27 16:36:15
tags: Spring
categories: 源码解读
---

## 1、Spring的历史简介

- Spring：翻译成春天，代表给软件行业带来了春天~
- 2002年，首次推出了Spring框架的雏形：interface21框架~
- Spring框架即以interface21框架为基础，经过重新设计，并不断丰富其内涵，于2004年3月24日发布了1.0正式版~
- **Rod Johnson**，Spring Framework创始人，著名作者。很难想象Rod Johnson的学历，真的让好多人大吃一惊，他是悉尼大学的博士，然而他的专业不是计算机，而是音乐学~
- Spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合了现有的技术框架~

<!--more-->

**从以前的SSH到现在的SSM都需要Spring来整合，因为Spring框架就是一个大杂烩，用来解放程序员的。**

- SSH：Struct2 + Spring + Hibernate
- SSM：SpringMVC + Spring + Mybatis

## 2、Spring的优点

- Spring是一个开源免费的框架（容器）~
- Spring是一个轻量级的、非侵入式的框架~
- 控制反转（IOC），面向切面编程（AOP）~
- 支持事务的处理，对框架整合的支持~

**总结一句话：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架~**

## 3、Spring的七大模块

![img](https://pic2.zhimg.com/80/v2-6219164646cd5a15e162d8ff1debf3fd_720w.jpg)

**核心容器(Spring core)**

核心容器提供Spring框架的基本功能。Spring以bean的方式组织和管理Java应用中的各个组件及其关系。Spring使用BeanFactory来产生和管理Bean，它是工厂模式的实现。BeanFactory使用控制反转(IoC)模式将应用的配置和依赖性规范与实际的应用程序代码分开。BeanFactory使用依赖注入的方式提供给组件依赖。

**Spring上下文(Spring context)**

Spring上下文是一个配置文件，向Spring框架提供上下文信息。Spring上下文包括企业服务，如JNDI、EJB、电子邮件、国际化、校验和调度功能。

**Spring面向切面编程(Spring AOP)**

通过配置管理特性，Spring AOP 模块直接将面向方面的编程功能集成到了 Spring框架中。所以，可以很容易地使 Spring框架管理的任何对象支持 AOP。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖 EJB 组件，就可以将声明性事务管理集成到应用程序中。

**Spring DAO模块**

DAO模式主要目的是将持久层相关问题与一般的的业务规则和工作流隔离开来。Spring 中的DAO提供一致的方式访问数据库，不管采用何种持久化技术，Spring都提供一直的编程模型。Spring还对不同的持久层技术提供一致的DAO方式的异常层次结构。

**Spring ORM模块**

Spring 与所有的主要的ORM映射框架都集成的很好，包括Hibernate、JDO实现、TopLink和IBatis SQL Map等。Spring为所有的这些框架提供了模板之类的辅助类，达成了一致的编程风格。

**Spring Web模块**

Web上下文模块建立在应用程序上下文模块之上，为基于Web的应用程序提供了上下文。Web层使用Web层框架，可选的，可以是Spring自己的MVC框架，或者提供的Web框架，如Struts、Webwork、tapestry和jsf。

**Spring MVC框架(Spring WebMVC)**

MVC框架是一个全功能的构建Web应用程序的MVC实现。通过策略接口，MVC框架变成为高度可配置的。Spring的MVC框架提供清晰的角色划分：控制器、验证器、命令对象、表单对象和模型对象、分发器、处理器映射和视图解析器。Spring支持多种视图技术。

## 4、Spring的拓展

在Spring的官网介绍：现代化的Java开发！说白了就是基于Spring的开发！

![img](https://pic2.zhimg.com/80/v2-f79ce65e11b0d34113369ae8d7ca1f71_720w.jpg)

- Spring Boot

- - 一个快速开发的脚手架。
  - 基于SpringBoot可以快速的开发单个微服务。
  - 约定大于配置。

- Spring Cloud

- - SpringCloud是基于SpringBoot实现的。

**今天的Spring就介绍到这里，下次来详细讲一下控制反转（IOC）和面向切面编程（AOP）。**
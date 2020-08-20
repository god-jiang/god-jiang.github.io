---
title: python爬虫入门笔记
copyright: true
date: 2020-01-22 12:09:27
tags: 爬虫
categories: python学习
---

## 背景

> 由于这两天在家大扫除贴对联准备过年，所以刷题的机会少了许多，我也就放松放松一下，不写题解了，哈哈。由于python语言越来越火热，虽然我是走Java后台开发，但是也被python给吸引住了。所以这几天我学习了一下python的爬虫入门，记录一下我学习python爬虫的经历吧。

<!--more-->

## 基础准备

- 我觉得要学习一个新的东西的时候，兴趣是最重要的一个因素。因为我本人很喜欢看小说，然后又是技术控，所以想试一下用python爬虫爬取我喜欢的小说（刺激~~~）
- 有一门面向对象的编程语言基础，例如我熟悉Java，然后入手python就觉得还可以（有点自恋~~~）
- 装python3.x的环境（因为我是用python3.8）,觉得麻烦可以直接装anaconda也行。我是因为毕业设计做深度学习都有安装，不过我还是用自己安装的python3.8来做爬虫。

## 开发爬虫的步骤

- 目标数据（网站、页面）
- 分析数据加载流程（分析目标数据所对应的url）
- 下载数据到本地
- 清洗，处理数据
- 数据持久化

**因为我喜欢看伏天氏，所以爬取的是笔趣阁里面的伏天氏小说，以此来记录python爬虫的入门。**

## **爬取数据**

1. 需要导入requests库，没有这个库可以直接在win+r的cmd里面输入pip install requests下载即可
2. 需要学习正则表达式来帮助我们爬取想要的数据

## 代码（加注释）

```python3
#!/usr/bin/env python 
# -*- coding:utf-8 -*-

# 导入requests库，前提是已安装requests库，可以在命令提示符窗口输入pip install requests得到，
import requests
# 爬虫必备的正则模块
import re

# url存放要爬取的网页地址
url = 'https://www.jupindai.com/book/87.html'

# requests发起get请求url，返回response
response = requests.get(url)
# 设置网页响应回来的编码格式
response.encoding = 'gbk'
# 拿到网页的html
html = response.text;
# 拿到小说的名字
title = re.findall(r'<meta name="apple-mobile-web-app-title" content="(.*?)">', html)[0]
# print(title)
# 新建一个文件保存小说
fb = open('%s.txt' % title, 'w', encoding='utf-8')
# print(html)

# 获取对应的章节List
dl = re.findall(
    r'<dl class="panel-body panel-chapterlist">.*?</div>',
    html, re.S)[1]
# 获取对应的title和href
chapter_info_list = re.findall(r'<a href="(.*?)" title="(.*?)">(.*?)</a>', dl)
# print(chapter_info_list)

# 循环每一个chapter_info_list，分别下载
for chapter_info in chapter_info_list:
    chapter_url, none, chapter_title = chapter_info
    chapter_url = 'https://www.jupindai.com%s' %\
                  chapter_url
    # 下载
    chapter_response = requests.get(chapter_url)
    chapter_response.encoding = 'gbk'
    chapter_html = chapter_response.text
    # print(chapter_url, chapter_title)
    # 提取章节内容
    chapter_content = re.findall(r'<div class="panel-body" id="htmlContent">(.*?)</div>', chapter_html, re.S)[0]
    # 清洗数据
    chapter_content = str(chapter_content).replace(' ', '')
    chapter_content = str(chapter_content).replace('&nbsp;', '')
    chapter_content = str(chapter_content).replace('<br/>', '')
    # 回车
    chapter_content = str(chapter_content).replace('\r', '')
    # 换行
    chapter_content = str(chapter_content).replace('\n', '')
    # print(chapter_content)
    # 数据持久化
    fb.write(chapter_title)
    fb.write('\n')
    fb.write(chapter_content)
    fb.write('\n')
    print(chapter_url)
```

## 运行部分截图

![img](/images/爬虫/3.jpg)

------

**PS：由于写代码的时候是一边写一边测试，所以中间挺多过程你们可能看着有点懵，可以尝试着自己写一下来熟悉一下整个过程。这个应该就是最简单的一个python爬虫入门了吧，因为喜欢看小说，刚好现在在看《伏天氏》，就试着爬取一下数据，结果还不错，就是过程可能有点坎坷，毕竟本身我就是学Java出身，python也是半吊子，要不是刚好毕业设计做深度学习，我估计连python的语法都不会吧（哈哈），觉得对你有点帮助的点点赞，谢谢你们的支持了。**
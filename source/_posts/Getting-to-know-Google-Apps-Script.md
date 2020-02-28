---
title: 初识Google Apps Script
tags:
  - GAS
  - Javascript
  - API
  - Sheets
categories:
  - GAS
date: 2020-02-01 10:04:56
---


# 先来认识几个概念
为对抗Microsoft Office系列产品在办公领域的统治地位, 从2004年推出Gmail开始, Google着手建立了一系列的基于云端运行的在线工具, 从此开创了一条与传统Office客户端运行软件不同的发展路线, 让用户利用浏览器就能随时随地在云端办公. <!-- more -->

今天的人们已经越来越接受云端办公的理念, 也有越来越多的人体会到云端以及整合所带来的收益, 就连老对手Microsoft也与时俱进, 把Office搬上云端, 推出Office365这样的在线服务.

# Google Apps 有什么?
今天的 Google Apps 包含了一大堆人们耳熟能详的应用工具:

|| App | Remark |
|----| ----- | ----- |
|![](https://www.gstatic.com/images/branding/product/2x/sheets_48dp.png)| Sheets | Google表格, 类似MS Excel |
|![](https://www.gstatic.com/images/branding/product/2x/docs_48dp.png)| Docs | Google文档, 类似MS Word |
|![](https://www.gstatic.com/images/branding/product/2x/slides_48dp.png)| Slides | Google幻灯片, 类似MSMS PPT |
|![](https://www.gstatic.com/images/branding/product/2x/forms_48dp.png)| Forms | Google表单 |
|![](https://www.gstatic.com/images/branding/product/2x/drive_48dp.png)| Driver | Google云盘 |
|![](https://www.gstatic.com/images/branding/product/2x/gmail_48dp.png)| Gmail | Google电子邮件, 类似MS hotmail |
|![](https://www.gstatic.com/images/branding/product/2x/calendar_48dp.png)| Calendar | Google日历, 类似MS outlook |
|![](https://www.gstatic.com/images/branding/product/2x/chat_48dp.png)| Hangouts | 环聊, 初衷可能是MS Skype |
|![](https://www.gstatic.com/images/branding/product/2x/sites_48dp.png)| Sites | Google站点, 类似MS Sharepoints |
|![](https://www.gstatic.com/images/branding/product/2x/contacts_48dp.png)| Contacts | Google联系人 |
|![](https://www.gstatic.com/images/branding/product/2x/groups_48dp.png)| Groups | Google群组 |
|![](https://www.gstatic.com/images/branding/product/2x/maps_48dp.png)| Maps | Google地图 |
|![](https://www.gstatic.com/images/branding/product/2x/translate_48dp.png)| Translate | Google翻译 |

> 除了给个人提供的免费版之外, 还发展了面向企业的收费版本, G Suit, 包括上述Google Apps之外, 还包含一些企业域名的服务. 人均5$/month, 从提供服务的内容来看, 价格确实不贵

 
# Google Apps Script 是什么?
为了能够满足用户对于Google Apps的更加个性化二次开发需求, Google推出了 ***Google Apps Scripts (GAS)***.

GAS是一个快速应用开发平台, 直接内嵌在所有Google Apps中, 用户可以快速开发出web apps以及一些自动化任务, 对Google Apps进行操作, 或者实现数据交换.

GAS使用的语言是Javascript, 接下来的我们就从GAS For Sheets开始学习.





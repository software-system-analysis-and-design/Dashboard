---
layout: default
title: 挣钱宝
---





这里主要记录一些非核心的功能需求，并对一些需求进行细化补充。



### 消息通知需求 

我们主要关注任务发布者的消息通知，建立专门的消息通知记录模块。主要有以下几种情景需要：

1. 某一任务已经超过截止时间仍未全部完成，通知；
2. 某一任务在截止时间内全部完成，通知；
3. 任务未全部完成需要退还余款信息时，通知；



### 闲钱结算需求

在闲钱结算方面 ，我们定义以下规则和需求：

1. 用户在创建有偿任务时，需要根据任务设定的金额和个数支付给系统相应的资金；
2. 用户完成有偿任务之后，系统会根据任务的金额及时返回资金；
3. 用户有偿任务到期仍未全部完成时，系统自动结算退还资金；
4. 由于支付接口要求限制，用户可以指定金额进行充值满足有偿任务的发布。

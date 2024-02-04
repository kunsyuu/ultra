---
layout: post
title: Telegram验证码不发送短信而是发送给其他设备的解决
date: 2024-01-29 14:34:15
categories: Life
---
最近买了一个国外的手机号码，试图用这个新的手机号码登录Telegram时，不管是在手机端还是电脑客户端，都是提示“We've sent the code to the Telegram app for _your number_ on your other device.”。虽然在电脑端会有个Send SMS之类的按钮，但点击也仅仅是弹出一个提示框仍然是告诉你需要其他已登录的设备，而不会实际发SMS短信。

![](https://ucarecdn.com/91795815-d23c-46e4-bb30-d482f486b35a/3901.webp)

验证码是发送给其他已登录的客户端，而不是通过手机短信SMS来做验证，虽然我的确有这个号码的SIM卡，但仍然无法登录。想要登录，就必须先有一个已经登录的客户端才行。一开始我怀疑这个号码曾经被别人使用过，但现在号码已经在我手上了，没理由我却使用不了。

搜索了很多网页、视频，终于在一个页面发现有个人提了一句，可以使用 _Telegram X_ 这个客户端来先登录，带有X后缀的这个客户端是可以发送短信验证码的。下载试了一下果然正常的接收到SMS短信验证码并成功登录，是一个完全空白的账号。随后再通过扫二维码登录windows版。这样就可以正常使用了。

参考：https://github.com/TGX-Android/Telegram-X
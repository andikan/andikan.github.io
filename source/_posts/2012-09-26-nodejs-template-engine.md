---
layout: post
title: "node.js template engine"
date: 2012-09-26 23:56
comments: true
categories: [nodejs]
---

幾乎每一種程式語言都有各自的template engine，可以讓變數快速產生在web page上，  
各個語言的的template engine與比較可點閱：[wiki-Template engine(web)](http://goo.gl/ywsLx)  
<!--more-->  
 
  
而在node.js中也有許多template engine可以選擇：[node.js template engine](https://github.com/joyent/node/wiki/modules#wiki-templating "node.js template engine")  
其中express也支援許多template engine，像是：  
* haml.js : implementation of Haml, Haml多用於ruby on rails  
* Jade : 屬於 express default template engine，haml.js的後繼者  
* ejs : Embedded Javascript, 與 Rails 預設的 Embedded Ruby(erb) 十分相似  
* Blade : inspired by Jade & Haml  
* Swig : inspired by Django, Jinja, and Twig，適合python Django的開發者  
* TwigJS : 從PHP的template engine Twig沿生而來  

選擇一個自己喜歡的template engine可以加速開發的速度，本身對於 Jade 簡潔的語法還不太適應，所以較常使用 ejs，因為與 erb 很像很容易熟悉與上手，用  Jade 少打 end tag 感覺怪怪的～  


###References  
[quora.com](http://www.quora.com/What-is-the-best-node-js-template-engine)  
[csser.com](http://www.csser.com/board/4f3f516e38a5ebc978000504)  
[stackoverflow.com](http://stackoverflow.com/questions/1787716/is-there-a-template-engine-for-node-js)  
[ihower.tw](http://ihower.tw/rails3/actionview.html)  
      

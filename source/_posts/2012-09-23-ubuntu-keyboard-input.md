---
layout: post
title: "Ubuntu英文介面下的中文輸入(ibus)"
date: 2012-09-23 22:06
comments: true
categories: Ubuntu
---

在 Ubuntu 12.04 下，當使用英文介面時，需要中文輸入時的一些設定,  
進入system setting -> Language Support 中,  
在 Keyboard Input method system 選擇 ibus,  
右上角中即會產生一個鍵盤的小icon, 點下這個icon後選preferences,  
在Input Method 中勾選 Customize active input methods, 可以點add加入需要的中文輸入法(如新酷音),  
切換成ibus的input method 預設快速鍵 是Ctrl + space,  
當右上方沒有出現小鍵盤的icon時, 可下command來重新啟動ibus :  
{% codeblock %}
ibus-daemon -x -r -d 
{% endcodeblock%}
<!--more-->
  

### Sublime-text 中文輸入問題
在 ubuntu 的 sublime-text 中無法直接使用ibus作中文輸入,
需要其他 plugin 來作輔助, 目前找到的方法是[InputHelper](https://github.com/xgenvn/InputHelper "InputHelper")
, 安裝這個 plugin :
{% codeblock %}
cd ~/.config/sublime-text-2/Packages
git clone https://github.com/xgenvn/InputHelper.git
{% endcodeblock%}
很大的缺點在於輸入中文時需要先按 Ctrl+Shift+Z, 會跳出一個視窗來作輸入,  
希望可以找到其他更方便的sublime-text in Ubuntu 中文輸入解決方法 ~




---
layout: post
title: "在 Ubuntu 12.04 安裝 node.js"
date: 2012-09-24 01:50
comments: true
categories: [nodejs]
---

使用 nvm(Node Version Manage) 來安裝 node.js,  
預先需要 curl, git, g++ :  
{% codeblock %}
$ sudo apt-get install git-core g++ curl
{% endcodeblock%}   
接著即可用以下指令安裝 :  
{% codeblock %}
$ git clone git://github.com/creationix/nvm.git ~/.nvm
$ echo ". ~/.nvm/nvm.sh" >> ~/.bashrc
{% endcodeblock%}  
<!--more-->  
重新開啟 terminal 或是打`source ~/.bashrc`或`. ~/.bashrc` 載入新的bashrc設定到目前bash環境中, 接著 :  
{% codeblock %}
$ nvm install v0.8.9 # install current version, take some time
$ nvm alias default v0.8.9 # set default node version
$ node -v # verify 
{% endcodeblock %}  

node.js 在 0.6.3 之後的版本開始內建 npm (Node Package Management),    
可用 npm -v 作確認  

更多 node.js resource 可點閱 ： [NodeCloud](http://www.nodecloud.org/ "NodeCloud")  
npm rank ： [Nipster](http://eirikb.github.com/nipster/ "Nipster")  





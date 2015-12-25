---
layout: post
title: Bower - A package manager for web
date: 2013-05-08 01:21:40
categories: [javascript]
comments: true
---

![Bower twitter](http://farm8.staticflickr.com/7368/8717219451_ff5da4959c_z.jpg "Bower twitter")

[Bower](https://github.com/bower/bower)是一個來自twitter用來管理網站套件的工具，一個front-end的套件管理工具，用來方便管理專案中各種前端所需要的javascript librarys, frameworks, 和 modules，也包含許多html/css等assets，有近兩千種components在其上，使用起來相當方便，在include第三方package時不再需要一個個下載，可直接寫好packages相依性即可快速安裝各種js檔案進入專案資料夾中。  
<!--more-->  
  

首先就是先安裝bower，透過npm快速安裝(installed bower globally)：  
`npm install bower -g`

接著可以在家目錄或是project目錄下建立一個.bowerrc的設定檔，這個設定檔用來控制預設安裝的路徑與搜尋路徑等等，以JSON格式撰寫：  
{% codeblock An example .bowerrc lang:javascript %}
{
  "directory": "javascripts/components",           // 預設安裝路徑資料夾
  "endpoint": "https://bower.mycompany.com",       // 指定bower server，預設為bower官方server
  "json": "bower.json",                            // 設定各個專案的bower設定檔案名稱
  "searchpath": [ "https://bower.herokuapp.com" ], // 用來指定搜尋路徑，首要會先從endpoint開始搜尋，接著到searchpath依次搜尋
  "shorthand_resolver": ""                         // 定義package的縮寫格式
}
{% endcodeblock %} 
[一個簡單的bower server](https://github.com/bower/bower-server)  
  
在進入專案資料夾後即可快速開起bower設定檔，預設為bower.json，如同node.js中的`package.json`或ruby的`Gemfile`角色，只是管理的內容不同：`bower init` 

在bower.json的package設定上也很容易：
{% codeblock An example .bowerrc lang:javascript %}
{
  "name": "project-name",
  "version": "1.0.0",
  "dependencies": {
    "<name>": "<version>",
    "<name>": "<folder>",
    "<name>": "<package>"
  }
}
{% endcodeblock %}  
依照這樣的方式把自己需要的packages一個個條列出來，在按下：`bower install`  
即可將bower.json中所有相依的packages一次通通下載入.bawerrc中設定的預設資料夾中，使用起來和package.json十分相似。  

另外bower當然也提供互動式指令，如：  
`bower search [<name>]`  
`bower list`  
`bower install [<name>]`  
`bower install [<name>]  --save`  // 安裝後直接加入到bower.json中的dependencies裡。  
`bower uninstall <name>`  

也可將自己所寫的package快速註冊到bower server中：  
`bower register <my-package-name> <git-endpoint>`  

[Bower](https://github.com/bower/bower)使用上真的很直覺也和node.js中的npm類似，十分親近且實用的前端套件管理系統，  
也可在這個網站[Bower components](http://sindresorhus.com/bower-components/)搜尋bower所成列的packages。  
  


References：  
http://bower.io/  
http://net.tutsplus.com/tutorials/tools-and-tips/meet-bower-a-package-manager-for-the-web/  
http://sindresorhus.com/bower-components/  


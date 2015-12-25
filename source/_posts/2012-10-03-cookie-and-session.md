---
layout: post
title: "cookies 和 session 的神秘關係"
date: 2012-10-03 11:55
comments: true
categories: nodejs
---

由於HTTP協定中stateless的性質，當每一次client在對Server發送request時，前後的要求並不會互相影響，server並不會紀錄之前的狀態，也因此可以使用較少的系統資源來服務較多的client，而要讓server記住client的行為與資料時，就需要cookies與session的協助。
  
###cookies  
當server想要儲存使用者的某些狀態時，就可以發送cookie給client，cookie是http header裡面其中一個欄位，cookie裡的資料以key/value的形式儲存，cookies通常儲存在client的瀏覽器中，也因此若當cookie並沒有加密時，在傳送的過程中容易被攔截或盜取，故並不鼓勵以cookie儲存一些敏感的資料，除了加密之外，更要設定時間在不需要cookie的時候將它刪除。  
每個cookies的檔案最大只能到4k，在使用者瀏覽網站的時候瀏覽器會將cookie儲存在記憶體中，當瀏覽器關閉時，尚未expire的cookies會被存進文字檔中，並等待下次連線使用。 
<!--more-->

###session  
相對於cookies處存在client端，session則是儲存在server端，session也需要cookie的輔助才能產生運作，因為server會傳送存有session id的cookie給client，並在server端建立起這個session id的檔案，在之後client在瀏覽網頁時都會夾帶此session id，如此一來server即可從此session id來辨認每個使用者所儲存的狀態與data。相對於cookies，session多用來儲存敏感的資料，也常常成為攻擊的目標，如[session hijacking](http://knowledge.twisc.ntust.edu.tw/doku.php?id=3%E4%BC%BA%E6%9C%8D%E7%AB%AF%E5%AE%89%E5%85%A8:3-2%E6%87%89%E7%94%A8%E7%A8%8B%E5%BC%8F%E5%BC%B1%E9%BB%9E:Session%20hijacking)。  
  
###session in node.js  
在[npm](https://npmjs.org/)中有許多與session相關的module，而在express中是使用connect middleware來實現session功能，預設是儲存在記憶體中，當網站規模變大時，變需要透過資料庫作儲存，如[redis](https://github.com/visionmedia/connect-redis)、[mongoDB](https://github.com/masylum/connect-mongodb)、[couchDB](https://github.com/tdebarochez/connect-couchdb)等等，在這裡簡單介紹express中session的使用方式。  
  
在app.js中必須有這兩行的設定：
{% codeblock app.js lang:js %}
// in the app.configure
app.use(express.cookieParser());
app.use(express.session({ secret: 'andikan'});
{% endcodeblock %}  
  
這樣的設定可以直接在指令產生express app時加上--session or -s 作設定。  
接著就可以使用session了！例如：
{% codeblock create and read session lang:js %}
req.session.name = 'andy';  // set a session {name:'andy'}
req.session.cookie.maxAge = 3600000; // set the session expire after an hour.
req.session.destroy();  // destroys the session and re-generated next request.
{% endcodeblock %}   
document可參閱[connect session](http://www.senchalabs.org/connect/middleware-session.html)  
  

####reference  
[Jollen's PHP](http://www.jollen.org/php/216_session_cookies/)  
[TWISC@NTUST網路應用安全知識庫](http://knowledge.twisc.ntust.edu.tw/doku.php?id=3%E4%BC%BA%E6%9C%8D%E7%AB%AF%E5%AE%89%E5%85%A8:3-1%E4%BC%BA%E6%9C%8D%E5%99%A8%E7%AE%A1%E7%90%86:session%E5%92%8Ccookie%E7%9A%84%E4%BD%BF%E7%94%A8%E5%8F%8A%E5%B8%B6%E4%BE%86%E7%9A%84web%E9%A2%A8%E9%9A%AA)  
[Fred's blog](http://fred-zone.blogspot.tw/2011/11/nodejs-express-cookie-based-session.html)  
[HINA blog](http://blog.hinablue.me/entry/nodejs-first-look-part-2)  
[hack sparrow](http://www.hacksparrow.com/sessions-in-express-js-node-js-web-framework.html)  
[nodejitsu](http://blog.nodejitsu.com/sessions-and-cookies-in-node)  


 

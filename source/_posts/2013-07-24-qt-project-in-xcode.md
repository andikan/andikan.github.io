---
layout: post
title: Qt 4.8.4 project created with qmake fail to open in Xcode
date: 2013-07-24 01:36:00
categories: [Qt]
tags:
comments: true
sharing: true
---

承先前一篇[CGAL, Qt 在 Mac OS X 安裝編譯與執行](/blog/2013/04/13/cgal-on-macos-x/)，當用qmake新開一個Qt xcode project時，這個project卻無法用xcode開啟，最後發現這時候需要修改 project_name/project_name.xcodeproj/project.pbxproj 檔案的設定。  
<!--more-->

整個流程從開啟一個project資料夾開始，先mkdir project_name後再把.h, .cpp檔案放入或新增入資料夾中，接著在project_name dir裡以    
`qmake -project` 來建立project_name.pro  
`qmake -spec macx-g++` 來建立Mac環境下的Makefile  
`qmake -spec macx-xcode` 生成project_name.xcodeproj資料夾  
接著就是修改project_name.xcode裡面的project.pbxproj檔案，將  
`isa = PBXFrameworkReference;`修改為  
`lastKnownFileType = wrapper.framework;`  
`isa = PBXFileReference;`  
如此一來即可點擊project_name.xcodeproj順利在xcode開啟此project。


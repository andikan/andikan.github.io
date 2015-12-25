---
layout: post
title: CGAL, Qt 在 Mac OS X 安裝編譯與執行
date: 2013-04-13 02:00:07
comments: true
categories: [CGAL]
tags:
---

這個月買了新電腦，希望將Geometric Modeling課程中的作業轉移到MacOS X上編譯執行，助教和網路上許多教學文都是Windows下用Visual Studio之相關安裝流程，故在轉移上遇到許多問題，但在最後不斷嘗試的結果下終於可以編譯並執行，過程中許多設定還有地方和細節不明就裡，但在此做一個簡短的記錄，go！    
<!--more-->

剛開始希望能直接使用Xcode作為IDE，並先裝了Xcode，之後再從Xcode中的Preferences -> Downloads 點選下載Command line Tools來安裝編譯器和指令工具如LLVM、Make，再以Homebrew做為套件管理工具來簡化之後安裝流程，以一行指令即可安裝Homebrew：  
{% codeblock lang:bash %}
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
{% endcodeblock %}  
  
Homebrew可以用來安裝許多套件與程式，透過ruby所寫的formula簡化安裝流程，不用再從每個套件的官方網站下載編譯，接下來就可以用它來一個一個安裝所需要的library與framework了。  
  
* Boost C++ Libraries
直接以
{% codeblock lang:bash %}
brew install boost  
{% endcodeblock %} 
即可安裝至 /usr/local/Cellar資料夾底下，Homebrew會建立一個Cellar(酒窖)的資料夾來放置一個個套件(bottle)，移除也相當容易，只要：
{% codeblock lang:bash %}
brew uninstall formula 
{% endcodeblock %}  
就可以快速的移除不需要的套件，更多formula可以從https://github.com/mxcl/homebrew/tree/master/Library/Formula 尋找，或是：
{% codeblock lang:bash %}
brew search formula 
{% endcodeblock %}  
來尋找需要的套件。  

* libQGLViewer C++ library, Qt  
接著安裝3D視覺化相關library，因為此library相依於Qt，故在
{% codeblock lang:bash %}
brew install libqglviewer  
{% endcodeblock %}  
過程中就會安裝好Qt與Qt相依的套件，所有套件都會在同一個/usr/local/Cellar資料夾下。  
  
* Cmake      
cross platform make，在安裝CGAL時需用cmake來build。
{% codeblock lang:bash %}
brew install cmake  
{% endcodeblock %}    
  
* CGAL      
Computational Geometry Algorithms Library  
{% codeblock lang:bash %}
brew install cgal --imaging  
{% endcodeblock %}  
安裝時需加上--imaging選項來增加此library對Qt的支援。  
  
接下來便可以開始一個Qt project了，先開一個資料夾並把撰寫好的.cpp, .h放進去，先將課程assignment的skeleton code放入此資料夾中，並cd至此資料夾，接著：
{% codeblock %}
qmake -project    
{% endcodeblock %}  
來產生一個.pro的設定檔，這個設定檔將用來產生Makefile。原本以為可以透過qmake -spec macx-xcode projectname.pro來產生Xcode project設定檔便可以在Xcode上編輯，但一直失敗，無法將專案從Xcode上開啟，但不能氣餒繼續嘗試，開始編輯.pro檔中的設定參數，以下為目前嘗試的設定方法：  
{% codeblock Here's an example .pro file. lang:bash %}
TEMPLATE = app
TARGET = 
DEPENDPATH += .
# include headers
INCLUDEPATH += /usr/local/Cellar/cgal/4.1/include \
               /usr/local/Cellar/gmp/5.1.1/include \
               /usr/local/Cellar/boost/1.53.0/include \
               /usr/local/Cellar/libqglviewer/2.3.17/QGLViewer.framework/Headers \
               /usr/local/Cellar/qt/4.8.4/include
# include libraries and framework
LIBS += -L/usr/local/Cellar/cgal/4.1/lib \
        -L/usr/local/Cellar/gmp/5.1.1/lib \
        -L/usr/local/Cellar/boost/1.53.0/lib \
        -L/usr/local/Cellar/libqglviewer/2.3.17/QGLViewer.framework/Headers \
        -L/usr/local/Cellar/qt/4.8.4/lib
LIBS += -lssl -lcrypto
LIBS += -lCGAL
QMAKE_LFLAGS += -F/usr/local/Cellar/libqglviewer/2.3.17/
LIBS += -framework QGLViewer

# qt include
QT += xml opengl

# Input
HEADERS += CControlPanel.h \
           CMainWindow.h \
           CMesh.h \
           CMeshViewer.h \
           Define.h \
           IncludeLib.h \
           MeshIO.h \
           OpenGLUtil.h
FORMS += CMainWindow.ui
SOURCES += CControlPanel.cpp \
           CMainWindow.cpp \
           CMesh.cpp \
           CMeshViewer.cpp \
           main.cpp \
           MeshIO.cpp \
           OpenGLUtil.cpp

CONFIG += console
CONFIG -= app_bundle
CONFIG += x86_64
CONFIG -= i386

# compiler setting
QMAKE_CC = gcc
QMAKE_CXX = g++

QMAKE_CFLAGS_X86_64 += -mmacosx-version-min=10.7
QMAKE_CXXFLAGS_X86_64 = $$QMAKE_CFLAGS_X86_64

# libQGLviewer setting
QGLVIEWER_STATIC = yes
{% endcodeblock %}  
  
接著再用此.pro檔產生Makefile  
{% codeblock %}
qmake projectname.pro  #change to your project name    
{% endcodeblock %}  
  
產生Makefile後就可以開始make來編譯程式了，若順利編譯成功則會產生一個執行檔，執行時可能會發生找不到QGLViewer framework的狀況，還須將此建立一個symbolic link到/Library/Frameworks裡：  
{% codeblock lang:bash %}
sudo ln -s /usr/local/Cellar/libqglviewer/2.3.17/QGLViewer.framework /Library/Frameworks/QGLViewer.framework    
{% endcodeblock %}  

如此即可成功執行，也可使用各種文字編輯器撰寫相容於CGAL, Qt, QGLViewer library之相關程式了。  

### References : 
http://www.informit.com/articles/article.aspx?p=1405563&seqNum=2  
http://bitdewy.github.io/blog/2012/12/09/qt-xcode-hello/
http://www.libqglviewer.com/compilation.html  
http://stackoverflow.com/questions/4900230/help-getting-started-with-qt  
https://cours.etsmtl.ca/log750/share/simpleViewer.pro  








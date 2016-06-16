# 版本控制 Git
版本控制在團隊開發中扮演了一個非常重要的角色，所以在此我將推 Git 給大家認識，
為何推 Git ? 原因如下:  
> 1. 操作簡單易懂，且有一個開放的 github 站可以用。
2. 強大的分支管理。
3. 分布式版本控制系統，每個人的電腦就是一個版本庫。

安裝 Git
----
linux Debian or Ubuntu  

    $ sudo apt-get install git

安裝完成後，需要進行一些基本設定:  

    $ git config --global user.name "Your Name"
    $ git confit --global user.email "email@qq.com"

建立版本庫
----
    建立資料夾
    $ mkdir gitTest
    $ cd gitTest

    初始化(需在目標目錄下，gitTest)
    $ git init
    初始化完成後資料夾下會多出一個 .git 資料夾  

添加版本庫
----
    $ vi readme.md  #編輯文檔
    $ git add readme.md   #將文檔加到暫存庫
    $ git commit -m "readme 建立"  #寫版本說明，以便日後查詢版本

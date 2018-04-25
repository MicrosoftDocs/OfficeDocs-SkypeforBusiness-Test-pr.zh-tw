---
title: 設定 AD FS 2.0 支援用戶端驗證
TOCTitle: 設定 AD FS 2.0 支援用戶端驗證
ms:assetid: 4d93d400-ccaa-4da8-a71b-d05d7ba79d93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn308565(v=OCS.15)
ms:contentKeyID: 56269081
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 AD FS 2.0 支援用戶端驗證

 

_**上次修改主題的時間：** 2013-07-03_

有兩種可能的驗證類型可設定允許 AD FS 2.0 支援使用智慧卡驗證：

  - 表單架構驗證 (FBA)

  - 傳輸層安全性用戶端驗證

您可以使用表單架構驗證，開發能讓使用者以本身使用者名稱/密碼或智慧卡和 PIN 進行驗證的網頁。此主題著重如何以 AD FS 2.0 實作傳輸層安全性用戶端驗證。如需有關 AD FS 2.0 驗證類型的資訊，請參閱＜AD FS 2.0：如何變更本機驗證類型＞(英文)，網址為：[http://go.microsoft.com/fwlink/p/?LinkId=313384](http://go.microsoft.com/fwlink/p/?linkid=313384)。


**設定 AD FS 2.0 支援用戶端驗證**

1.  使用網域管理員帳戶登入 AD FS 2.0 電腦。

2.  啟動 Windows 檔案總管。

3.  瀏覽到 C:\\inetpub\\adfs\\ls。

4.  為現有的 web.config 檔案製作備份。

5.  使用「記事本」開啟現有的 web.config 檔案。

6.  從功能表列選取 **\[編輯\]**，然後選取 **\[尋找\]**。

7.  搜尋 **\<localAuthenticationTypes\>**。
    
    請留意，列出的驗證類型有四種，一行列出一種。

8.  將含有 TLSClient 驗證類型的行移至區段中的清單頂端。

9.  儲存並關閉 web.config 檔案。

10. 以較高的權限啟動命令提示字元。

11. 執行下列命令，重新啟動 IIS：
    
        IISReset /Restart /NoForce


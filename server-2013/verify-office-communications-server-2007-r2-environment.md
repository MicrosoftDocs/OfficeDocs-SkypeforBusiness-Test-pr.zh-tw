---
title: 驗證 Office Communications Server 2007 R2 環境
TOCTitle: 驗證 Office Communications Server 2007 R2 環境
ms:assetid: e051bdd5-e7ef-4754-8705-900b2c57f37c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721906(v=OCS.15)
ms:contentKeyID: 49890345
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證 Office Communications Server 2007 R2 環境

 

_**上次修改主題的時間：** 2012-10-16_

在與 Office Communications Server 2007 R2 處於共存狀態時，您必須在部署 Lync Server 2013 之前，確認已設定且啟動 Office Communications Server 2007 R2 服務。

**使用 Office Communications Server 2007 R2 系統管理工具確認已啟動集區**

1.  開啟 Office Communications Server 2007 R2 系統管理工具。

2.  依序展開 \[樹系\] 節點、\[Standard Edition Server\] 或 \[Enterprise Pool\] 節點，然後展開集區或伺服器名稱。

3.  確定服務執行於 Standard Edition Server 或 Enterprise Pool。
    
    ![Office Communications Server 2007 R2 管理主控台](images/JJ204914.76897b6d-f433-47d2-930d-0816fc30a3c2(OCS.15).jpg "Office Communications Server 2007 R2 管理主控台")

**檢閱為 Office Communications Server 2007 R2 設定的使用者**

1.  開啟 Office Communications Server 2007 R2 系統管理工具。

2.  依序展開 \[樹系\] 節點、\[Standard Edition Server\] 或 \[Enterprise Pool\] 節點，然後展開集區或伺服器名稱。

3.  按一下 \[使用者\] 。

4.  確認 Office Communications Server 2007 R2 使用者清單。
    
    ![OCS 管理工具中的使用者清單](images/JJ721906.f6bb7c4f-cbed-4389-8d0a-69a28577f17a(OCS.15).jpg "OCS 管理工具中的使用者清單")

**確認舊版 XMPP 同盟合作夥伴設定**

1.  從舊版 XMPP 伺服器瀏覽到 \[系統管理工具\]\\\[服務\] Applet。

2.  確認 Office Communications Server XMPP 閘道服務已經啟動。
    
    ![Office Communications Server XMPP 閘道服務](images/JJ205231.23223724-3c4b-4cb9-ace2-1cab2c3c91c3(OCS.15).jpg "Office Communications Server XMPP 閘道服務")


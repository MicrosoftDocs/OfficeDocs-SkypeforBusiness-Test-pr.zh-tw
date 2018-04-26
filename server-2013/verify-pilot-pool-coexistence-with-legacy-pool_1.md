---
title: 確認試驗集區與舊版集區共存
TOCTitle: 確認試驗集區與舊版集區共存
ms:assetid: 597d0fa6-ca04-4521-b1c2-72d7f35ecd08
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204914(v=OCS.15)
ms:contentKeyID: 49291006
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認試驗集區與舊版集區共存

 

_**上次修改主題的時間：** 2012-09-28_

## 在 Office Communications Server 2007 R2 系統管理工具中確認集區

1.  開啟 Office Communications Server 2007 R2 系統管理工具。

2.  依序展開 \[樹系\] 節點、\[Standard Edition Server\] 或 \[Enterprise Pool\] 節點，然後展開集區或伺服器名稱。

3.  確定 Office Communications Server 2007 R2 服務正在集區上執行。
    
    ![Office Communications Server 2007 R2 管理主控台](images/JJ204914.76897b6d-f433-47d2-930d-0816fc30a3c2(OCS.15).jpg "Office Communications Server 2007 R2 管理主控台")  

## 在 Lync Server 2013 控制台中確認試驗集區

1.  從屬於 CsAdministrator 角色成員的使用者帳戶，登入 Lync Server 2013 前端伺服器。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下 \[拓撲\] 。

4.  確認您部署的伺服器位於試驗集區。
    
    ![\[Lync Server 控制台拓撲\] 頁面](images/JJ204914.a3d1ba5f-c1a7-45e8-b9a5-7cb07b01af8c(OCS.15).jpg "[Lync Server 控制台拓撲] 頁面")  

## 確認已啟動 Lync Server 2013 服務

1.  在 Lync Server 2013 前端伺服器上，開啟 **\[系統管理工具\]** 群組中的 **\[服務\]** 小程式。

2.  確認所列的服務與下圖所示的清單相符。
    
    ![顯示已啟動 Lync 服務的服務頁面](images/JJ204914.fd35d54a-2ab6-4c09-b5e9-fd5bf10f6f51(OCS.15).jpg "顯示已啟動 Lync 服務的服務頁面")


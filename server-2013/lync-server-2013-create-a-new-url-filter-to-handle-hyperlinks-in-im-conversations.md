---
title: 在 IM 交談中建立處理超連結的新 URL 篩選器
TOCTitle: 在 IM 交談中建立處理超連結的新 URL 篩選器
ms:assetid: d0ee01e5-f039-4a34-ac9d-659fe4e9e879
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182590(v=OCS.15)
ms:contentKeyID: 49292387
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 IM 交談中建立處理超連結的新 URL 篩選器

 

_**上次修改主題的時間：** 2012-09-26_

除了修改全域 URL 篩選，您還可以為 Lync Server 2013 部署中的個別網站設定自訂 URL 篩選。如需 URL 篩選的詳細資訊，請參閱＜[在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)＞。

## 若要建立新的 URL 篩選

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中按一下 **\[IM 和目前狀態\]**，然後按一下 **\[URL 篩選\]**。

4.  在 **\[URL 篩選\]** 頁面上，按一下 **\[新增\]**。

5.  在 **\[選取站台\]** 中，按一下要建立 URL 篩選的網站，然後按一下 **\[確定\]**。

6.  在 **\[新增 URL 篩選\]** 對話方塊中，選取 **\[啟用 URL 篩選\]** 核取方塊，以啟用網站的 URL 篩選。

7.  若要封鎖任何作用中 URL (該 URL 包含具有 **\[編輯檔案篩選器\]** 中的 **\[要封鎖的副檔名\]** 下所列副檔名的檔案)，請選取 **\[以副檔名封鎖 URL\]** 核取方塊。

8.  在 **\[超連結首碼\]** 下拉式清單方塊中，按一下與您對立即訊息交談中的 URL 所要使用的處理方式相對應的選項。
    
    **\[允許訊息\]** 方塊可在傳送允許傳送的超連結時，讓警告訊息可以傳送給使用者。

9.  按一下 **\[認可\]**。

## 請參閱

#### 工作

[在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)  
[在特定的站台建立新檔案傳輸篩選器](lync-server-2013-create-a-new-file-transfer-filter-for-a-specific-site.md)  
[修改預設檔案傳輸篩選器](lync-server-2013-modify-the-default-file-transfer-filter.md)  

#### 概念

[修改預設 URL 篩選器](lync-server-2013-modify-the-default-url-filter.md)


---
title: 在特定的站台建立新檔案傳輸篩選器
TOCTitle: 在特定的站台建立新檔案傳輸篩選器
ms:assetid: d0006487-5217-491c-b730-e6c551cd9825
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182589(v=OCS.15)
ms:contentKeyID: 49292378
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在特定的站台建立新檔案傳輸篩選器

 

_**上次修改主題的時間：** 2012-10-18_

除了修改全域檔案傳輸篩選，您還可以為 Lync Server 2013 部署中的特定網站設定自訂檔案傳輸篩選。如需檔案傳輸篩選的詳細資訊，請參閱＜[在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)＞。

## 若要為特定網站建立檔案傳輸篩選

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[IM 和目前狀態\]** 和 **\[檔案篩選\]**。

4.  在 **\[檔案篩選\]** 頁面上，按一下 **\[新增\]**。

5.  在 **\[選取站台\]** 對話方塊中，按一下要建立檔案傳輸篩選的網站，然後按一下 **\[確定\]**。

6.  在 **\[新增檔案篩選\]** 中，按一下 **\[啟用檔案篩選\]** 核取方塊。

7.  在 **\[檔案傳輸\]** 下拉式清單方塊中，按一下 **\[全部封鎖\]** 或 **\[封鎖特定檔案類型\]**。

8.  如果您按一下 \[全部封鎖\]，請跳至步驟 10。

9.  如果您按一下 **\[封鎖特定檔案類型\]**，請執行下列動作：
    
    1.  按一下 **\[選取\]**，以修改您要封鎖之副檔名的預設清單。
    
    2.  在 **\[選取檔案類型\]** 對話方塊中，選取您要封鎖或允許的檔案類型，方法是在 **\[副檔名\]** 下方的類別中新增或移除其副檔名。
    
    3.  如果您未看見所要封鎖的檔案類型副檔名，請在 **\[將副檔名新增至清單\]** 下的文字方塊中輸入副檔名，然後按一下 **\[新增\]**。
    
    4.  按一下 **\[確定\]**。

10. 按一下 **\[認可\]**。

## 請參閱

#### 工作

[在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)  
[在 IM 交談中建立處理超連結的新 URL 篩選器](lync-server-2013-create-a-new-url-filter-to-handle-hyperlinks-in-im-conversations.md)  
[修改預設檔案傳輸篩選器](lync-server-2013-modify-the-default-file-transfer-filter.md)  

#### 概念

[修改預設 URL 篩選器](lync-server-2013-modify-the-default-url-filter.md)


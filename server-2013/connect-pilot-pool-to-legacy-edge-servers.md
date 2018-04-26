---
title: 將試驗集區連接到舊版 Edge Server
TOCTitle: 將試驗集區連接到舊版 Edge Server
ms:assetid: c3b67220-5705-47f6-852e-415204f3626c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721875(v=OCS.15)
ms:contentKeyID: 49890299
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將試驗集區連接到舊版 Edge Server

 

_**上次修改主題的時間：** 2012-09-29_

部署 Lync Server 2013 後，您需要為網站設定同盟路由。若要使用 Lync Server 2010 正在使用的同盟路由，您必須將 Lync Server 2013 設定成使用此路由。

若要啟用 Lync Server 2013 網站使用 Lync Server 2010 部署的 Director 和 Edge Server，請使用拓撲產生器建立與舊版 Edge 集區的關聯。

## 若要使用拓撲產生器建立與舊版 Edge 集區的關聯

1.  開啟 \[拓撲產生器\] 。

2.  選取您的網站，其位置就在 \[Lync Server\] 節點下方。

3.  在 \[執行\] 功能表上，按一下 \[編輯內容\] 。

4.  在左側窗格中，選取 \[同盟路由\] 。

5.  在 \[網站同盟路由指派\] 底下，選取 \[啟用 SIP 同盟\] ，然後選取 Lync Server 2010 Director 或是 Lync Server 2010 Edge Server (如果未列出 Director)。
    
    ![編輯內容，\[同盟路由\] 頁面](images/JJ721875.5f1d04c3-c724-426d-b27d-3fe89c6c5cfb(OCS.15).jpg "編輯內容，[同盟路由] 頁面")  

6.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。

7.  在拓撲產生器中的 Lync Server 2013 節點底下，瀏覽至 \[Standard Edition Server\] 或 \[Enterprise Edition 前端集區\] ，以滑鼠右鍵按一下集區，然後按一下 \[編輯內容\] 。

8.  在 \[關聯\] 底下，選取 \[設定相關聯的 Edge 集區 (適用於媒體元件)\] 旁邊的核取方塊。

9.  從清單中選取舊版 Edge Server。
    
    ![\[編輯內容\] 對話方塊，選取舊版 Edge](images/JJ721875.feae8156-540e-4804-bb0a-2b5736ec2900(OCS.15).jpg "[編輯內容] 對話方塊，選取舊版 Edge")  

10. 按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。

11. 在 \[拓撲產生器\] 中選取最頂端的節點 \[Lync Server\] 。

12. 從 \[動作\] 功能表中，按一下 \[發行拓撲\] ，然後按 \[下一步\] 。

13. 當 \[發行精靈\] 完成之後，按一下 \[完成\] 。


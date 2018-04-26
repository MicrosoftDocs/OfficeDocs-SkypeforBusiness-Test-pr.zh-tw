---
title: 將試驗集區連接到舊版 Edge Server
TOCTitle: 將試驗集區連接到舊版 Edge Server
ms:assetid: 9ed13c41-f3ab-4e1d-beb6-a00152c541e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205136(v=OCS.15)
ms:contentKeyID: 49291822
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將試驗集區連接到舊版 Edge Server

 

_**上次修改主題的時間：** 2012-10-02_

部署 Lync Server 2013 之後，系統不會設定此網站的同盟路由。若要使用 Office Communications Server 2007 R2 所用的同盟路由，必須設定 Lync Server 2013 使用此路由。

若要啟用 Lync Server 2013 網站以使用 BackCompatSite 的 Director 和 Edge Server，請使用拓撲產生器建立與舊版 Edge 集區的關聯。

## 若要使用拓撲產生器建立與舊版 Edge 集區的關聯

1.  在拓撲產生器中開啟試驗集區拓撲。

2.  選取您的 Lync Server 2013 網站。

3.  在 \[動作\] 功能表上，按一下 \[編輯內容\] 。

4.  在 \[網站同盟路由指派\] 底下，選取 \[啟用 SIP 同盟\]，然後選取 Office Communications Server 2007 R2 Director 或是 Office Communications Server 2007 R2 Edge Server (如未列出 Director)。
    
    ![\[編輯內容\] 對話方塊，\[同盟路由\] 頁面](images/JJ205136.bc13014b-3578-4d9e-9ff7-bdd09130b676(OCS.15).jpg "[編輯內容] 對話方塊，[同盟路由] 頁面")  

5.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。

6.  在拓撲產生器中的 Lync Server 2013 節點底下，瀏覽至 \[Standard Edition Server\] 或 \[Enterprise Edition 前端集區\] ，以滑鼠右鍵按一下集區，然後按一下 \[編輯內容\] 。

7.  在 \[關聯\] 底下，選取 \[設定相關聯的 Edge 集區 (適用於媒體元件)\] 旁邊的核取方塊。

8.  從清單中選取 BackCompatSite 的 Edge Server 介面。
    
    ![\[編輯內容\] 對話方塊，\[一般\] 頁面](images/JJ205136.75045212-03ca-4b82-8337-5dacb487094f(OCS.15).jpg "[編輯內容] 對話方塊，[一般] 頁面")  

9.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。

10. 在 \[拓撲產生器\] 中選取最頂端的節點：\[Lync Server\]。

11. 從 \[動作\] 功能表中，按一下 \[發行拓撲\] ，然後按 \[下一步\] 。

12. 當 \[發行精靈\] 完成之後，按一下 \[完成\] 。


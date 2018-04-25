---
title: 移除 BackCompatSite
TOCTitle: 移除 BackCompatSite
ms:assetid: 039650e3-541b-45c2-a682-c4fa08423118
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204637(v=OCS.15)
ms:contentKeyID: 49289931
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除 BackCompatSite

 

_**上次修改主題的時間：** 2012-09-28_

停用所有集區並解除安裝所有 Edge Server 之後，請執行 \[拓撲產生器合併精靈\] 以移除 BackCompatSite 。

## 從拓撲產生器移除 BackCompat 網站

1.  從拓撲產生器開啟現有的部署。

2.  在 \[執行\] 功能表中，按一下 \[合併 2007 R2 拓撲\] 。

3.  按 \[下一步\] 繼續。

4.  在「指定舊版 Edge」 頁面中，確認 Edge Server 清單是否為空的。若不是空的，請使用 \[移除\] 按鈕移除所有舊版的 Edge Server，然後按 \[下一步\] 。
    
    ![合併拓撲精靈，\[指定 Edge 安裝\] 頁面](images/JJ204637.fb35a59a-711e-4259-b177-7311df1fed3c(OCS.15).jpg "合併拓撲精靈，[指定 Edge 安裝] 頁面")  

5.  在「指定內部 SIP 連接埠設定」 頁面中按 \[下一步\] 。

6.  在「摘要」 頁面中按 \[下一步\] ，以開始合併拓撲，進而移除舊版網站。

7.  在 \[狀態\] 欄中，檢查其值是否為 \[成功\] ，然後按一下 \[完成\] ，以關閉精靈。

8.  在拓撲產生器的左窗格中，展開 BackCompatSite 並確定沒有列出任何伺服器。

9.  以滑鼠右鍵按一下 \[BackCompatSite\] ，然後按一下 \[刪除\] 。

10. 在 **\[拓撲產生器\]** 中選取最頂端的節點 **\[Lync Server\]** 。

11. 在 **\[執行\]** 功能表中，選取 **\[發行拓撲\]** ，然後按 **\[下一步\]** 。

12. 當 \[發行精靈\] 完成之後，按一下 \[完成\] ，以關閉精靈。


---
title: 設定監看員節點以參與 System Center 搜索
TOCTitle: 設定監看員節點以參與 System Center 搜索
ms:assetid: 15c5dcfd-603b-47ea-af1b-8714c2ec08af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204704(v=OCS.15)
ms:contentKeyID: 49290198
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定監看員節點以參與 System Center 搜索

 

_**上次修改主題的時間：** 2012-10-22_

若要確定監看員節點有參與 System Center Operations Manager 的探索程序，您必須在已安裝 System Center Operations Manager 主控台的電腦上完成下列程序：

1.  在 \[管理\] 索引標籤上，按一下 \[代理程式管理\]。

2.  用滑鼠右鍵按一下監看員節點電腦的名稱，然後按一下 \[內容\]。在 \[內容\] 對話方塊中的 \[安全性\] 索引標籤上，選取 \[允許此代理程式作為 Proxy 並探索其他電腦中的受管理物件\]，然後按一下 \[確定\]。

將監看員節點設為 Proxy 之後，重新啟動監看員節點電腦。電腦重新啟動之後，確認該電腦上的 Operations Manager 事件記錄中沒有記錄任何錯誤事件。在電腦執行 15 分鐘左右之後，使用 Operations Manager 主控台來確認 Lync Server 電腦列示在 **Lync** 類別底下。


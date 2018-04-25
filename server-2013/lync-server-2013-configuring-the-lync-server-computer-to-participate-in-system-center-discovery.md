---
title: 設定 Lync Server 電腦以參與 System Center 搜索
TOCTitle: 設定 Lync Server 電腦以參與 System Center 搜索
ms:assetid: 2f9c9cb0-3120-4571-9cd2-657c2123fe21
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204776(v=OCS.15)
ms:contentKeyID: 49290478
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 電腦以參與 System Center 搜索

 

_**上次修改主題的時間：** 2012-10-20_

若要確保您的新 Lync Server 代理程式參與了 System Center Operations Manager 探索程序，您必須在已安裝 System Center Operations Manager 主控台的每台電腦上，完成下列程序：

1.  在 \[管理\] 索引標籤上，按一下 \[代理程式管理\]。

2.  在電腦名稱上按一下滑鼠右鍵，然後按一下 \[內容\]。在 \[內容\] 對話方塊中的 \[安全性\] 索引標籤上，選取 \[允許此代理程式作為 Proxy 並探索其他電腦中的受管理物件\]，然後按一下 \[確定\]。

完成步驟 2 之後，請重新啟動健康狀態代理程式服務 (重新啟動服務會「強制執行」新機器的探索。若您沒有重新啟動服務，則在 4 個小時過後，System Center Operations Manager 才會探索新機器)。重新啟動服務之後，請在該電腦上確認 Operations Manager 事件記錄中沒有記錄任何錯誤事件。


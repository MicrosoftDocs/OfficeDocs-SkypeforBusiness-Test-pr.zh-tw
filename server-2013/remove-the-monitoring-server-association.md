---
title: 移除監控伺服器關聯
TOCTitle: 移除監控伺服器關聯
ms:assetid: c45b22ae-fc06-484a-a05b-735bd1bb7448
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721877(v=OCS.15)
ms:contentKeyID: 49890301
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除監控伺服器關聯

 

_**上次修改主題的時間：** 2012-10-04_

若要移除 監控伺服器，您必須變更或清除相關聯 前端集區、 前端伺服器、 Survivable Branch Appliance 以及 Survivable Branch 伺服器的相依性。您要編輯 前端集區、 前端伺服器、 Survivable Branch Appliance 以及 Survivable Branch 伺服器的屬性以移除相依性。當您移除相依性並刪除 拓撲產生器中的伺服器後，就會收到 拓撲產生器中的相關聯資料庫存放區物件也會被刪除的通知。

## 若要移除監控伺服器關聯

1.  開啟 Lync Server 2013 前端伺服器，再開啟拓撲建置器。

2.  瀏覽至 Lync Server 2010 節點。

3.  在拓撲產生器中，依據監控伺服器定義的所在位置，展開 \[Enterprise Edition 前端集區\]、\[Standard Edition 前端伺服器\] 或 \[分支網站\]。

4.  若已與 Survivable Branch 伺服器 關聯，請依序展開 \[分支站台\] 、分支網站名稱及 \[Survivable Branch Appliances\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>使用者介面中的 [Survivable Branch Appliances] 會套用至 Survivable Branch 伺服器 及 Survivable Branch Appliance。</td>
    </tr>
    </tbody>
    </table>


5.  以滑鼠右鍵按一下關聯到監控伺服器的集區、伺服器或裝置，然後按一下 \[編輯屬性\]。

6.  在 \[編輯內容\] 之 \[一般\] 下的 \[關聯\] 下方，清除 \[建立監控伺服器關聯\] 核取方塊，然後按一下 \[確定\] 。

7.  針對其他與 監控伺服器相關聯的集區、伺服器或裝置，重複上述步驟。

8.  以滑鼠右鍵按一下 監控伺服器，然後按一下 \[刪除\] 。

9.  在 \[刪除相依存放區\] 上，按一下 \[確定\] 。

10. 發行拓撲，並檢查複寫狀態，然後視需要執行 Lync Server 部署精靈。


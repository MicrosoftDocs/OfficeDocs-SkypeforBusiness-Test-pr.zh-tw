---
title: 移除封存伺服器關聯
TOCTitle: 移除封存伺服器關聯
ms:assetid: dabac157-71ee-4afe-b0b6-4a083d165ffb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721903(v=OCS.15)
ms:contentKeyID: 49890337
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除封存伺服器關聯

 

_**上次修改主題的時間：** 2012-10-04_

若要移除 封存伺服器，您需要變更或清除對關聯之 前端集區、 前端伺服器、 Survivable Branch Appliance 及 Survivable Branch 伺服器的相依性。您要編輯 前端集區、 前端伺服器、 Survivable Branch Appliance 及 Survivable Branch 伺服器的屬性來移除相依性。在 拓撲產生器中清除相依性及刪除伺服器之後，系統會通知您將會一併刪除 拓撲產生器中相關聯的資料庫存放區物件。

## 移除封存伺服器關聯

1.  開啟 Lync Server 2013 前端伺服器，再開啟拓撲建置器。

2.  瀏覽至 Lync Server 2010 節點。

3.  在 拓撲產生器中，依據 封存伺服器定義的所在位置，展開 \[Enterprise Edition 前端集區\] 、\[Standard Edition 前端伺服器\] 或 \[分支站台\] 。

4.  若已與 Survivable Branch 伺服器 關聯，請依序展開 \[分支站台\] 、分支網站名稱及 \[Survivable Branch Appliances\] 。
    
    > [!NOTE]  
    > 使用者介面中的 [Survivable Branch Appliances] 會套用至 Survivable Branch 伺服器 及 Survivable Branch Appliance。
    


5.  以滑鼠右鍵按一下關聯到 封存伺服器的集區、伺服器或裝置，然後按一下 \[編輯屬性\] 。

6.  在 \[編輯屬性\] 的 \[一般\] 底下，清除 \[關聯\] 底下的 \[建立封存伺服器的關聯\] 核取方塊，然後按一下 \[確定\] 。

7.  針對與您要移除之 封存伺服器相關聯的任何其他集區、伺服器或裝置，重複上一個步驟。

8.  以滑鼠右鍵按一下封存伺服器，然後按一下 \[刪除\]。

9.  在 \[刪除相依存放區\] 上，按一下 \[確定\] 。

10. 發行拓撲，並檢查複寫狀態，然後視需要執行 Lync Server 部署精靈。


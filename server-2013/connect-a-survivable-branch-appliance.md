---
title: 連接 Survivable Branch Appliance
TOCTitle: 連接 Survivable Branch Appliance
ms:assetid: fe3167e2-d1b1-4cd4-bf30-262e0e7d14e8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721948(v=OCS.15)
ms:contentKeyID: 49890523
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 連接 Survivable Branch Appliance

 

_**上次修改主題的時間：** 2012-10-19_

每個 Survivable Branch Appliance (SBA) 均與作為 SBA 備份登錄器的前端集區相關聯；將前端集區移轉至 Lync Server 2013 時，必須在升級集區時解除 SBA 與 Lync Server 2010 前端集區的關聯。一旦將集區移轉至 Lync Server 2013，即可重新將 SBA 與升級後的前端集區相關聯。這涉及從「拓撲產生器」中的舊版 Lync Server 2010 拓撲刪除 SBA，然後將 SBA 新增至 Lync Server 2013 拓撲。隸屬於舊版 Lync Server 2010 SBA 的使用者，必須先移至其他前端集區，才能從拓撲中移除 SBA。一旦將 SBA 新增至 Lync Server 2013 拓撲，即可將這些使用者移回 SBA。這些步驟摘述如下：

1.  將隸屬於舊版 SBA Lync Server 2010 的分支使用者移至其他前端集區。

2.  從舊版 Lync Server 2010 拓撲移除 SBA，以中斷作為備份登錄器的現有前端集區連線。

3.  將 SBA 新增至 Lync Server 2013 拓撲，並將此新前端集區設定為備份登錄器。

4.  將分支使用者移至新 Lync Server 2013 SBA。

**將 Lync Server 2010 SBA 分支網站新增至拓撲**

1.  開啟 \[拓撲產生器\] 。

2.  在左窗格中，以滑鼠右鍵依序按一下 \[分支網站\] 和 \[新增分支網站\] 。

3.  在 \[定義新的分支網站\] 對話方塊中，按一下 \[名稱\] ，然後輸入分支網站的名稱。

4.  (選用) 按一下 \[描述\]，然後為分支網站輸入有意義的描述。

5.  按 \[下一步\] 。

6.  (選用) 在下一個 \[定義新的分支網站\] 對話方塊中，執行下列其中一項操作：
    
    1.  按一下 \[城市\] ，然後輸入分支網站所在位置的城市名稱。
    
    2.  按一下 \[省/地區\] ，然後輸入分支網站所在位置的省或地區名稱。
    
    3.  按一下 \[國碼\] ，然後輸入分支網站所在國家/地區的兩位數撥號碼。

7.  按 \[下一步\] ，然後執行下列其中一項：
    
    1.  如果您在此網站上是使用 Lync 2010 Survivable Branch Appliance 或 Survivable Branch Server，請確定取消核取 \[當這個精靈關閉時，開啟新的 Survivable 精靈\] 選項。按一下 \[完成\] 。

8.  將舊版 Lync Server 2010 SBA 與 Lync Server 2013 前端集區相關聯：
    
    1.  展開已建立的分支網站。
    
    2.  以滑鼠右鍵按一下 \[Lync Server 2010\] ，然後按一下 \[新增\] 。
    
    3.  按一下 \[Survivable Branch Appliance…\] 。

9.  遵循開啟之精靈的指引。如需有關精靈項目的詳細資訊，請參閱 [在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)。
    
    > [!NOTE]  
    > Lync Server 2010 Survivable Branch Appliance 僅可與 Lync Server 2010 監控儲存區相關聯。
    


10. 如果您不在此網站使用 Survivable Branch Appliance 或 Survivable Branch Server，請清除 \[當這個精靈關閉時，開啟新的 Survivable Branch Appliance 精靈\] 核取方塊，然後按一下 \[完成\] 。

11. 針對您要新增至拓撲的每一個分支網站重複上述步驟。


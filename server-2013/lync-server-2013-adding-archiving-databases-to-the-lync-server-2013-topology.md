---
title: 將封存資料庫新增至 Lync Server 2013 拓撲
TOCTitle: 將封存資料庫新增至 Lync Server 2013 拓撲
ms:assetid: 089ab32f-1167-4bb8-a283-fdc6c9613072
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204654(v=OCS.15)
ms:contentKeyID: 49290009
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將封存資料庫新增至 Lync Server 2013 拓撲

 

_**上次修改主題的時間：** 2012-10-10_

您必須先將封存納入拓撲中，才能設定部署來支援封存。本主題中的資訊說明如何使用拓撲產生器將封存新增至現有的拓撲。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要使用 Microsoft Exchange 整合，為部署中的所有使用者將封存資料和檔案儲存在 Exchange 2013 伺服器上，請勿指定 [封存 SQL Server 儲存區] 或 [使用 SQL Server 儲存區鏡像] 資訊。</td>
</tr>
</tbody>
</table>


## 新增封存資料庫支援至拓撲

1.  在執行 Lync Server 2013 的電腦上，或安裝 Lync Server 系統管理工具的電腦上，使用本機 Users 群組成員的帳戶 (或具有相等使用者權限的帳戶) 登入。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用本機 Users 群組成員的帳戶來定義拓撲，但是若要發行拓撲 (新增伺服器至拓撲時所必需)，您必須使用 <strong>Domain Admins</strong> 群組成員及 <strong>RTCUniversalServerAdmins</strong> 群組成員的帳戶，而且在您要用於 Lync Server 2013 檔案儲存區 (以便拓撲產生器可設定所需的判別存取控制清單 (DACL)) 的檔案共用上，具有完整控制權限 (亦即，讀取、寫入和修改) 的帳戶，或是具有相等權限的帳戶。</td>
    </tr>
    </tbody>
    </table>


2.  啟動拓撲產生器。

3.  在主控台樹狀目錄中，瀏覽至要部署封存的前端集區，然後按一下要部署封存的前端集區名稱。

4.  在 \[動作\] 功能表中，按一下 \[編輯內容\]。

5.  在 \[編輯內容\] 對話方塊中，按一下 \[一般\]。

6.  向下捲動至 \[封存\]。

7.  選取 \[封存\] 核取方塊。

8.  在 \[封存 SQL Server 儲存區\] 底下，執行下列動作：
    
      - 若要使用現存的 SQL Server 儲存區，請在下拉式清單方塊中，按一下您要使用之 SQL Server 儲存區的名稱。如果您的所有使用者都安置在 Microsoft Exchange Server 2013 或更新版本上，則可以為 Exchange 中的所有使用者封存 Lync 通訊。在此情況下，您不需要設定 SQL Server 封存儲存區。
    
      - 若要指定新的 SQL Server 儲存區，請按一下 \[新增\]，然後在 \[定義新的 SQL Server 儲存區\] 對話方塊中，執行下列動作：
        
          - 在 **SQL Server FQDN** 中，指定要建立新 SQL Server 儲存區之伺服器的 FQDN。
        
          - 按一下 \[預設執行個體\] 以使用預設執行個體，或指定不同的執行個體，然後按一下 \[具名執行個體\]，再指定您要使用的執行個體。
        
          - 如果指定的 SQL Server 執行個體在鏡像關聯中，請選取 \[此 SQL 執行個體在鏡像關聯中\] 核取方塊，然後在 \[鏡像連接埠號碼\] 中指定連接埠號碼。

9.  如果您要使用 SQL Server 儲存區鏡像，請選取 \[啟用 SQL Server 儲存區鏡像\]，然後執行下列動作：
    
      - 若要使用現存的 SQL Server 儲存區來進行鏡像，請在 \[封存 SQL Server 儲存區鏡像\] 下拉式清單方塊中，按一下您要用於鏡像之 SQL Server 儲存區的名稱。
    
      - 若要指定新的 SQL Server 儲存區來進行鏡像，請按一下 \[新增\]，然後在 \[定義新的 SQL Server 儲存區\] 對話方塊中，執行下列其中一個動作：
        
        1.  在 \[SQL Server FQDN\] 中，指定要建立新 SQL Server 儲存區之 SQL Server 的 FQDN。
        
        2.  按一下 \[預設執行個體\] 以使用預設執行個體，或指定不同的執行個體，然後按一下 \[具名執行個體\]，再指定您要使用的執行個體。
        
        3.  如果指定的 SQL Server 執行個體在鏡像關聯中，請選取 \[此 SQL 執行個體在鏡像關聯中\] 核取方塊，然後在 \[鏡像連接埠號碼\] 中指定連接埠號碼。
    
      - 如果您啟用 SQL Server 鏡像，而且想要包含 SQL Server 鏡像見證 (第三個個別的 SQL Server 執行個體，可偵測主要 SQL Server 伺服器和鏡像執行個體的運作情況)，請選取 \[使用 SQL Server 鏡像見證來啟用自動容錯移轉\] 核取方塊，然後執行下列其中一個動作：
        
        1.  在 **SQL Server FQDN** 中，指定要建立新 SQL Server 鏡像見證之伺服器的 FQDN。
        
        2.  按一下 \[預設執行個體\] 以使用預設執行個體，或指定不同的執行個體，然後按一下 \[具名執行個體\]，再指定您要用於鏡像見證的執行個體。
        
        3.  如果指定的 SQL Server 執行個體在鏡像關聯中，請選取 \[此 SQL 執行個體在鏡像關聯中\] 核取方塊，然後在 \[鏡像連接埠號碼\] 中指定連接埠號碼。

10. 若要儲存設定，請按一下 \[確定\]。


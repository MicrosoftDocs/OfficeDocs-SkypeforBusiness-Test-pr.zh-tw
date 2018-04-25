---
title: Lync Server 2013：發行拓撲
TOCTitle: 發行拓撲
ms:assetid: 3b5a744b-b3a8-4538-a55e-e2e4f72dff47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425880(v=OCS.15)
ms:contentKeyID: 49290648
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中發行拓撲

 

_**上次修改主題的時間：** 2013-10-01_

若要在新增或移除伺服器角色時順利發行、啟用或停用拓撲，您應該以 RTCUniversalServerAdmins 和 Domain Admins 群組成員的使用者身分登入。您也可以委派適當的系統管理員權利和使用權限。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)＞。若要進行其他組態變更，則僅需要 RTCUniversalServerAdmins 群組中的成員資格。

在 拓撲產生器 中定義拓撲之後，您必須將拓撲發行到 中央管理存放區。中央管理存放區 提供在定義、設定、維護、管理、描述及運作 Lync Server 2013 部署時，所需要的穩固、結構描述化的資料儲存。它也驗證資料，以確保設定一致性。對此設定資料的所有變更都發生在 中央管理存放區，避免發生「不同步」的問題。資料的唯讀複本會複製到拓撲中的所有伺服器，包括 Edge Server。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SQL Server 至少需要 20 GB 的可用磁碟空間，才能成功發佈初始拓撲及建立中央管理伺服器。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅限 Enterprise Edition：若要發行拓撲，SQL Server 後端伺服器必須上線，並納入防火牆例外中以供人存取。如需指定防火牆例外的詳細資訊，請參閱＜ <a href="lync-server-2013-understanding-firewall-requirements-for-sql-server.md">瞭解與 Lync Server 2013 搭配使用時之 SQL Server 的防火牆需求</a>＞。如需設定 SQL Server 的詳細資訊，請參閱＜ <a href="lync-server-2013-configure-sql-server-for-lync-server.md">為 Lync Server 2013 設定 SQL Server</a>＞。</td>
</tr>
</tbody>
</table>


## 若要發行拓撲

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  選取本機檔案以開啟其中的拓撲。如果您在操作當初用於定義拓撲的電腦，檔案就位於您在稍早步驟儲存該檔案的位置。此位置通常是當初設定拓撲的使用者的 Documents 資料夾。

3.  用滑鼠右鍵按一下 **\[ Lync Server 2013\]** 節點，然後按一下 **\[發行拓撲\]** 。

4.  在 **\[發行拓撲\]** 頁面上，按 **\[下一步\]** 。

5.  在 **\[建立資料庫\]** 頁面上，選取您要發行的資料庫。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您不具有建立某些資料庫的適當權限，可以清除那些資料庫旁邊的核取方塊，讓具有適當權限的其他人稍後再來建立資料庫。如需詳細資訊，請參閱＜ <a href="lync-server-2013-deployment-permissions-for-sql-server.md">Lync Server 2013 中 SQL Server 的部署權限</a>＞。</td>
    </tr>
    </tbody>
    </table>


6.  (選用) 按一下 \[進階\]。進階 SQL Server 資料檔案位置選項可讓您選取下列選項：
    
      - **自動判斷資料庫檔案位置** - 此選項會根據 SQL Server 型伺服器上的磁碟組態，判斷最佳的運作效能，將記錄和資料檔案分散至最佳位置。
    
      - **使用 SQL Server 執行個體預設值** - 此選項會使用執行個體設定值，將記錄和資料檔案存放在 SQL Server 型伺服器上。此選項不使用 SQL Server 型伺服器的運作功能來判斷記錄和資料的最佳位置。SQL Server 系統管理員通常會將記錄和資料檔案移至對於 SQL Server 型伺服器和組織管理程序而言適合的位置。
    
    依序按一下 **\[確定\]** 和 **\[下一步\]** 。

7.  在 **\[選取中央管理伺服器\]** 頁面上，選取 前端集區。

8.  (選用) 按一下 \[進階\]。進階 SQL Server 資料檔案位置選項可讓您選取下列選項：
    
      - **自動判斷資料庫檔案位置** - 此選項會根據 SQL Server 型伺服器上的磁碟組態，判斷最佳的運作效能，將記錄和資料檔案分散至最佳位置。
    
      - **使用 SQL Server 執行個體預設值** - 此選項會使用執行個體設定值，將記錄和資料檔案存放在 SQL Server 型伺服器上。此選項不使用 SQL Server 型伺服器的運作功能來判斷記錄和資料的最佳位置。SQL Server 系統管理員通常會將記錄和資料檔案移至對於 SQL Server 型伺服器和組織管理程序而言適合的位置。
    
    按一下 \[確定\] 。

9.  按 **\[下一步\]** 完成發行程序。

10. 發行程序完成時，請按一下 \[完成\] 。
    
    成功發行拓撲後，您可以開始在拓撲中每部執行 Lync Server 2013 的伺服器上安裝 中央管理存放區的本機複本。建議您先從第一個 前端集區開始。

## 請參閱

#### 其他資源

[針對 Lync Server 2013 設定前端伺服器和前端集區](lync-server-2013-setting-up-front-end-servers-and-front-end-pools.md)


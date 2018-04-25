---
title: 準備還原 Lync Server
TOCTitle: 準備還原 Lync Server
ms:assetid: 857e4e02-908e-433a-96c6-be1795a9cb61
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202179(v=OCS.15)
ms:contentKeyID: 52056140
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 準備還原 Lync Server

 

_**上次修改主題的時間：** 2015-03-09_

在您因故障而開始還原伺服器和資料庫之前，您必須先判斷：

  - 需要還原的項目。

  - 還原需要用到的硬體、軟體、資料及工具。

## 決定要還原的項目

本主題說明如何還原出現在伺服器、集區或中央管理存放區層級的 Lync Server 中斷問題。若中央管理存放區故障，您的 Lync Server 部署仍會持續運作，但您卻無法變更任何設定。若是後端伺服器或 Standard Edition Server 故障，則使用者集區將停止運作。若是其他的伺服器故障，影響程度將視該伺服器所執行的伺服器角色，以及該伺服器是否代管了一或多個資料庫而定。

### 還原的項目

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果是這個東西故障，</th>
<th>請參閱本節：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Standard Edition server</p></td>
<td><p><a href="lync-server-2013-restoring-a-standard-edition-server.md">還原 Standard Edition 伺服器</a></p></td>
</tr>
<tr class="even">
<td><p>中央管理存放區</p></td>
<td><p><a href="lync-server-2013-restoring-the-server-hosting-the-central-management-store.md">還原裝載中央管理存放區的伺服器</a></p></td>
</tr>
<tr class="odd">
<td><p>Enterprise Edition 後端</p></td>
<td><p><a href="lync-server-2013-restoring-an-enterprise-edition-back-end-server.md">還原 Enterprise Edition 後端伺服器</a></p></td>
</tr>
<tr class="even">
<td><p>Enterprise Edition 鏡像後端主要伺服器</p></td>
<td><p><a href="lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-primary.md">還原鏡像 Enterprise Edition 後端伺服器 - 主要</a></p></td>
</tr>
<tr class="odd">
<td><p>Enterprise Edition 鏡像後端次要伺服器</p></td>
<td><p><a href="lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md">還原鏡像 Enterprise Edition 後端伺服器 - 鏡像</a></p></td>
</tr>
<tr class="even">
<td><p>執行伺服器角色 (例如前端伺服器、Edge Server、Director、中繼伺服器) 的任何 Enterprise Edition Server 或 Persistent Chat Server。</p></td>
<td><p><a href="lync-server-2013-restoring-an-enterprise-edition-member-server.md">還原 Enterprise Edition 成員伺服器</a></p></td>
</tr>
<tr class="odd">
<td><p>整個 Lync Server 集區</p></td>
<td><p><a href="lync-server-2013-restoring-a-lync-server-pool.md">還原 Lync Server 集區</a></p></td>
</tr>
<tr class="even">
<td><p>Enterprise Edition 檔案存放區</p></td>
<td><p><a href="lync-server-2013-restoring-a-file-store.md">還原檔案存放區</a></p></td>
</tr>
<tr class="odd">
<td><p>獨立的監控資料庫或封存資料庫</p></td>
<td><p><a href="lync-server-2013-restoring-monitoring-or-archiving-data.md">還原監控資料和封存資料</a></p></td>
</tr>
<tr class="even">
<td><p>獨立的常設聊天室資料庫</p></td>
<td><p><a href="lync-server-2013-restoring-persistent-chat-data.md">還原常設聊天室資料</a></p></td>
</tr>
</tbody>
</table>


## 準備好硬體、軟體和工具

還原伺服器時，您必須用一部全新或乾淨的電腦。此外，必須準備好下列硬體和軟體：

  - 與故障伺服器具有相同完整網域名稱 (FQDN) 的乾淨或全新伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>安裝作業系統時，小心不要刪除 Active Directory 網域服務 中的電腦帳戶，並確定保留所有該帳戶的群組權限。</td>
    </tr>
    </tbody>
    </table>


  - 作業系統的安裝軟體。若要安裝作業系統，請使用組織所制定的伺服器部署程序與設定。還原服務時，應該準備好這些程序和設定需求以便隨時參考。

  - SQL Server 2012 或 SQL Server 2008 R2 的安裝軟體。若要安裝資料庫伺服器，請使用組織所制定且版本正確的 SQL Server 與資料庫伺服器部署程序和設定。還原服務時，應該準備好這些程序和設定需求以便隨時參考。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>安裝本機設定存放區後，Lync Server 部署精靈便會自動在每個 Standard Edition 伺服器及其他 Lync Server 伺服器上安裝 SQL Server 2012 Express，除非您在伺服器上已預先安裝 SQL Server 2012 或 SQL Server 2008 R2。</td>
    </tr>
    </tbody>
    </table>


  - 可備份系統映像的軟體
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>建議您在安裝作業系統和 SQL Server 後，先製作一個系統映像複本，再開始還原。您即可在還原期間發生任何狀況時，使用此映像做為回復點。</td>
    </tr>
    </tbody>
    </table>


  - Lync Server 2013 安裝軟體。Lync Server 部署精靈位於 Lync Server 的安裝資料夾或媒體中，路徑為：\\setup\\amd64\\Setup.exe。

還原期間，您會用到下列工具：

  - Lync Server 管理命令介面 指令程式

  - Import-CsUserData

  - 用來還原 Windows 資料夾的工具

  - 拓撲產生器

  - SQL Server 資料庫公用程式，例如 SQL Server Management Studio

## 準備還原伺服器

還原伺服器前，您必須執行下列步驟：

1.  安裝作業系統。

2.  如果伺服器是後端伺服器，請安裝 SQL Server 2012 或 SQL Server 2008 R2。

3.  還原或重新註冊您的憑證。如需憑證的詳細資訊，請參閱＜[備份和還原需求：資料](lync-server-2013-backup-and-restoration-requirements-data.md)＞中的＜其他備份需求＞。

4.  開始還原前先製作系統映像，以免還原期間出現任何狀況時，可以做為回復點。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 部署精靈和本主題中程序所提到的 Cmdlet，會設定所有必要的存取控制清單 (ACL)。</td>
</tr>
</tbody>
</table>


開始還原前，先確定要還原元件所需的硬體和軟體皆已備齊。安裝作業系統和 SQL Server 後，接下來大多的還原程序步驟都可以遠端執行。例外的步驟在程序中會註明。

也建議您在開始還原前，先準備好組織的備份與還原規劃，以及上次備份的資訊，如本文件工作表中的資訊 (如需詳細資訊，請參閱＜[備份和還原工作表](lync-server-2013-backup-and-restoration-worksheets.md)＞)。


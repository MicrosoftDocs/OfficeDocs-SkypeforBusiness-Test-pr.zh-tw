---
title: 備份和還原需求：工具和權限
TOCTitle: 備份和還原需求：工具和權限
ms:assetid: 35ec2e33-f33e-4f84-9e64-6550fd78aa52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202171(v=OCS.15)
ms:contentKeyID: 52056084
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份和還原需求：工具和權限

 

_**上次修改主題的時間：** 2015-03-09_

本主題指出您可以用來備份及還原 Lync Server 2013 的工具、所需的權限，以及是否可以從遠端或在本機執行命令。明確來說，本主題著重在 Lync Server 提供的備份及還原工具。

## 備份

若要備份 Lync Server，請使用下表指出的工具。所有備份 Lync Server 所需的命令都可以寫成指令碼，並可從遠端執行。

### 用於備份 Lync Server 的工具

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>若要備份這個：</th>
<th>使用此工具或 Cmdlet：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拓撲設定資料 (Xds.mdf)</p></td>
<td><p>Export-CsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>位置資訊服務 (E9-1-1) 資料 (Lis.mdf)</p></td>
<td><p>Export-CsLisConfiguration</p></td>
</tr>
<tr class="odd">
<td><p>回應群組設定資料 (RgsConfig.mdf)</p></td>
<td><p>Export-CsRgsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>持續性使用者資料 (Rtcxds.mdf 資料庫)</p>
<p>會議 ID</p></td>
<td><p>Export-CsUserData</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>封存資料庫 (LcsLog.mdf)</p></li>
<li><p>監視詳細通話記錄資料庫 (LcsCDR.mdf)</p></li>
<li><p>監視 QoE 資料庫 (QoEMetrics.mdf)</p></li>
</ul></td>
<td><p>SQL Server 資料庫工具，例如 SQL Server Management Studio</p></td>
</tr>
<tr class="even">
<td><p>常設聊天室資料庫 (Mgc.mdf)</p></td>
<td><p>SQL Server 備份程序或 Export-CsPersistentChatData。Export-CsPersistentChatData 會將常設聊天室資料匯出為檔案。</p></td>
</tr>
<tr class="odd">
<td><p>所有的檔案存放區︰Lync Server 檔案存放區、封存檔案存放區</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Meeting.Active</strong> 檔案不應備份。會議進行期間會使用這些檔案並予以鎖定。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>標準檔案系統管理工具，如 Robocopy。</p></td>
</tr>
</tbody>
</table>


## 還原

若要還原 Lync Server，請使用下表中的工具。所有還原 Lync Server 所需的命令都可以寫成指令碼。部分命令可以從遠端執行，但其他命令則需要在本機執行，如下表所示。

### 用來還原 Lync Server 的工具

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>若要執行此作業：</th>
<th>使用此工具或 Cmdlet：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>建立全新的電腦</p></td>
<td><ul>
<li><p>Windows 作業系統安裝軟體</p></li>
<li><p>SQL Server 安裝軟體</p></li>
<li><p>如果以可匯出的私密金鑰來還原憑證，則請認證 Microsoft Management Console (MMC) 嵌入式管理單元</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>還原檔案存放區資料</p></td>
<td><p>標準檔案系統管理工具，如 Robocopy</p></td>
</tr>
<tr class="odd">
<td><p>重新建立空的資料庫，並設定下列的權限：</p>
<ul>
<li><p>中央管理存放區</p></li>
<li><p>後端伺服器</p></li>
<li><p>監控資料庫</p></li>
<li><p>封存資料庫</p></li>
</ul></td>
<td><p>Install-CsDatabase</p></td>
</tr>
<tr class="even">
<td><p>將 Active Directory 網域服務 指標還原至中央管理存放區</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在任何時候遺失服務連線點，都可以重新執行此 Cmdlet。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>Set-CsConfigurationStoreLocation</p></td>
</tr>
<tr class="odd">
<td><p>將拓撲、原則及組態設定匯入至 中央管理存放區 (Xds.mdf)</p></td>
<td><p>Import-CsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>發行並啟用拓撲</p></td>
<td><p>拓撲產生器</p>
<p>-或-</p>
<p>Publish-CsTopology 和 Enable-CsTopology</p></td>
</tr>
<tr class="odd">
<td><p>啟用上次發行的拓撲</p></td>
<td><p>Enable-CsTopology</p></td>
</tr>
<tr class="even">
<td><p>重新安裝 Lync Server 元件</p></td>
<td><p>Lync Server 安裝程式</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>位在 Lync Server 安裝資料夾或媒體的 \setup\amd64\Setup.exe。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="odd">
<td><p>還原位置資訊 (E9-1-1) 資料 (Lis.mdf)</p></td>
<td><p>Import-CsLisConfiguration</p></td>
</tr>
<tr class="even">
<td><p>還原持續性使用者資料 (Rtcxds.mdf)</p></td>
<td><p>Import-CsUserData</p></td>
</tr>
<tr class="odd">
<td><p>還原回應群組設定資料 (RgsConfig.mdf)</p></td>
<td><p>Import-CsRgsConfiguration</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果設定是要還原在資料庫中沒有回應群組資料的新部署集區中，則應使用 –OverwriteOwner 選項。即使要還原的資料是在有著相同完整網域名稱 (FQDN) 的集區中，也請使用此選項，否則匯入將會失敗。這是因為回應群組的連絡人物件已經存在於 Active Directory 中。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>還原下列資料庫：</p>
<ul>
<li><p>封存資料庫 (LcsLog.mdf)</p></li>
<li><p>監視資料庫：詳細通話記錄資料庫 (LcsCDR.mdf) 及 QoE 資料庫 (QoEMetrics.mdf)</p></li>
</ul></td>
<td><p>SQL Server 資料庫管理工具</p></td>
</tr>
<tr class="odd">
<td><p>常設聊天室資料庫 (Mgs.mdf)</p></td>
<td><p>SQL Server 還原程序或 Import-CsPersistentChatData。您可以在使用 Import-CsPersistentChatData 時搭配 Export-CsPersistentChatData 建立的檔案，而資料將會匯入常設聊天室資料庫。</p></td>
</tr>
</tbody>
</table>


## 必要權限

使用者必須是 **RTCUniversalServerAdmins** 群組的成員才能執行本主題中說明的所有命令。大部分的備份和還原命令都不支援角色型存取控制 (RBAC)。兩個例外是常設聊天室 Cmdlet Export-CsPersistentChatData 和 Import-CsPersistentChatData，這兩個命令必須是由 CsPersistentChatAdministrator 群組成員的使用者來執行。若要執行 Lync Server 部署精靈，使用者也必須是本機系統管理員群組的成員。


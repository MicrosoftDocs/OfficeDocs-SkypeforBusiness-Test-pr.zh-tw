---
title: Set-CsArchivingServer
TOCTitle: Set-CsArchivingServer
ms:assetid: d4e51c14-34a6-4134-bb71-87bc2f11092d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398923(v=OCS.15)
ms:contentKeyID: 49292443
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingServer

 

_**上次修改主題的時間：** 2015-03-09_

可讓您指定一或多部封存伺服器的新資料庫位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsArchivingServer [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingDatabase <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會變更封存伺服器 ArchivingServer:atl-cs-001.litwareinc.com 的封存資料庫位置。在此範例中，新的資料庫位於 ArchivingDatabase:atl-sql-001.litwareinc.com。

    Set-CsArchivingServer -Identity "ArchivingServer:atl-cs-001.litwareinc.com" -ArchivingDatabase "ArchivingDatabase:atl-sql-001.litwareinc.com"

## 詳細描述

封存伺服器提供一種方法，讓您能夠儲存組織中所有立即訊息 (IM) 工作階段的完整記錄。對於某些組織來說，保存這些 IM 工作階段的複本是很有用的。對於其他必須保存所有電子通訊記錄的組織來說，它們必須遵從法規保存這些 IM 工作階段的複本。

封存伺服器 會將每個 IM 工作階段 (連同工作階段的開始時間和參與工作階段的人員等資訊) 的記錄存放於 SQL Server 資料庫中。在安裝 封存伺服器 時您必須指定該資料庫的位置，而在大部分的情況下並不需要變更該資料庫的位置。然而在發生硬體故障或其他問題時，您可以使用 **Set-CsArchivingServer** Cmdlet，將封存伺服器指向新的資料庫。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsArchivingServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingServer"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>新 封存資料庫 所在的服務位置。例如：-ArchivingDatabase ArchivingDatabase:atl-sql-001.litwareinc.com.在指定資料庫位置時，請務必使用服務位置而避免使用 SQL Server 路徑。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之 封存伺服器 的服務位置。例如：-Identity ArchivingServer:atl-cs-001.litwareinc.com。您可以執行下列命令以擷取所有封存伺服器的服務位置：</p>
<p>Get-CsService –ArchivingServer | Select-Object Identity</p>
<p>請注意，當您在指定封存伺服器時，可以省略首碼 &quot;ArchivingServer:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Set-CsArchivingServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsArchivingServer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayArchivingServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)


---
title: Remove-CsArchivingConfiguration
TOCTitle: Remove-CsArchivingConfiguration
ms:assetid: d83b8935-079e-47d0-ba48-c95dd07965c0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398951(v=OCS.15)
ms:contentKeyID: 49292470
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsArchivingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的封存設定集合。封存設定可用於啟用或停用自動儲存立即訊息 (IM) 工作階段功能，以及視情況封鎖無法封存的立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsArchivingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Remove-CsArchivingConfiguration** Cmdlet，來刪除 Identity 為 site:Redmond 的封存組態設定。

    Remove-CsArchivingConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會移除已在網站範圍設定的所有封存組態設定。為達成此目的，命令會先使用 **Get-CsArchivingConfiguration** Cmdlet 搭配 Filter 參數，以傳回在網站範圍設定之所有設定的集合。作法是使用篩選值 "site:\*"，將傳回的資料限制在 Identity 開頭為 "site:" 字元的設定。然後將篩選後的集合管線傳送到 **Remove-CsArchivingConfiguration** Cmdlet，以刪除該集合中的每一個項目。

    Get-CsArchivingConfiguration -Filter "site:*" | Remove-CsArchivingConfiguration

## 範例 3

範例 3 會刪除 EnableArchiving 屬性已設為 "None" 的所有封存組態設定。為了執行此工作，會呼叫不含任何參數的 **Get-CsArchivingConfiguration** Cmdlet，以傳回設定供組織使用之所有封存設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnableArchiving 屬性等於 "None" 的設定。接著將篩選後的集合管線傳送到 **Remove-CsArchivingConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsArchivingConfiguration | Where-Object {$_.EnableArchiving -eq "None"} | Remove-CsArchivingConfiguration

## 詳細描述

有許多組織認為，保留使用者參與之所有 IM 工作階段和會議的記錄是相當有用的。另外，也有一些組織會強制保留這些記錄。例如，根據法律規定，許多金融界的組織都必須保留所有電子通訊的副本。

就封存 IM 和網路會議工作階段而言，Lync Server 可讓您根據需求彈性地選擇。如果您已部署 封存伺服器，便能使用各種 **CsArchivingConfiguration** Cmdlet 來啟用及停用 IM 工作階段的封存功能，以及管理您的封存資料庫。而在封存失敗時，您也可以藉由暫停 IM 來確保所有電子通訊均能納入記錄。

在安裝 Lync Server 時，系統會為您建立全域封存設定的集合。根據預設，這些設定會套用至整個組織。或者，您也可以使用 **New-CsArchivingConfiguration** Cmdlet，以在網站間建立自訂的組態設定。您日後可以使用 **Remove-CsArchivingConfiguration** Cmdlet，來移除所有使用 **New-CsArchivingConfiguration** Cmdlet 建立之網站特定的設定。移除網站的設定之後，受影響的網站接著將改由全域設定來管理。

請注意，您也可以針對全域封存設定執行 **Remove-CsArchivingConfiguration** Cmdlet。但在此情況下，將不會移除設定，原因在於您無法刪除全域設定，而只會將所有全域屬性重設為預設值。例如，假設您已在全域範圍啟用 IM 工作階段封存功能，而稍後您執行了下列命令：

Remove-CsArchivingConfiguration -Identity global

執行該命令將會重設全域設定的屬性值；這表示，EnableArchiving 將回復成預設值 None。如此一來，全域範圍內的封存功能都將停用。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsArchivingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsArchivingConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之封存組態設定集合的唯一識別碼。若要移除全域集合，請使用下列語法：-Identity global (請注意，您不能真正移除全域設定，只能將屬性重設為預設值)。若要移除網站集合，請使用類似下列的語法：-Identity site:Redmond。若要移除針對個別登錄器集區設定的設定，語法如下：</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p>
<p>請注意，集區層級的設定僅適用於 Lync Server 2013。</p>
<p>在指定原則 Identity 時不能使用萬用字元。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings 物件。**Remove-CsArchivingConfiguration** Cmdlet 接受封存組態物件的管線傳送輸入。

## 傳回類型

**Remove-CsArchivingConfiguration** Cmdlet 不會傳回值或物件，而是會移除 Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)  
[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)


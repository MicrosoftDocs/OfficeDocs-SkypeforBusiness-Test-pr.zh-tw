---
title: Remove-CsFileTransferFilterConfiguration
TOCTitle: Remove-CsFileTransferFilterConfiguration
ms:assetid: faae4d4b-ea8b-4d50-9c46-16a075476642
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413064(v=OCS.15)
ms:contentKeyID: 49292883
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsFileTransferFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的立即訊息檔案傳輸篩選組態 (立即訊息檔案傳輸篩選設定可用於禁止使用者透過立即訊息傳輸特定類型的檔案)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsFileTransferFilterConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Remove-CsFileTransferFilterConfiguration** Cmdlet 移除 Identity 為 site:Redmond 的檔案傳輸篩選組態。

    Remove-CsFileTransferFilterConfiguration -Identity site:Redmond

## 範例 2

範例 2 會移除在網站範圍的檔案傳輸篩選組態。為達成此目的，命令會先使用 **Get-CsFileTransferFilterConfiguration** Cmdlet 搭配 Filter 參數，以傳回網站範圍上的所有組態。篩選值 "site:\*" 會指示 **Get-CsFileTransferFilterConfiguration** Cmdlet 只傳回 Identity 開頭字串值為 "site:" 的組態。然後再將篩選後的組態集合管線傳送到 **Remove-CsFileTransferFilterConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsFileTransferFilterConfiguration -Filter site:* | Remove-CsFileTransferFilterConfiguration

## 範例 3

範例 3 顯示如何移除目前停用的所有檔案傳輸篩選組態。為達成此目的，命令會先使用 **Get-CsFileTransferFilterConfiguration** Cmdlet 傳回組織目前所使用之所有檔案傳輸篩選組態的集合。然後再將該資訊管線傳送到 **Where-Object** Cmdlet，這會只選取 Enabled 屬性等於 (-eq) False ($False) 的檔案傳輸篩選組態。接著將篩選後的集合管線傳送到 **Remove-CsFileTransferFilterConfiguration** Cmdlet，以繼續移除篩選後之集合中的每個項目。

    Get-CsFileTransferFilterConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsFileTransferFilterConfiguration

## 詳細描述

傳送立即訊息時，使用者可以附加並傳送檔案給交談中的其他參與者。Lync Server 可加以設定，如此便不允許使用 Lync Server 用戶端來傳送含特定副檔名的檔案 (特別是可能證明有害之檔案類型的副檔名)。

**Remove-CsFileTransferFilterConfiguration** Cmdlet 能讓您刪除檔案傳輸篩選設定。針對網站範圍上的組態，**Remove-CsFileTransferFilterConfiguration** Cmdlet 會移除設定；然後網站上的使用者會自動繼承全域檔案傳輸篩選組態。**Remove-CsFileTransferFilterConfiguration** Cmdlet 也可以根據全域組態來執行。不過，在該情況下將不會移除全域組態；而是將該組態中的所有屬性重設為其預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsFileTransferFilterConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsFileTransferFilterConfiguration"}

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
<td><p>要移除之檔案傳輸組態的唯一識別碼。若要參照全域組態，請使用下列語法：-Identity global。若要在網站範圍內參照組態，請使用類似下列的語法：-Identity site:Redmond。請注意，您無法在指定 Identity 時使用萬用字元值。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 物件。接受檔案傳輸篩選組態物件管線傳送的輸入。

## 傳回類型

這個 Cmdlet 不會傳回值或物件，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsFileTransferFilterConfiguration](new-csfiletransferfilterconfiguration.md)  
[Set-CsFileTransferFilterConfiguration](set-csfiletransferfilterconfiguration.md)  
[Get-CsFileTransferFilterConfiguration](get-csfiletransferfilterconfiguration.md)


---
title: Remove-CsDeviceUpdateConfiguration
TOCTitle: Remove-CsDeviceUpdateConfiguration
ms:assetid: 4335eb24-61a6-4e76-8242-edfd861d7d0b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425933(v=OCS.15)
ms:contentKeyID: 49290748
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDeviceUpdateConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的裝置更新組態設定。這些設定可用於管理裝置更新 Web 服務。亦即 Lync Server 元件可讓系統管理員將韌體更新散發到電話及其他執行 Lync Phone Edition 的裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDeviceUpdateConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Remove-CsDeviceUpdateConfiguration** Cmdlet 用於「移除」全域裝置更新組態設定。因為全域設定無法真的移除，所以命令不會刪除任何設定，但全域裝置更新組態設定中的所有屬性將重設為其預設值。

    Remove-CsDeviceUpdateConfiguration -Identity global

## 範例 2

範例 2 所示的命令會移除 Identity 為 site:Redmond 的裝置更新組態設定。因為這些設定是在網站範圍設定，所以將會遭刪除，Redmond 網站也不再有自己的裝置更新組態設定集。

    Remove-CsDeviceUpdateConfiguration -Identity site:Redmond

## 範例 3

在範例 3 中，所有已在網站範圍設定的裝置更新組態設定皆會移除。為達此目的，會使用 **Get-CsDeviceUpdateConfiguration** Cmdlet 搭配 Filter 參數，以傳回所有 Identity 開頭為字串值 "site:" 的設定 (根據定義，這些是在網站範圍設定的設定)。然後再將該集合管線傳送到 **Remove-CsDeviceUpdateConfiguration** Cmdlet，以移除集合中的每個項目。

    Get-CsDeviceUpdateConfiguration -Filter "site:*" | Remove-CsDeviceUpdateConfiguration 

## 範例 4

在範例 4 中，所有其 MaxLogFileSize 屬性大於 1024000 位元組的裝置更新組態設定皆會刪除。若要完成此工作，先呼叫 **Get-CsDeviceUpdateConfiguration** Cmdlet 以傳回所有裝置更新組態設定之集合。此集合便會傳送到 **Where-Object** Cmdlet，這會只選取其 MaxLogFileSize 屬性大於 1024000 位元組的組態設定。此篩選的集合接著被傳送到 **Remove-CsDeviceUpdateConfiguration** Cmdlet，這會刪除集合中的每個項目。

    Get-CsDeviceUpdateConfiguration | Where-Object {$_.MaxLogFileSize -lt 1024000} | Remove-CsDeviceUpdateConfiguration

## 詳細描述

裝置更新 Web 服務提供方法讓系統管理員將韌體更新分送到執行 Lync Phone Edition 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server。在測試和核准這些規則之後，便可在適當裝置連線至系統時套用到這些裝置。裝置在最初開啟電源時會檢查更新，然後在使用者登入時再次檢查。之後，裝置每隔 24 小時檢查一次更新。

Lync Server 使用裝置更新組態設定來管理裝置更新 Web 服務，這些組態設定可套用在全域範圍或網站範圍內。預設只有在全域範圍才有這些設定，但您可以使用 **New-CsDeviceUpdateConfiguration** Cmdlet 也在網站範圍指派自訂的設定。

此外，您可以使用 **Remove-CsDeviceUpdateConfiguration** Cmdlet 刪除已在網站範圍指派的設定。當您對網站執行此 Cmdlet 時，系統會移除指派給該網站的裝置更新組態設定。您也可以對全域設定執行 **Remove-CsDeviceUpdateConfiguration** Cmdlet。但在此狀況下不會移除全域設定；因為您無法移除全域裝置更新組態設定。而是全域屬性會重設為其預設值。例如，假設您已將全域屬性 MaxLogCacheLimit 變更為 1,024,000 位元組。如果您對全域設定執行 **Remove-CsDeviceUpdateConfiguration** Cmdlet，則不會移除全域設定，但任何已修改的全域設定將重設回其預設值。這表示 MaxLogCacheLimit 將重設回 512,000 位元組。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDeviceUpdateConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDeviceUpdateConfiguration"}

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
<td><p>指出要移除之裝置更新組態設定的 Identity。若要參照全域設定，請使用下列語法：-Identity global。若要參照網站設定，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration 物件。**Remove-CsDeviceUpdateConfiguration** Cmdlet 接受裝置更新組態物件管線傳送的執行個體。

## 傳回類型

無。反之，**Remove-CsDeviceUpdateConfiguration** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)  
[New-CsDeviceUpdateConfiguration](new-csdeviceupdateconfiguration.md)  
[Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md)


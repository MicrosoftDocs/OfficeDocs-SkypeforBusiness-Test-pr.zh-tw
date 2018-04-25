---
title: Remove-CsTrunkConfiguration
TOCTitle: Remove-CsTrunkConfiguration
ms:assetid: 45546534-1a18-4db2-be61-850bacf55a52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425943(v=OCS.15)
ms:contentKeyID: 49290775
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrunkConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有描述對等主幹實體 (例如服務提供者的公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或工作階段邊界控制器 (SBC)) 的主幹組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsTrunkConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity 為 site:Redmond 的主幹組態。

    Remove-CsTrunkConfiguration -Identity site:Redmond

## 範例 2

範例 2 會移除在網站層級定義的所有主幹組態。命令的第一部分會呼叫 **Get-CsTrunkConfiguration** Cmdlet，該 Cmdlet 會使用 Filter 參數來擷取 Identity 開頭為 site: 的所有主幹組態 (亦即所有在網站層級定義的主幹組態)。此組態集合會被傳送到 **Remove-CsTrunkConfiguration** Cmdlet，移除集合內的每一個物件。

    Get-CsTrunkConfiguration -Filter site:* | Remove-CsTrunkConfiguration

## 詳細描述

使用此 Cmdlet 移除適用於 PSTN 閘道實體的主幹組態。每個組態均含有對等主幹實體 (例如，服務提供者的 PSTN 閘道、IP-PBX 或 SBC) 的專屬設定。這些設定所設定的項目包括此主幹是否啟用媒體旁路、是否在特定情況下傳送即時傳輸控制通訊協定 (RTCP) 封包，以及是否需要安全即時通訊協定 (SRTP) 加密。

請注意，如果您在全域組態上呼叫 **Remove-CsTrunkConfiguration** Cmdlet，則不會移除該主幹組態。而是組態會被「重設」，且會以預設值取代所有自訂設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsTrunkConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrunkConfiguration"}

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
<td><p>您要移除之主幹組態的唯一識別碼。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 物件。接受主幹組態物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)


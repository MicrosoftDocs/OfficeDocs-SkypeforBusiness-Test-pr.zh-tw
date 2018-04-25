---
title: Remove-CsBandwidthPolicyServiceConfiguration
TOCTitle: Remove-CsBandwidthPolicyServiceConfiguration
ms:assetid: cf920168-3f65-4747-86cd-d3e287c84349
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398877(v=OCS.15)
ms:contentKeyID: 49292372
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsBandwidthPolicyServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的頻寬原則服務組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsBandwidthPolicyServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除為 Redmond 網站 (-Identity site:Redmond) 定義的頻寬原則服務組態。

    Remove-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

## 範例 2

範例 2 會移除所有停用記錄功能的頻寬原則服務組態。為了完成此工作，範例一開始會呼叫 **Get-CsBandwidthPolicyServiceConfiguration** Cmdlet。如此將傳回 Lync Server 部署中所有頻寬原則服務組態的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以將集合範圍縮小到只剩下 EnableLogging 屬性等於 (-eq) False ($False) 的組態。這樣一來，集合中便只剩下已停用記錄功能的組態。最後將此集合管線傳送到 **Remove-CsBandwidthPolicyServiceConfiguration** Cmdlet，以移除集合中的每一個項目。

    Get-CsBandwidthPolicyServiceConfiguration | Where-Object {$_.EnableLogging -eq $False} | Remove-CsBandwidthPolicyServiceConfiguration

## 詳細描述

通話許可控制 (CAC) 是一種根據頻寬限制，判斷是否允許建立即時通訊工作階段 (例如語音或視訊通話) 的方式。在 Lync Server 的 CAC 實作中，地區、網站及子網路是在網路中與這些實體之間的關係和連結一起定義，以便對它們之間的頻寬加上限制。頻寬原則服務是在 Lync Server 部署中執行 CAC 功能的元件，能判斷目前是否有足夠的頻寬可建立通話。這個 Cmdlet 可移除在服務層級定義的頻寬原則服務組態。儘管您也可以使用該 Cmdlet 來「移除」全域頻寬原則服務，然而事實上，您無法真正移除全域服務，只能將它重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsBandwidthPolicyServiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBandwidthPolicyServiceConfiguration"}

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
<td><p>您要移除之組態的唯一識別碼。此識別碼將由範圍 (全域組態) 或是範圍和名稱 (網站層級組態，如 site:Redmond) 所組成。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration 物件。接受頻寬原則服務組態物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會 Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)


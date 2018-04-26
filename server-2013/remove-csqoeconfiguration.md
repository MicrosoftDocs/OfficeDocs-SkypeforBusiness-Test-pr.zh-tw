---
title: Remove-CsQoEConfiguration
TOCTitle: Remove-CsQoEConfiguration
ms:assetid: 3b50e857-c524-4aad-b191-d324fc7c837c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425879(v=OCS.15)
ms:contentKeyID: 49290643
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsQoEConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除 QoE (Quality of Experience) 設定的集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsQoEConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Remove-CsQoEConfiguration** Cmdlet 移除指派給 Redmond 網站的 QoE 設定。使用 Identity 參數可確保只移除指派給指定網站的設定。

    Remove-CsQoEConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會移除已在網站範圍指派的所有 QoE 設定。為達成此目的，此命令會先使用 **Get-CsQoEConfiguration** Cmdlet 搭配 Filter 參數擷取適當的 QoE 設定；萬用字元字串 "site:\*" 可確保只傳回 Identity 開頭為字串值 site: 的設定。接著，篩選過的集合會傳送到 **Remove-CsQoEConfiguration** Cmdlet，以刪除集合中的所有項目。

    Get-CsQoEConfiguration -Filter site:* | Remove-CsQoEConfiguration

## 範例 3

範例 3 會刪除 KeepQoEDataForDays 屬性小於 30 的所有 QoE 設定。為達此目的，命令會先呼叫不含任何參數的 **Get-CsQoEConfiguration** Cmdlet ，以傳回組織目前所使用之所有 QoE 設定的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，，這會只挑出 KeepQoEDataForDays 屬性小於 (-lt) 30 天的設定。接著將篩選後的集合以管線傳送到 **Remove-CsQoEConfiguration** Cmdlet，以刪除該集合中的每一個項目。

    Get-CsQoEConfiguration | Where-Object {$_.KeepQoEDataForDays -lt 30} | Remove-CsQoEConfiguration

## 詳細描述

QoE 計量會追蹤組織內執行的音訊與視訊通話品質，包括網路封包遺失數目、背景雜訊，以及「抖動」(封包延遲中的差異) 的數目等等。這些計量都會儲存在資料庫中，除了其他資料 (例如通話詳細記錄) 之外，讓您可啟用和停用與其他資料記錄無關的 QoE。使用此 Cmdlet 可移除在網站層級設定 QoE 的設定。在全域 QoE 組態呼叫此 Cmdlet 會將所有屬性重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsQoEConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsQoEConfiguration"}

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
<td><p>您要移除之設定的唯一識別碼。可能的值為 global 和 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是您 Lync Server 部署中具有要移除之設定的網站的名稱。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings 物件。接受 QoE 組態物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)  
[Get-CsQoEConfiguration](get-csqoeconfiguration.md)


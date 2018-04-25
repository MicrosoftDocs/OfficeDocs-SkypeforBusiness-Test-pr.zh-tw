---
title: Remove-CsOutboundTranslationRule
TOCTitle: Remove-CsOutboundTranslationRule
ms:assetid: 73e0bd0d-2458-464a-9e6e-1868143aadc8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398556(v=OCS.15)
ms:contentKeyID: 49291331
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsOutboundTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的外撥轉譯規則。外撥轉譯規則會將電話號碼轉換成當地的撥號格式，以與專用交換機 (PBX) 系統互動。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsOutboundTranslationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除名稱為 Prefix Redmond 之 Redmond 網站的現有外撥轉譯規則。Identity 是唯一的，因此此命令會刪除單一規則。

    Remove-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## 範例 2

此範例會移除所有網站層級的外撥轉譯規則。此命令的第一部分會呼叫包含 Filter site:\* 的 **Get-CsOutboundTranslationRule** Cmdlet，以傳回 Identity 值開頭為 site: 的所有規則集合。接著會將此集合管線傳送到 **Remove-CsOutboundTranslationRule** Cmdlet，以移除集合中的每個規則。

    Get-CsOutboundTranslationRule -Filter site:* | Remove-CsOutboundTranslationRule

## 詳細描述

呼叫此 Cmdlet 可移除現有的外撥轉譯規則。Lync Server 會將電話號碼正規化為 E.164 格式。不過，許多專用交換機 (PBX) 系統無法使用此格式。將號碼傳送到中繼伺服器或閘道之前，外撥轉譯規則會將號碼轉譯為區域撥號格式。

每個外撥轉譯規則都會與一個主幹組態相關聯。也就是說，使用此 Cmdlet 移除規則時，會將其從對應範圍的主幹組態中移除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsOutboundTranslationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsOutboundTranslationRule"}

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
<td><p>您要移除之外撥轉譯規則的唯一識別碼。Identity 是由範圍加上每個範圍中的唯一名稱組成。例如，site:Redmond/OutboundRule1。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 物件。接受外撥轉譯規則物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 類型的物件。

## 請參閱

#### 其他資源

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)


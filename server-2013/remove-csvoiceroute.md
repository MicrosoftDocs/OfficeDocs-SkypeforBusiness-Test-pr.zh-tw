---
title: Remove-CsVoiceRoute
TOCTitle: Remove-CsVoiceRoute
ms:assetid: 6687e538-e8f6-4bf0-b393-2c7b4a3f2f06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398468(v=OCS.15)
ms:contentKeyID: 49291156
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceRoute

 

_**上次修改主題的時間：** 2015-03-09_

移除語音路由。語音路由所含的指示會指示 Lync Server 如何將 Enterprise Voice 使用者的來電，路由到公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsVoiceRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

移除識別為 Route1 的語音路由設定。

    Remove-CsVoiceRoute -Identity Route1

## 範例 2

這個命令會移除組織中所有的語音路由。首先由 **Get-CsVoiceRoute** Cmdlet 擷取所有的語音路由。然後將這些語音路由管線傳送至 **Remove-CsVoiceRoute** Cmdlet，進而移除每個路由。

    Get-CsVoiceRoute | Remove-CsVoiceRoute

## 範例 3

這個命令會移除識別中包含字串 "Redmond" 的所有語音路由。首先會呼叫 **Get-CsVoiceRoute** Cmdlet 並搭配 Filter 參數。Filter 參數的值是 Redmond 字串且前後加上萬用字元 (\*)，這樣會指定該字串可在 Identity 內的任何位置。在擷取識別中包含字串 Redmond 的所有語音路由之後，便會將這些語音路由管線傳送至 **Remove-CsVoiceRoute** Cmdlet，這樣會移除每個路由。

    Get-CsVoiceRoute -Filter *Redmond* | Remove-CsVoiceRoute

## 詳細描述

使用此 Cmdlet 移除現有的語音路由。語音路由透過 PSTN 使用方式和語音原則相關聯，因此移除語音路由並不會變更和語音原則相關的任何值，只會變更和刪除之語音路由模式相符之號碼的路由。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsVoiceRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceRoute"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>唯一識別您要刪除之語音路由的字串(如果路由名稱包含空格 (例如 Test Route)，必須使用雙引號括住整個字串)。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件。接受語音路由物件管線傳送的輸入。

## 傳回類型

移除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)


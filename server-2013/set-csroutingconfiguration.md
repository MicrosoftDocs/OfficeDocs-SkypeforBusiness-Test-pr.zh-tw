---
title: Set-CsRoutingConfiguration
TOCTitle: Set-CsRoutingConfiguration
ms:assetid: ab69c6e8-262a-4ecb-b1af-513383c494fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412811(v=OCS.15)
ms:contentKeyID: 49291960
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改語音路由的清單。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

修改路由組態中的語音路由有幾個步驟。在此範例中，我們一開始會先呼叫 **Get-CsRoutingConfiguration** Cmdlet，以擷取路由組態物件。然後將擷取的物件 (只會有一個) 指派給變數 $a。

在此範例的第 2 行，則從變數 $a 擷取 Route 屬性的內容，這個變數是語音路由物件的集合。接著，將該集合傳送至 **Where-Object** Cmdlet，由其搜尋 Name 與字串 LocalRoute 相符之所有語音路由物件的集合。我們將該物件指定到變數 $b。

接下來，我們為 SuppressCallerId 屬性指派 $False 值，以修改 LocalRoute 語音路由物件。更新該物件，即可更新變數 $a 中的物件。但是該物件仍然只留在記憶體中。最後一個步驟是需要儲存那些變更，方法是將 $a 傳遞到 **Set-CsRoutingConfiguration** Cmdlet 的 Instance 參數。

這並不是修改路由組態的建議方式。若要修改路由組態，只需使用 **Set-CsVoiceRoute** Cmdlet 變更個別語音路由，如下所示：

Set-CsVoiceRoute -Identity LocalRoute -SuppressCallerId $False

這一行會完成範例 1 所示的相同工作。

    $a = Get-CsRoutingConfiguration
    $b = $a.Route | Where-Object {$_.Name -match "LocalRoute"}
    $b.SuppressCallerId = $False
    Set-CsRoutingConfiguration -Instance $a

## 詳細描述

語音路由包含一些指示，告知 Lync Server 如何將 Enterprise Voice 使用者的來電轉接至公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。使用這個 Cmdlet，可以修改在 Lync Server 部署內定義之任何語音路由的設定。

不建議使用這個 Cmdlet。若要修改路由設定，可呼叫 **Set-CsVoiceRoute** Cmdlet，修改個別的語音路由。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRoutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRoutingConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，語音路由的管理將會同時考量撥打電話與接聽電話的位置。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>路由組態的範圍。這必須是 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>路由組態 (Microsoft.Rtc.Management.WritablConfig.Policy.Voice.PstnRoutingSettings) 物件。呼叫 <strong>Get-CsRoutingConfiguration</strong> Cmdlet 可擷取此類型的物件。</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>針對 Lync Server 部署定義的所有語音路由清單 (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件)。</p>
<p>您應該使用 <strong>Set-CsVoiceRoute</strong> Cmdlet，修改個別的語音路由物件。那是修改此清單中之路由的建議方式。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.WritableConfig.Management.Policy.Voice.PSTNRoutingSettings 物件。接受路由組態物件管線傳送的輸入。

## 傳回類型

**Set-CsRoutingConfiguration** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)


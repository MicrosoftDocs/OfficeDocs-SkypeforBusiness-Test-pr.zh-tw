---
title: Set-CsVoiceRoute
TOCTitle: Set-CsVoiceRoute
ms:assetid: b786aec0-946e-4ce5-812e-25e5d8cfa4d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412893(v=OCS.15)
ms:contentKeyID: 49292103
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoute

 

_**上次修改主題的時間：** 2015-03-09_

修改語音路由。語音路由所含的指示會指示 Lync Server 如何將 Enterprise Voice 使用者的來電，路由到公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個命令將 Route1 語音路由的 Description 設定為 "Test Route"。

    Set-CsVoiceRoute -Identity Route1 -Description "Test Route"

## 範例 2

此範例中的命令會修改識別身分為 Route1 的語音路由，將 PSTN 使用方式 Long Distance 加入此語音路由的使用方式清單。Long Distance 必須位於全域 PSTN 使用方式的清單中 (呼叫 **Get-CsPstnUsage** Cmdlet 即可擷取此清單)。

    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"}

## 範例 3

此範例會修改名為 Route1 的語音路由，在該路由的 PSTN 使用方式清單中填入組織所有的現有電話使用方式。此範例的第一個命令會擷取全域 PSTN 使用方式的清單。請注意，**Get-CsPstnUsage** Cmdlet 的呼叫會以括弧括住，表示我們先擷取包含 PSTN 使用方式資訊的物件 (因為只有一個全域 PSTN 使用方式，只會擷取一個物件)。命令接著會擷取此物件的 Usage 屬性。該屬性 (包含使用方式清單) 會指派給 $x 變數。此範例的第二行會呼叫 **Set-CsVoiceRoute** Cmdlet，以修改識別身分為 Route1 的語音路由。請注意傳遞給 PstnUsages 參數的值：@{replace=$x}。此值表示會使用 $x 的內容來取代此路由之 PstnUsages 清單中的所有內容，其中包含在第 1 行擷取的 PSTN 使用方式清單。

    $x = (Get-CsPstnUsage).Usage
    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{replace=$x}

## 範例 4

這組命令會將識別身分為 Route1 之語音路由的 Name 屬性變更為 RouteA。變更 Name 屬性會自動變更 Identity 屬性，在此範例中會變更為 RouteA。

第一行會呼叫 **Get-CsVoiceRoute** Cmdlet，以擷取識別身分為 Route1 的語音路由。傳回的物件會儲存於變數 $x 中。接著為該物件的 Name 屬性指派字串值 "RouteA"。最後，將變數 $x 中所含的物件傳遞到 **Set-CsVoiceRoute** Cmdlet 的 Instance 參數以進行變更。

    $x = Get-CsVoiceRoute -Identity Route1
    $x.Name = "RouteA"
    Set-CsVoiceRoute -Instance $x

## 範例 5

此範例會修改名為 Route1 的語音路由，並在該路由的 PSTN 閘道清單 (PstnGatewayList) 中填入識別身分為 PstnGateway:192.168.0.100 的閘道伺服器角色。此範例的第一行會呼叫 **Get-CsVoiceRoute** Cmdlet，以擷取要修改的語音路由，在此範例中為 Route1。接著在 Route1 的 PstnGatewayList 屬性上呼叫 Add 方法。我們會將 Add 方法傳遞到要新增之服務的 Identity。最後呼叫 **Set-CsVoiceRoute** Cmdlet，將 Instance 參數傳遞到變數 $y，這樣將會以新加入的 PSTN 閘道更新 Route1 (儲存於 $y 中)。

    $y = Get-CsVoiceRoute -Identity Route1
    $y.PstnGatewayList.Add("PstnGateway:192.168.0.100")
    Set-CsVoiceRoute -Instance $y

## 詳細描述

使用此 Cmdlet 修改現有的語音路由。語音路由透過公用交換電話網路 (PSTN) 使用方式而與語音原則產生關聯。語音路由包含規則運算式，可識別將經由指定的語音路由來轉接的電話號碼：符合規則運算式的電話號碼會經由此路由來轉接。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsVoiceRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoute"}

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
<td><p><em>AlternateCallerId</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如果 SuppressCallerId 參數設為 True，則會顯示 AlternateCallerId 參數的值以接收各通話方，而非來電者的實際號碼。此號碼應該為有效號碼，且可用來代表組織內的部門，例如「支援」或「人力資源」。</p>
<p>如果 SuppressCallerId 參數設為 False，則會忽略 AlternateCallerId 參數。</p>
<p>此值必須符合規則運算式 (\+)?[1-9]\d*(;ext=[1-9]\d*)?。換言之，值的開頭可以是加號 (+)，但不一定必須是加號；必須由任何數目的數字組成；後面可以接著以 ;ext= 開頭的分機，最後再接著任何數目的數字(請注意，如果加入分機，則必須以雙引號括住字串)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此電話路由用途的描述。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>語音路由的唯一識別身分 (如果路由名稱包含空格 (例如 Test Route)，必須使用括弧括住整個字串)。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>路由</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。 此物件必須是 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 類型，呼叫 <strong>Get-CsVoiceRoute</strong> Cmdlet 即可擷取此物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberPattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定套用此路由之電話號碼的規則運算式。符合此模式的號碼將根據其餘路由設定來轉接。例如，預設號碼模式 [0-9]{10} 指定包含 0 到 9 之任何數字的 10 位數號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>數字可解析至多個語音路由。如果有多個路由，則優先順序可決定套用路由的順序。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>一個 中繼伺服器 可以與多個閘道產生關聯。此參數包含與此語音路由相關聯的閘道清單。此清單的每一個成員必須是 PSTN 閘道或 中繼伺服器 的服務識別碼。唯有在針對 Microsoft Office Communications Server 2007 或 Microsoft Office Communications Server 2007 R2 設定中繼伺服器後，此值才能參照中繼伺服器。對於 Lync Server，PSTN 閘道是必須要使用的項目。Identity 服務是 ServiceRole:FQDN 格式的字串，其中 ServiceRole 為服務角色 (PSTNGateway) 的名稱，FQDN 是集區的完整網域名稱 (FQDN)，或該伺服器的 IP 位址。例如，PSTNGateway:redmondpool.litwareinc.com. Service 識別可透過呼叫 Get-CsService | Select-Object Identity 命令來擷取。</p>
<p>如果您變更語音路由並讓 PstnGatewayList 清單空白，或者如果您做的變更是移除清單中的所有項目，就會收到警告訊息表示使用者無法進行 PSTN 通話。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可套用至此語音路由的 PSTN 使用方式 (例如 Local 或 Long Distance)。PSTN 使用方式必須是現有的使用方式(您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取 PSTN使用方式)。</p>
<p>如果您變更語音路由並讓 PstnUsages 清單空白，或者如果您做的變更是移除清單中的所有 PSTN 使用方式，就會收到警告訊息表示使用者無法進行 PSTN 通話。</p></td>
</tr>
<tr class="odd">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定是否在撥出電話上顯示來電者的識別碼。如果此參數設為 True，則會隱藏來電者識別碼。將會顯示 AlternateCallerId 的值，而非實際識別碼。當 SuppressCallerId 設為 True 時，必須提供 AlternateCallerId 的值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件。**Set-CsVoiceRoute** Cmdlet 接受語音路由物件管線傳送的輸入。

## 傳回類型

**Set-CsVoiceRoute** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)


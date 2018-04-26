---
title: New-CsVoiceRoute
TOCTitle: New-CsVoiceRoute
ms:assetid: 1118f74f-b06c-41d2-8b1b-5cc1e1957b77
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398197(v=OCS.15)
ms:contentKeyID: 49290137
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRoute

 

_**上次修改主題的時間：** 2015-03-09_

建立新的語音路由。語音路由所含的指示會指示 Lync Server 如何將 Enterprise Voice 使用者的來電，路由到公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsVoiceRoute -Name <String> <COMMON PARAMETERS>

    New-CsVoiceRoute -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例中的命令會建立 Identity 為 Route1 的新語音路由。其他所有屬性會設為預設值。

    New-CsVoiceRoute -Identity Route1

## 範例 2

此範例中的命令會建立 Identity 為 Route1 的新語音路由。它也會將為 Long Distance 的 PSTN 使用方式新增至使用方式清單，將 PstnGateway:redmondpool.litwareinc.com 服務 ID 新增至 PSTN 閘道清單。

    New-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"} -PstnGatewayList @{add="PstnGateway:redmondpool.litwareinc.com"}

## 範例 3

此範例會建立名為 Route1 的新語音路由，並在路由的 PSTN 使用方式清單中填入組織的所有現有使用方式。此範例的第一個命令會擷取全域 PSTN 使用方式的清單。請注意，**Get-CsPstnUsage** Cmdlet 的呼叫會以括弧括住，表示我們先擷取包含 PSTN 使用方式資訊的物件 (因為只有一個全域 PSTN 使用方式，只會擷取一個物件)。命令接著擷取此物件的 Usage 屬性。該屬性 (包含使用方式清單) 會指派給 $x 變數。此範例的第二行會呼叫 **New-CsVoiceRoute** Cmdlet 以建立新的語音路由。此語音路由的識別為 Route1。請注意傳遞給 PstnUsages 參數的值：@{add=$x}。此值表示將 $x 的內容 (包含在線路 1 中擷取的電話使用方式清單) 新增到此路由的 PSTN 使用方式清單。

    $x = (Get-CsPstnUsage).Usage
    New-CsVoiceRoute -Identity Route1 -PstnUsages @{add=$x}

## 詳細描述

使用此 Cmdlet 來建立新的語音路由。所有語音路由都是在全域範圍上建立。不過，可以定義多個全域語音路由。作法是透過 Identity 參數，此參數需要唯一路由名稱。

語音路由透過 PSTN 使用方式與語音原則產生關聯。語音路由包含規則運算式，可識別將經由指定的語音路由來轉接的電話號碼：符合規則運算式的電話號碼會經由此路由來轉接。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsVoiceRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRoute"}

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
<td><p>可唯一識別語音路由的名稱。語音路由只能在全域範圍上定義，所以 Identity 只是您要提供給路由的名稱 (路由名稱中可以包含空格，例如 Test Route，但是在呼叫 <strong>New-CsVoiceRoute</strong> Cmdlet 時，必須以雙引號括住整個字串)。</p>
<p>如果已指定 Identity，Name 必須保留空白。Identity 的值會指派給 Name。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>語音路由的唯一名稱。如果設定此參數，值會自動套用至語音路由 Identity。您不能同時指定 Identity 和 Name。</p></td>
</tr>
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
<td><p>此語音路由用途的描述。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>NumberPattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定套用此路由之電話號碼的規則運算式。符合此模式的號碼將根據其餘路由設定來轉接。</p>
<p>預設值：[0-9]{10}</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>數字可解析至多個語音路由。如果有多個路由，則優先順序可決定套用路由的順序。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>在 Lync Server 中，一個中繼伺服器可以與多個閘道產生關聯。此參數包含與此語音路由相關聯的閘道清單。此清單的每一個成員必須是 PSTN 閘道或中繼伺服器的服務識別碼。唯有在針對 Microsoft Office Communications Server 2007 或 Microsoft Office Communications Server 2007 R2 設定中繼伺服器後，此值才能參照中繼伺服器。若為 Lync Server，PSTN 閘道是必須要使用的項目。Identity 服務是 &lt;ServiceRole&gt;:&lt;FQDN&gt; 格式的字串，其中 ServiceRole 為服務角色 (PSTNGateway) 的名稱，FQDN 是集區的完整網域名稱 (FQDN)，或該伺服器的 IP 位址。例如，PSTNGateway:redmondpool.litwareinc.com. Service 識別可透過呼叫 Get-CsService | Select-Object Identity 命令來擷取。</p>
<p>此清單預設為空白。但如果您在建立新語音路由時將此參數保留空白，則會收到警告訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可套用至此語音路由的 PSTN 使用方式 (例如 Local 或 Long Distance 等)。PSTN 使用方式必須是現有的使用方式(您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取 PSTN使用方式)。</p>
<p>此清單預設為空白。但如果您在建立新語音路由時將此參數保留空白，則會收到警告訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定是否在撥出電話上顯示來電者的識別碼。如果此參數設為 True，則會隱藏來電者識別碼。將會顯示 AlternateCallerId 的值，而非實際識別碼。當 SuppressCallerId 設為 True 時，必須提供 AlternateCallerId 的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)


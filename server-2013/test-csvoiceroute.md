---
title: Test-CsVoiceRoute
TOCTitle: Test-CsVoiceRoute
ms:assetid: 39d5012d-7beb-41c6-ac94-51011da04872
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425873(v=OCS.15)
ms:contentKeyID: 49290631
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceRoute

 

_**上次修改主題的時間：** 2015-03-09_

針對語音路由號碼模式測試電話號碼，然後傳回布林值 (True/False)，指出所提供之號碼是否符合路由的號碼模式。號碼模式只是語音路由所使用的屬性之一，可指示 Lync Server 如何將來自 Enterprise Voice 使用者的來電，路由到公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsVoiceRoute -Route <Route> -TargetNumber <PhoneNumber> [-Force <SwitchParameter>]

## 範例

## 範例 1

此命令會判斷指定號碼是否符合指定路由的模式。我們會先使用 **Get-CsVoiceRoute** Cmdlet 擷取語音路由 testroute。我們會使用該路由做為 **Test-CsVoiceRoute** Cmdlet 之 Route 參數的值。我們也會在 TargetNumber 參數中加入要測試的號碼。其輸出是一個布林值，表示目標號碼是否符合該路由的模式。

    $vr = Get-CsVoiceRoute -Identity testroute
    Test-CsVoiceRoute -TargetNumber "+14255551212" -Route $vr

## 範例 2

範例 2 會執行與範例 1 相同的動作。不過，在此範例中，該動作是在單一個命令中執行。我們會先呼叫 **Get-CsVoiceRoute** Cmdlet 以擷取具有 Identity testroute 的語音路由。我們將該語音路由以管線傳送到 **Test-CsVoiceRoute** Cmdlet，並針對 TargetNumber 參數中提供的號碼，測試該路由。請注意，我們不需要提供 Route 參數，因為路由已管線傳送到 Cmdlet 中。

    Get-CsVoiceRoute -Identity testroute | Test-CsVoiceRoute -TargetNumber "+14255551212"

## 範例 3

此範例會擷取 Lync Server 部署中所定義的所有語音路由集合，並針對 **Test-CsVoiceRoute** Cmdlet 的呼叫中提供的 TargetNumber，測試每個路由的號碼模式。針對每個測試的路由，其輸出將會是 True 或 False 值。

    Get-CsVoiceRoute | Test-CsVoiceRoute -TargetNumber "+14255551212"

## 範例 4

在針對多個路由擷取語音路由測試結果方面，此範例類似範例 3。不過，範例 3 的輸出只是一個 True/False 值的清單，並未清楚指出測試結果適用於哪一個路由。此範例會解決該問題 (若要使輸出更清楚，可以做幾件事情，但這個簡短的範例至少會完成該工作)。

首先，我們呼叫 **Get-CsVoiceRoute** Cmdlet 以擷取所有語音路由，並將集合指派給變數 $z。在下一行中，我們開始一個 foreach 迴圈。此迴圈每次會取用集合中的一個成員，並將它指派給變數 $x。針對 $x (其中包含單一語音路由的參考)，我們所做的第一件事是顯示該路由的 Identity：$x.Identity。該命令的下一個部分是呼叫 **Test-CsVoiceRoute** Cmdlet，其中會針對目標號碼測試路由 $x。最後的輸出將會是語音路由識別的清單，緊接著表示目標號碼是否符合具有該識別之路由中的號碼模式的 True/False 指示器 (輸出格式並不很理想)。

    $z = Get-CsVoiceRoute
    foreach ($x in $z){$x.Identity; Test-CsVoiceRoute -TargetNumber "+14255551212" -Route $x}

## 詳細描述

語音路由包含規則運算式，可識別將經由指定的語音路由來轉接的電話號碼：符合規則運算式的電話號碼會經由此路由來轉接。這個 Cmdlet 會驗證是否會根據路由的號碼模式 (NumberPattern 屬性)，透過指定的語音路由來轉接指定的電話號碼。您可以使用此 Cmdlet 疑難排解路由問題，或是只針對特定路由試驗電話號碼，以確定其結果如預期。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsVoiceRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceRoute"}

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
<td><p><em>Route</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route</p></td>
<td><p>包含語音路由參考的物件，您想要用此語音路由來測試 TargetNumber 參數中所指定的號碼。您可以呼叫 <strong>Get-CsVoiceRoute</strong> Cmdlet 來擷取語音路由物件。</p>
<p>完整資料類型：Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route</p></td>
</tr>
<tr class="even">
<td><p><em>TargetNumber</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>您想要測試在 Route 參數中指定之語音路由的電話號碼。此號碼應該採用 E.164 格式 (例如 +14255551212)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件。接受管線傳送的語音路由物件輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.Voice.VoiceRouteTestResult 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)


---
title: Set-CsDiagnosticConfiguration
TOCTitle: Set-CsDiagnosticConfiguration
ms:assetid: 26463da9-cd6a-4ea3-961c-2570a8801cba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425734(v=OCS.15)
ms:contentKeyID: 49290380
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDiagnosticConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的診斷組態設定。診斷組態設定可用於指定是否要將進出指定網域或統一資源識別元 (URI) 的流量記錄在 Lync Server 記錄檔中。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDiagnosticConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDiagnosticConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Filter <Filter>] [-Force <SwitchParameter>] [-LogAllSipHeaders <$true | $false>] [-LoggingShare <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會使用 **New-CsDiagnosticsFilter** Cmdlet 建立新的診斷篩選，然後將新篩選指派給全域診斷組態設定。為了執行此工作，第一個命令會呼叫 **New-CsDiagnosticsFilter** Cmdlet，以建立僅存於記憶體中的診斷篩選，該篩選會使用 FQDN fabrikam.com 和 URI sip:user@fabrikam.com。然後再將「虛擬」篩選儲存在 $x 變數中。

在命令 2 中， **Set-CsDiagnosticConfiguration** Cmdlet 會將新的篩選指派給全域範圍診斷組態設定。在此狀況下，任何存在於 Filter 屬性中的值都會替換為新建立的篩選。

    $x = New-CsDiagnosticsFilter -Fqdn fabrikam.com -Uri sip:user@fabrikam.com 
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## 範例 2

範例 2 會示範如何將新的 FQDN 新增至全域範圍診斷篩選組態設定的 Filter 屬性。為達成此目的，範例中的第一個命令會使用 **Get-CsDiagnosticConfiguration** Cmdlet 擷取全域設定的 Filter 屬性值。作法是將 **Get-CsDiagnosticConfiguration** Cmdlet 的呼叫放置在括弧中，如此會使 Windows PowerShell 命令列介面在執行其他任何工作之前，先執行該命令。傳回全域設定之後，會擷取 Filter 屬性的值並儲存在名稱為 $x 的變數中。

在第二個命令中，Add 方法用於將新的 FQDN (fabrikam.com) 新增至篩選。當此工作完成時，範例中的最後一個命令會使用 **Set-CsDiagnosticConfiguration** Cmdlet 來儲存修改後的診斷集合。最終結果是，fabrikam.com 將會新增至已包含在 Filter 屬性中的任何 FQDN。

    $x = (Get-CsDiagnosticConfiguration -Identity global).Filter
    $x.Fqdn.Add("fabrikam.com")
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## 範例 3

範例 3 所示的命令會從全域範圍診斷組態設定的 Filter 屬性中移除 FQDN (fabrikam.com)。範例中的第一個命令會使用 **Get-CsDiagnosticConfiguration** Cmdlet 擷取全域設定之 Filter 屬性的目前值；此值會儲存在名為 $x 的變數中。在擷取該值之後，會使用 Remove 方法移除 FQDN fabrikam.com。在移除 FQDN 之後，會使用 **Set-CsDiagnosticConfiguration** Cmdlet 將修改過的篩選 (儲存在 $x 變數中) 寫入全域設定。

    $x = (Get-CsDiagnosticConfiguration -Identity global).Filter
    $x.Fqdn.Remove("fabrikam.com")
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## 範例 4

在範例 4 中，全域範圍診斷組態設定之 Filter 屬性中的所有項目都會遭到移除。作法是將 Filter 屬性設為 Null 值。

    Set-CsDiagnosticConfiguration -Identity global -Filter $Null

## 詳細描述

如果您啟用 Lync Server 記錄功能，則這些記錄檔中預設會包含進出任何網域或 URI 的流量。這可確保記錄檔中會盡量記錄最多的資訊。

但是，這有時候會造成資訊過多。例如，當遇到特定網域的連線問題時，需要將記錄範圍限制在您網路與該網路間的流量；這樣您才能更容易識別相關記錄，進而更輕鬆地診斷並修正問題。

診斷組態設定可讓您指定要記錄在記錄檔中的網域或 URI。 Lync Server 可讓您在網站範圍內建立診斷組態設定。如此一來，您就可以將異於其他網站的設定套用至 Redmond 網站。

您可以使用 **Set-CsDiagnosticConfiguration** Cmdlet，在指定集合中新增或移除篩選。篩選可用來指定要記錄流量的網域。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDiagnosticConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDiagnosticConfiguration"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.Filter</p></td>
<td><p>要記錄流量之網域和 URI 的集合。Filter 內容含有三個不同的項目，並且需要使用 <strong>New-CsDiagnosticsFilter</strong> Cmdlet 來加以建立：</p>
<p>Fqdn – 要包含在篩選中的網域集合 (更嚴格來說，是 SIP 位址的主機部分)。例如，完整網域名稱 (FQDN ) 可能看起來如下所示：fabrikam.com。或者，可使用萬用字元來代表多個網域：*.fabrikam.com。您可以在單一篩選中包含多個網域。</p>
<p>Uri – 要包含在篩選中之 URI 的集合 (URI 代表 SIP 位址中的 user@host 部分)。URI 可以由下列任何模式所組成：user@fabrikam.com、user@* 或 *@fabrikam.com。您可以在單一篩選中包括多個 URI。</p>
<p>Enabled – 表示是否要啟用篩選。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之診斷組態設定的唯一識別碼。若要修改在網站範圍設定的設定值，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要修改全域設定，請使用下列語法：-Identity global。</p>
<p>如果未指定此參數，則 <strong>Set-CsDiagnosticConfiguration</strong> Cmdlet 將會自動修改全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DiagnosticFilterSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>LogAllSipHeaders</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 False，只有核心 SIP 標題會記錄到記錄檔中。將此值設為 False 有助於縮減記錄檔的大小。若設為 True，將會記錄所有的 SIP 標題。</p></td>
</tr>
<tr class="odd">
<td><p><em>LoggingShare</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>上傳診斷記錄的共用資料夾。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings 物件。 **Set-CsDiagnosticConfiguration** Cmdlet 接受管線傳送的診斷組態設定物件執行個體。

## 傳回類型

**Set-CsDiagnosticConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[New-CsDiagnosticsFilter](new-csdiagnosticsfilter.md)  
[Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)


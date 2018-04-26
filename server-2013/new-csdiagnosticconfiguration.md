---
title: New-CsDiagnosticConfiguration
TOCTitle: New-CsDiagnosticConfiguration
ms:assetid: 9028d9c1-e812-4055-bdf0-59cb83c6f50f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398733(v=OCS.15)
ms:contentKeyID: 49291652
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDiagnosticConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的診斷組態設定。診斷組態設定可用於指定是否要將進出指定網域或統一資源識別元 (URI) 的流量記錄在 Lync Server 記錄檔中。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDiagnosticConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Filter <Filter>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LogAllSipHeaders <$true | $false>] [-LoggingShare <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為 Redmond 網站建立新的診斷組態設定集合。

    New-CsDiagnosticConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會建立新的診斷篩選，然後將該篩選指派給新的診斷設定集合。為了執行此工作，第一個命令會呼叫 **New-CsDiagnosticsFilter** Cmdlet 來建立僅在於記憶體中的診斷篩選；此命令會將 FQDN fabrikam.com 和 URI sip:user@fabrikam.com 新增至篩選。此命令也會將 Enabled 屬性設為 ($True) 以啟動篩選。所產生的虛擬篩選接著會儲存於變數 $x 中。

命令 2 使用 **New-CsDiagnosticConfiguration** Cmdlet 為 Redmond 網站建立新的診斷組態設定集合。這些新設定將會使用變數 $x 中儲存的診斷篩選。

    $x = New-CsDiagnosticsFilter -Fqdn fabrikam.com -Uri "sip:user@fabrikam.com" -Enabled $False 
    
    New-CsDiagnosticConfiguration -Identity site:Redmond -Filter $x

## 範例 3

範例 3 所示的命令會示範如何建立一開始只存在於記憶體中的診斷組態設定。為達成此目的，第一個命令會呼叫 **New-CsDiagnosticConfiguration** Cmdlet 並搭配下列兩個參數：Identity (指定設定的 Identity) 和 InMemory (指示新設定只可建立在記憶體中)。產生的物件會儲存在 $x 變數中。

建立這些虛擬設定後，第二個命令可用來將 LoggingShare 屬性設定為 UNC 路徑 \\\\atl-fs-001\\logs。然後，最後一個命令是用來將虛擬診斷組態設定轉換為套用至 Redmond 網站的實際設定集合。請注意，最後一個命令是必要項目。如果您沒有呼叫 **Set-CsDiagnosticConfiguration** Cmdlet，則不會將設定套用至 Redmond 網站，而且只要您結束 Windows PowerShell 工作階段或刪除變數 $x，這些虛擬設定就會消失。

    $x = New-CsDiagnosticConfiguration -Identity site:Redmond -InMemory
    $x.LoggingShare = "\\atl-fs-001\logs"
    Set-CsDiagnosticConfiguration -Instance $x

## 詳細描述

如果您啟用 Lync Server 記錄功能，則這些記錄檔中預設會包含進出任何網域或 URI 的流量。這可確保記錄檔中會盡量記錄最多的資訊。

但是，這有時候會造成資訊過多。例如，當遇到特定網域的連線問題時，需要將記錄範圍限制在您網路與該網路間的流量；這樣您才能更容易識別相關記錄，進而更輕鬆地診斷並修正問題。

診斷組態設定可讓您指定要在記錄檔中記錄的網域或 URI；例如，您可以只記錄進出特定網域的流量。 Lync Server 可讓您在網站範圍內建立診斷組態設定。如此一來，您將能對某個網站 (例如 Redmond 網站) 套用與其他網站不同的設定。

請注意，您無法在全域範圍建立診斷組態設定；那是因為全域範圍已經主控這些設定。同樣地，如果指定的網站已經包含診斷組態設定，您就無法在網站範圍建立新設定集合。例如，如果您嘗試建立 Redmond 網站的新集合，而且該網站已經主控診斷組態設定，則您的命令將會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDiagnosticConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDiagnosticConfiguration"}

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
<td><p>要建立之診斷組態設定的唯一識別碼。由於只能在網站範圍建立新設定，因此您必須使用如下的語法：-Identity &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.Filter</p></td>
<td><p>如果啟用診斷篩選，將記錄其流量之網域和 URI 的集合。Filter 屬性由三種不同的項目組成：</p>
<p>Fqdn – 要包含在篩選中之網域的集合 (在技術上是 SIP 位址的主機部分)。例如，完整網域名稱 (FQDN) 可能看起來如下：fabrikam.com。或者，可使用萬用字元來代表多個網域：*.fabrikam.com。您可以在單一篩選中包含多個網域。</p>
<p>Uri – 要包含在篩選中之 URI 的集合 (Uri 是 SIP 位址的 user@host 部分)。URI 可以由下列任何模式所組成：user@fabrikam.com、user@* 或 *@fabrikam.com。您可以在單一篩選中包括多個 URI。</p>
<p>Enabled – 表示是否要啟用篩選。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。 **New-CsDiagnosticConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsDiagnosticConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings 的新執行個體。

## 請參閱

#### 其他資源

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[New-CsDiagnosticsFilter](new-csdiagnosticsfilter.md)  
[Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)


---
title: Get-CsDiagnosticConfiguration
TOCTitle: Get-CsDiagnosticConfiguration
ms:assetid: f642bdca-82bb-4c72-9558-7e5ec43565fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413034(v=OCS.15)
ms:contentKeyID: 49292835
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDiagnosticConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之診斷組態設定的資訊。診斷組態設定可用於指定是否要將進出指定網域或統一資源識別元 (URI) 的流量記錄在 Lync Server 記錄檔中。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDiagnosticConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDiagnosticConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前所使用之所有診斷組態設定的資訊。作法是呼叫不含任何參數的 **Get-CsDiagnosticConfiguration** Cmdlet。

    Get-CsDiagnosticConfiguration

## 範例 2

範例 2 會傳回已套用至 Redmond 網站 (-Identity site:Redmond) 的診斷組態設定資訊。

    Get-CsDiagnosticConfiguration -Identity site:Redmond

## 範例 3

範例 3 所示的命令會顯示 Redmond 網站的診斷組態設定內所包含之個別篩選的資訊。為達成此目的，命令會先使用 **Get-CsDiagnosticConfiguration** Cmdlet 傳回 Redmond 網站的設定。然後再將該資訊管線傳送至 **Select-Object** Cmdlet，以使用 ExpandProperty 參數「展開」Filter 屬性的值。展開 Filter 屬性可讓您存取診斷組態設定中所維護之個別篩選的屬性與屬性值。

    Get-CsDiagnosticConfiguration -Identity site:Redmond | Select-Object -ExpandProperty Filter

## 範例 4

範例 4 所示的命令會傳回在全域診斷組態設定中的篩選子集；明確地說就是 Uri 屬性包含 SIP 位址 sip:diagnostics@litwareinc.com 的篩選。為達成此目的，命令會先使用 **Get-CsDiagnosticConfiguration** Cmdlet 傳回全域診斷組態設定執行個體的所有篩選資訊。然後再將該資訊管線傳送至 **Select-Object** Cmdlet，以展開 Filter 屬性。接著將個別篩選物件管線傳送至 **Select-Object** Cmdlet，以擷取其 Uri 屬性包含 SIP 位址 sip:diagnostics@litwareinc.com 的篩選。

    Get-CsDiagnosticConfiguration -Identity global | Select-Object -ExpandProperty Filter | Where-Object {$_.Uri -contains "sip:diagnostics@litwareinc.com"}

## 範例 5

範例 5 是範例 4 所示命令的變化；但是，在範例 5 中，只有 Uri 屬性不包含 SIP 位址 sip:diagnostics@litwareinc.com，才會傳回篩選。為達成此目的，命令會呼叫 **Get-CsDiagnosticConfiguration** Cmdlet 傳回全域組態設定執行個體的所有診斷組態資訊。然後再將該資訊管線傳送至 **Select-Object** Cmdlet，以展開 Filter 屬性。接著將篩選後的物件管線傳送至 **Select-Object** Cmdlet，這會只選取 Uri 屬性不包含 SIP 位址 sip:diagnostics@litwareinc.com 的篩選。

    Get-CsDiagnosticConfiguration -Identity global | Select-Object -ExpandProperty Filter | Where-Object {$_.Uri -notcontains "sip:diagnostics@litwareinc.com"}

## 詳細描述

如果您啟用 Lync Server 記錄功能，則這些記錄檔中預設會包含進出任何網域或 URI 的流量。這可確保記錄檔中會盡量記錄最多的資訊。

但是，這有時候會造成資訊過多。例如，當遇到特定網域的連線問題時，需要將記錄範圍限制在您網路與該網路間的流量；這樣您才能更容易識別相關記錄，進而更輕鬆地診斷並修正問題。

診斷組態設定可讓您指定要記錄在記錄檔中的網域或 URI。Lync Server 可讓您在網站範圍內建立診斷組態設定。如此一來，您就可以將異於其他網站的設定套用至 Redmond 網站。

**Get-CsDiagnosticConfiguration** Cmdlet 可讓您傳回組織中目前使用之診斷組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDiagnosticConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDiagnosticConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在指定要傳回的設定集合時使用萬用字元。例如，此語法會傳回網站範圍設定的所有設定：-Filter &quot;site:*&quot;。</p>
<p>請注意，您不能在同一個命令中同時使用 Filter 和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之診斷組態設定的唯一識別碼。若要傳回在此網站範圍設定的設定，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要傳回全域設定，請使用下列語法：-Identity global。</p>
<p>若未指定此參數，則會傳回所有目前正在使用的診斷組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取診斷組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsDiagnosticConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDiagnosticConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)


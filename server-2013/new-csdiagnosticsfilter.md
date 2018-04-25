---
title: New-CsDiagnosticsFilter
TOCTitle: New-CsDiagnosticsFilter
ms:assetid: f1af92b1-4d1f-4eb3-9874-7fa6f6ae39c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413009(v=OCS.15)
ms:contentKeyID: 49292785
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDiagnosticsFilter

 

_**上次修改主題的時間：** 2015-03-09_

建立診斷組態設定所要使用的新診斷篩選。診斷組態設定可用於指定是否要將進出指定網域或統一資源識別元 (URI) 的流量記錄在 Lync Server 記錄檔中。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDiagnosticsFilter [-Enabled <$true | $false>] [-ExcludeConferenceMessages <$true | $false>] [-ExcludePresenceNotifications <$true | $false>] [-ExcludeRegisterMessages <$true | $false>] [-ExcludeSubscribeMessages <$true | $false>] [-ExcludeSuccessfulRequests <$true | $false>] [-Fqdn <PSListModifier>] [-Uri <PSListModifier>]

## 範例

## 範例 1

範例 1 所示的命令使用 **New-CsDiagnosticsFilter** Cmdlet 來建立新的診斷篩選，然後將該篩選指派給全域診斷組態設定。為了執行此工作，第一個命令會呼叫 **New-CsDiagnosticsFilter** Cmdlet 建立僅存在記憶體內的診斷篩選。此篩選會將 FQDN fabrikam.com 和 URI user@fabrikam.com 新增至篩選中。此命令也會將 Enabled 屬性設為 ($True) 以啟動篩選。所產生的虛擬篩選接著會儲存於變數 $x 中。

在第二個命令中，**Set-CsDiagnosticConfiguration** Cmdlet 可用來將新的篩選指派給全域診斷組態設定。在此案例中，任何存在於 Filter 屬性中的值都將由儲存於 $x 中的新建篩選所取代。

    $x = New-CsDiagnosticsFilter -Fqdn "fabrikam.com" -Enabled $False
    Set-CsDiagnosticConfiguration -Identity global -Filter $x 

## 範例 2

範例 2 所示的命令是範例 1 顯示的命令變化；但範例 2 會將兩個 FQDN (fabrikam.com 和 contoso.com) 加入篩選的 Fqdn 屬性。為達此目的，會將這兩個名稱 (由逗號分隔) 用為 Fqdn 參數的參數值。

    $x = New-CsDiagnosticsFilter -Fqdn "fabrikam.com","contoso.com" -Enabled $False
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## 詳細描述

如果您啟用 Lync Server 記錄功能，則這些記錄檔中預設會包含進出任何網域或 URI 的流量。這可確保記錄檔中會盡量記錄最多的資訊。

換句話說，這也會產生資訊過多的情況。例如，當遇到特定網域的連線問題時，需要將記錄範圍限制在您網路與該網路間的流量；這樣您才能更容易識別相關記錄，進而更輕鬆地診斷並修正問題。

診斷組態設定讓您可以指定記錄檔中要記錄的網域或 URI；例如，您可能只想記錄指定網域的來回流量。除了全域設定外，Lync Server 可讓您在網站範圍或服務範圍 (針對 Edge Server 或登錄器服務) 建立診斷設定。因此，除了可以將設定套用至您的其他網站外，您也可以將不同設定套用至 Redmond 網站。

**New-CsDiagnosticsFilter** Cmdlet 讓您能將篩選新增至診斷設定的集合中。此集合包含將在記錄檔中記錄其流量的網域與 URI。如果已啟用篩選，將只會記錄篩選中與網域和 URI 相關的資訊；基於記錄的目的，將略過來自其他網域和 URI 的流量。

請注意，**New-CsDiagnosticsFilter** Cmdlet 會為診斷篩選建立僅存在記憶體內的執行個體。建立其中一個虛擬篩選之後，接著將需使用 **New-CsDiagnosticConfiguration** Cmdlet 或 **Set-CsDiagnosticConfiguration** Cmdlet，將該篩選新增至集合中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDiagnosticsFilter** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDiagnosticsFilter"}

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
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否應採用篩選。預設值為 True ($True)。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeConferenceMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，關於會議訊息的資訊 (也就是，任何在其 To 或 From 標頭中含有會議 URI 的訊息) 不會記錄於記錄檔中。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludePresenceNotifications</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，關於目前狀態通知的資訊 (也就是，任何使用 NOTIFY 或 BENOTIFY 方法的訊息) 不會記錄於記錄檔中。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeRegisterMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，關於用戶端註冊的資訊 (也就是，任何使用 REGISTER 方法的訊息) 不會記錄於記錄檔中。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeSubscribeMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，關於用戶端訂閱的資訊 (也就是，任何使用 SUBSCRIBE 方法的訊息) 不會記錄於記錄檔中。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeSuccessfulRequests</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，記錄檔中將不會記錄成功的 SIP 要求的資訊，而只會儲存失敗要求的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Fqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>要包含於篩選的網域集合 (更嚴格來說，這些網域是 SIP 位址的主機部分)。針對 FQDN 屬性，您可以使用完整網域名稱 (FQDN)，例如：fabrikam.com。或者，可使用萬用字元來代表多個網域：*.fabrikam.com。您可以在單一篩選上擁有一個以上的網域。</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>要包含於篩選中的 URI 集合 (URI 是 SIP 位址的 user@host 部分)。URI 可以由下列任何模式所組成：</p>
<p>user@fabrikam.com</p>
<p>user@*</p>
<p>*@fabrikam.com</p>
<p>您可以在單一篩選中包含多個 URI。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsDiagnosticsFilter** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsDiagnosticsFilter** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.Filter 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)


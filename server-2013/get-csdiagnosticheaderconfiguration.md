---
title: Get-CsDiagnosticHeaderConfiguration
TOCTitle: Get-CsDiagnosticHeaderConfiguration
ms:assetid: a5b247b8-621a-463b-8034-f2f6970706fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412774(v=OCS.15)
ms:contentKeyID: 49291900
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDiagnosticHeaderConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之診斷標頭組態設定的資訊。診斷標頭組態設定可指定是否要在 SIP 訊息中加入標頭資訊，以供疑難排解及錯誤報告時使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDiagnosticHeaderConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDiagnosticHeaderConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

前面的命令會傳回組織目前使用的所有診斷標頭組態設定的資訊。作法是呼叫不含任何參數的 **Get-CsDiagnosticHeaderConfiguration** Cmdlet。

    Get-CsDiagnosticHeaderConfiguration

## 範例 2

範例 2 會傳回診斷標頭組態設定的單一集合 (即集合的 Identity 為 site:Redmond)。

    Get-CsDiagnosticHeaderConfiguration -Identity site:Redmond

## 範例 3

範例 3 所示的命令會傳回所有在服務範圍設定的診斷標頭設定。為達成此目的，會呼叫 **Get-CsDiagnosticHeaderConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "service:\*" 可確保只會傳回 Identity 開頭為字元 "service:" 的設定。

    Get-CsDiagnosticHeaderConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回所有允許傳送到外部網路的診斷標頭組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsDiagnosticHeaderConfiguration** Cmdlet，這會傳回目前使用的所有診斷標頭設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 SendToExternalNetworks 屬性等於 True 的設定。

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True}

## 範例 5

範例 5 所示的命令會傳回至少符合下列其中一項條件的診斷標頭組態設定資訊：1) SendToExternalNetworks 屬性等於 True；且/或 2) SendToOutsideUnauthenticatedUsers 等於 True。為達成此目的，命令會先使用 **Get-CsDiagnosticHeaderConfiguration** Cmdlet 傳回目前使用的所有診斷標頭設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 SendToExternalNetworks 屬性和/或 SendToOutsideUnauthenticatedUsers 屬性為 True 的設定。

\-or 運算子指定傳回的設定只需符合指定條件之一。若要求設定必須符合兩個指定條件，則要改用 -and 運算子：

Where-Object {$\_.SendToExternalNetworks -eq $True -and $\_.SendToOutsideUnauthenticatedUsers -eq $True}

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True -or $_.SendToOutsideUnauthenticatedUsers -eq $True}

## 詳細描述

傳送 SIP (工作階段初始通訊協定) 訊息時，您可以在每則訊息上附加 ms-diagnostics 標頭。此訊息 (一般使用者看不到) 包含有助於疑難排解連線問題或報告錯誤的資訊。例如，診斷標頭可包含啟用用戶端應用程式 (例如 Lync 2013) 的錯誤代碼，以在發生特定情況時採取預先決定動作。

若是在內部網路內傳送的 SIP 訊息，有幾個理由可以不包含這些診斷標頭：它們對訊息大小的影響最小，且對於要解決連線問題的系統管理員來說可能是沒價值的工具。但是，診斷標頭也包含了一些您可能不想讓內部網路以外人員看到的資訊，像是 SIP 伺服器的完整網域名稱 (FQDN)。因此，診斷標頭組態設定可讓您決定是否傳送診斷標頭給外部網路使用者 (例如，同盟網域的使用者) 和/或外部使用者 (外部使用者係指從內部網路之外進行連線，且尚未經過驗證的使用者)。

根據預設，標頭不會包含在傳送給外部網路或未驗證的使用者的訊息中。不過，您可以修改全域診斷標頭設定，以將標頭包含在給外部網路和/或未驗證的使用者的訊息中。或者，您可以在網站範圍或服務範圍 (針對 Edge Server 或登錄器服務) 建立自訂設定。這樣一來，您就可以選擇包含從某一個網站或經由某一個 Edge Server 傳送的訊息診斷標頭，同時不允許從其他網站或經由其他 Edge Server 傳送的訊息診斷標頭。

**Get-CsDiagnosticHeaderConfiguration** Cmdlet 提供方法，讓您擷取目前組織中使用的診斷標頭組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDiagnosticHeaderConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDiagnosticHeaderConfiguration"}

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
<td><p>可讓您在指定要傳回的設定集合時使用萬用字元。例如，此語法會傳回網站範圍設定的所有設定：-Filter &quot;site:*&quot;。此語法會傳回所有在服務範圍內所做的設定：-Filter &quot;service:*&quot;。</p>
<p>請注意，您不能在同一個命令中同時使用 Filter 和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回的診斷標頭組態設定的唯一識別碼。若要傳回在此網站範圍設定的設定，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要傳回在服務範圍設定的設定，請使用下列語法：-Identity &quot;service:EdgeServer:atl-edge-001.litwareinc.com&quot;。若要傳回全域設定，請使用下列語法：-Identity global。</p>
<p>若未指定此參數，將會傳回目前所使用的所有診斷標頭組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取診斷標頭組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsDiagnosticHeaderConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDiagnosticHeaderConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)  
[Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)  
[Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)


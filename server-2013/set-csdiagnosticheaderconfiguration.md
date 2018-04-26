---
title: Set-CsDiagnosticHeaderConfiguration
TOCTitle: Set-CsDiagnosticHeaderConfiguration
ms:assetid: e9243b84-63c7-4ee1-8568-6b4417e10b0c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399045(v=OCS.15)
ms:contentKeyID: 49292674
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDiagnosticHeaderConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改組織目前所使用的一或多個診斷標頭組態設定集合。診斷標頭組態設定可指定是否要在 SIP 訊息中加入標頭資訊，以供疑難排解及錯誤報告時使用。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDiagnosticHeaderConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDiagnosticHeaderConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-SendToExternalNetworks <$true | $false>] [-SendToOutsideUnauthenticatedUsers <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改 Identity 為 site:Redmond 的診斷標頭組態設定。在此範例中，將 SendToOutsideUnauthenticatedUsers 屬性的值設定為 True。

    Set-CsDiagnosticHeaderConfiguration -Identity site:Redmond -SendToOutsideUnauthenticatedUsers $True

## 範例 2

範例 2 所示的命令為範例 1 所示之命令的變化。但此範例會修改所使用之所有診斷標頭組態設定的 SendToOutsideUnauthenticatedUsers 屬性。為達成此目的，會先呼叫不含任何參數的 **Get-CsDiagnosticHeaderConfiguration** Cmdlet，以傳回目前使用之所有診斷標頭設定的集合。然後，此集合會管線傳送到 **Set-CsDiagnosticHeaderConfiguration** Cmdlet，以將集合中每一個項目的 SendToOutsideUnauthenticatedUsers 屬性設定為 True。

    Get-CsDiagnosticHeaderConfiguration | Set-CsDiagnosticHeaderConfiguration -SendToOutsideUnauthenticatedUsers $True

## 範例 3

在範例 3 中，再次修改 SendToOutsideUnauthenticatedUsers 屬性，但這次僅針對 SendToExternalNetworks 屬性為 True 的那些診斷標頭設定。為了執行此工作，命令會先使用 **Get-CsDiagnosticHeaderConfiguration** Cmdlet 傳回目前使用之所有診斷標頭組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 SendToExternalNetworks 屬性等於 True 的設定。接著將該篩選後的集合管線傳送到 **Set-CsDiagnosticHeaderConfiguration** Cmdlet，以將集合中每一個項目的 SendToOutsideUnauthenticatedUsers 屬性值設為 True。

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True} | Set-CsDiagnosticHeaderConfiguration -SendToOutsideUnauthenticatedUsers $True

## 詳細描述

系統管理員可以選擇在傳送到組織的每則 SIP 訊息上附加 ms-diagnostics 標頭。此訊息 (一般使用者看不到) 包含有助於疑難排解連線問題或報告錯誤的資訊。例如，診斷標頭可包含啟用用戶端應用程式 (例如 Lync Server) 的錯誤代碼，以在發生特定情況時採取預先決定動作。

若是在內部網路內傳送的 SIP 訊息，有幾個理由可以不包含這些診斷標頭：它們對訊息大小的影響最小，且對於要解決連線問題的系統管理員來說可能是沒價值的工具。但是，診斷標頭也包含了一些您可能不想讓內部網路以外人員看到的資訊，像是 SIP 伺服器的完整網域名稱 (FQDN)。因此，診斷標頭組態設定可讓您決定是否傳送診斷標頭給外部網路使用者 (例如，同盟網域的使用者) 和/或外部使用者 (外部使用者係指從內部網路之外進行連線，且尚未經過驗證的使用者)。

根據預設，標頭不會包含在傳送給外部網路或未驗證的使用者的訊息中。不過，您可以修改全域診斷標頭設定，以將標頭包含在給外部網路和/或未驗證的使用者的訊息中。或者，您可以在網站範圍或服務範圍 (針對 Edge Server 或登錄器服務) 建立自訂設定。這樣一來，您就可以選擇包含從某一個網站或經由某一個 Edge Server 傳送的訊息診斷標頭，同時不允許從其他網站或經由其他 Edge Server 傳送的訊息診斷標頭。

**Set-CsDiagnosticHeaderConfiguration** Cmdlet 提供您修改現有診斷標頭組態設定集合的方法。您可使用這個 Cmdlet，啟用 (或停用) 外部網路和/或外部使用者的診斷標頭傳輸。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDiagnosticHeaderConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDiagnosticHeaderConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之診斷標頭組態設定的唯一識別碼。若要修改在網站範圍設定的設定值，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要修改設定於服務範圍的設定，請使用類似下列的語法：-Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;。若要修改全域設定，請使用下列語法：-Identity global。</p>
<p>如果未指定此參數，則 <strong>Set-CsDiagnosticHeaderConfiguration</strong> Cmdlet 將會自動修改全域設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DiagnosticHeaderSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>SendToExternalNetworks</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，會在傳送給外部網路使用者 (例如，同盟網域的使用者) 的訊息附加診斷標頭。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>SendToOutsideUnauthenticatedUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，會在傳送給外部使用者的訊息附加診斷標頭。外部使用者係指從內部網路之外進行連線 (例如，經由 Proxy 伺服器)，且尚未經過驗證的使用者。</p>
<p>預設值為 False。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings 物件。 **Set-CsDiagnosticHeaderConfiguration** Cmdlet 接受診斷標頭設定物件的管線執行個體。

## 傳回類型

**Set-CsDiagnosticHeaderConfiguration** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsDiagnosticHeaderConfiguration](get-csdiagnosticheaderconfiguration.md)  
[New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)  
[Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)


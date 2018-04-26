---
title: Set-CsHealthMonitoringConfiguration
TOCTitle: Set-CsHealthMonitoringConfiguration
ms:assetid: 375af06c-70c8-4775-8c7b-3b3f8fd9afcc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425847(v=OCS.15)
ms:contentKeyID: 49290585
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsHealthMonitoringConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有之健康狀況監控組態設定的集合。這些設定讓系統管理員無須提供所需測試帳戶的使用者名稱與密碼，即可執行品質保證測試。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsHealthMonitoringConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsHealthMonitoringConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-FirstTestSamAccountName <String>] [-FirstTestUserSipUri <String>] [-Force <SwitchParameter>] [-SecondTestSamAccountName <String>] [-SecondTestUserSipUri <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會設定已指派給 atl-cs-001.litwareinc.com 集區之狀況監控組態設定的第一個測試使用者。在此範例中，新測試使用者的 SIP 位址會設為 sip:kenmyer@litwareinc.com，此測試使用者的 SamAccountName 會設為 kenmyer。

    Set-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -FirstTestSamAccountName "litwareinc\kenmyer"

## 範例 2

範例 2 是範例 1 所示之命令的變化，但此範例會將同一位測試使用者指派用於組織的每個運作情況監控組態設定集合。為了執行此工作，命令會先使用 **Get-CsHealthMonitoringConfiguration** Cmdlet 傳回所有運作情況監控組態設定的集合。然後，此集合會管線傳送到 **Set-CsHealthMonitoringConfiguration** Cmdlet，將相同的第一個測試使用者 SIP 位址與 SamAccountName 指派給集合中的每個項目。

    Get-CsHealthMonitoringConfiguration | Set-CsHealthMonitoringConfiguration -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -FirstTestSamAccountName "litwareinc\kenmyer"

## 範例 3

範例 3 會顯示您如何搜尋與取代指派給健全狀況組態設定集合的第一個測試使用者；在此範例中，任何時候當 SIP 位址為 sip:pilar@litwareinc.com 的使用者顯示為集合中的第一個測試使用者時，該使用者就會被取代。

為達成此目的，命令會先呼叫不含任何額外參數的 **Get-CsHealthMonitoringConfiguration** Cmdlet，以傳回目前用於組織的所有狀況監控組態設定的集合。此集合接著會被管線傳送到 **Where-Object** Cmdlet，這樣會只挑選出 FirstTestUserSipUri 屬性等於 (-eq) sip:pilar@litwareinc.com 的項目。篩選後的集合便會管線傳送到 **Set-CsHealthMonitoringConfiguration** Cmdlet，以取得集合中的每個項目，並將 FirstTestUserSipUri 屬性的值設為 sip:kenmyer@litwareinc.com，將 FirstTestSamAccountName 屬性的值設為 kenmyer。

    Get-CsHealthMonitoringConfiguration | Where-Object {$_.FirstTestUserSipUri -eq "sip:pilar@litwareinc.com"} | Set-CsHealthMonitoringConfiguration -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -FirstTestSamAccountName "litwareinc\kenmyer"

## 詳細描述

Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

有兩種不同的方式可執行綜合交易。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試帳戶。這些測試帳戶是已預先設定要搭配使用綜合交易的一對使用者帳戶。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。對集區設定測試帳戶時，系統管理員只要對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。相對的，綜合交易在執行檢查時，會自動使用預先設定的測試帳戶。

另一種方式是系統管理員會使用真正的使用者帳戶來執行綜合交易。例如，如果有兩位使用者無法交換立即訊息，則系統管理員可使用這兩個有問題的使用者帳戶來執行綜合交易 (而不是使用一對的測試帳戶)。如果您決定使用真正的使用者帳戶來執行綜合交易，您必須提供每位使用者的認證。

在您設定好運作狀況監視組態設定後，您可以隨時使用 **Set-CsHealthMonitoringConfiguration** Cmdlet 來修改這些設定。此 Cmdlet 可讓您變更設定與集區搭配使用之其中一個 (或兩個) 測試帳戶。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsHealthMonitoringConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsHealthMonitoringConfiguration"}

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
<td><p><em>FirstTestSamAccountName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>第一個測試使用者的 SamAccountName。必須使用「網域\使用者名稱」的格式輸入 FirstTestSamAccountName；例如：</p>
<p>-FirstTestSamAccountName litwareinc\kenmyer</p></td>
</tr>
<tr class="odd">
<td><p><em>FirstTestUserSipUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>第一個透過此健全狀況監視設定集合所設定使用之測試使用者 SIP 位址。請注意，SIP 位址必須包含 sip:首碼。例如：-FirstTestUserSipUri &quot;sip:kenmyer@litwareinc.com&quot;。</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>已指派要修改之狀況監控組態設定的集區完整網域名稱 (FQDN)。例如：-Identity atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>HealthMonitoringSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondTestSamAccountName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>第二個測試使用者的 SamAccountName。必須使用「網域\使用者名稱」的格式輸入 SecondTestSamAccountName；例如：</p>
<p>-SecondTestSamAccountName litwareinc\pilar</p></td>
</tr>
<tr class="even">
<td><p><em>SecondTestUserSipUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>第二個透過此健全狀況監視設定集合所設定使用之測試使用者 SIP 位址。請注意，SIP 位址必須包含 sip:首碼。例如：-FirstTestUserSipUri &quot;sip:pilar@litwareinc.com&quot;。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings 物件。**Set-CsHealthMonitoringConfiguration** Cmdlet 會接受運作狀況監控組態物件的管線傳送的執行個體。

## 傳回類型

無。反之，**Set-CsHealthMonitoringConfiguration** Cmdlet 會修改 Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings 物件的現有執行個體。

## 請參閱

#### 其他資源

[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)  
[Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)


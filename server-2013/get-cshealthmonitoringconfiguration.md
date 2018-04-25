---
title: Get-CsHealthMonitoringConfiguration
TOCTitle: Get-CsHealthMonitoringConfiguration
ms:assetid: 843876f1-8aa6-4324-a981-8eded4d3b16d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398667(v=OCS.15)
ms:contentKeyID: 49291524
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHealthMonitoringConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回您組織所使用之健康狀況監視組態設定的資訊。這些設定讓系統管理員無須提供所需測試帳戶的使用者名稱與密碼，即可執行品質保證測試。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsHealthMonitoringConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsHealthMonitoringConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回您組織目前正在使用的所有運作情況監控組態設定。

    Get-CsHealthMonitoringConfiguration

## 範例 2

範例 2 所示的命令會傳回下列狀況監控組態設定的單一集合：其 Identity 為 atl-cs-001.litwareinc.com 的設定。

    Get-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com

## 範例 3

範例 3 會傳回已針對網域 litwareinc.com 建立的所有狀況監控組態設定。為達成此目的，會呼叫 **Get-CsHealthMonitoringConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "\*.litwareinc.com" 可確保只會傳回 Identity 結尾為字串值 ".litwareinc.com" 的設定。

    Get-CsHealthMonitoringConfiguration -Filter *.litwareinc.com

## 範例 4

範例 4 所示的命令會傳回所有將具有 SIP 位址 sip:kenmyer@litwareinc.com 的使用者納入做為其中一個測試使用者的運作情況監控組態設定。為達此目的，命令會先呼叫 **Get-CsHealthMonitoringConfiguration** Cmdlet 而不加上任何參數；這會傳回組織中目前使用的所有運作情況監控組態設定集合。然後將此集合以管線傳送到 **Where-Object** Cmdlet，這會只挑出 FirstTestUserSipUri 屬性等於 "sip:kenmyer@litwareinc.com" 或 SecondTestUserSipUri 屬性等於 "sip:kenmyer@litwareinc.com" 的設定。結果會傳回第一位或第二位測試使用者使用了 Ken Myer 的 SIP 位址的任何設定集合。

    Get-CsHealthMonitoringConfiguration | Where-Object {$_.FirstTestUserSipUri -eq "sip:kenmyer@litwareinc.com" -or $_.SecondTestUserSipUri -eq " sip:kenmyer@litwareinc.com"}

## 詳細描述

Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員「手動」執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

有兩種不同的方式可執行綜合交易。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 設定每個登錄器集區或 Director 集區的測試帳戶。這些測試帳戶是已預先設定要搭配使用綜合交易的一對使用者帳戶。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。針對集區設定測試帳戶之後，系統管理員可以針對該集區執行綜合交易，而不必指定測試中涉及之使用者帳戶的身分識別 (以及提供其認證)。相對的，綜合交易在執行檢查時，會自動使用預先設定的測試帳戶。

另一種方式是系統管理員會使用真正的使用者帳戶來執行綜合交易。例如，如果有兩位使用者無法交換立即訊息，則系統管理員可使用這兩個有問題的使用者帳戶來執行綜合交易 (而不是使用一對的測試帳戶)。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每個使用者的認證。

**Get-CsHealthMonitoringConfiguration** Cmdlet 提供方法，讓您擷取目前組織中使用的狀況監控組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsHealthMonitoringConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHealthMonitoringConfiguration"}

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
<td><p>可讓您在指定要擷取的狀況監控組態設定時使用萬用字元。例如，此語法會傳回所有已設定給 litwareinc.com 網域的設定：-Filter &quot;*.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>已指派狀況監控組態設定之集區的完整網域名稱 (FQDN)。例如：-Identity atl-cs-001.litwareinc.com。</p>
<p>如果未加上此參數，則 <strong>Get-CsHealthMonitoringConfiguration</strong> Cmdlet 會傳回所有目前使用之狀況監控組態設定的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取狀況監控組態資料，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsHealthMonitoringConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsHealthMonitoringConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)  
[Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)


---
title: New-CsHealthMonitoringConfiguration
TOCTitle: New-CsHealthMonitoringConfiguration
ms:assetid: 8ed1da01-f7db-482d-b99a-777f239908e7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398718(v=OCS.15)
ms:contentKeyID: 49291632
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsHealthMonitoringConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立組織所使用之新健康狀況監視組態設定集合。這些設定讓系統管理員無須提供所需測試帳戶的使用者名稱與密碼，即可執行品質保證測試。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsHealthMonitoringConfiguration -TargetFqdn <String> <COMMON PARAMETERS>

    New-CsHealthMonitoringConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -FirstTestUserSipUri <String> -SecondTestUserSipUri <String> [-Confirm [<SwitchParameter>]] [-FirstTestSamAccountName <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SecondTestSamAccountName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立集區為 atl-cs-001.litwareinc.com 之運作狀況監視組態設定的新集合。這些新設定將會使用 sip:kenmyer@litwareinc.com 與 sip:pilar@litwareinc.com 做為預先設定的測試帳戶。

    New-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -SecondTestUserSipUri "sip:pilar@litwareinc.com"

## 範例 2

範例 2 會針對組織中的所有登錄器集區，建立狀況監控組態設定的新集合。為達此目的，範例中的第一個命令會使用 **Get-Service** Cmdlet 搭配 Registrar 參數，以傳回所有登錄器集區的集合。然後再將該集合管線傳送到 **Select-Object** Cmdle，以選取 PoolFqdn 內容 (此內容會傳回登錄器集區的 FQDN)。這些 FQDN 會儲存在名為 $x 的變數中。

第二個命令會建立 foreach 迴圈來循環每個登錄器集區 FQDN。命令會針對每個 FQDN 呼叫 **New-CsHealthMonitoringConfiguration** Cmdlet，以建立新的組態設定集合，其中儲存在 $x 中的 FQDN 會做為新集合的 Identity，也會將兩個相同的測試帳戶指派給每個集合：sip:kenmyer@litwareinc.com 和 sip:pilar@litwareinc.com。

    $x = Get-CsService -Registrar | Select-Object PoolFqdn
    foreach ($i in $x)
       {New-CsHealthMonitoringConfiguration -Identity $i.PoolFqdn -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -SecondTestUserSipUri "sip:pilar@litwareinc.com"}

## 詳細描述

Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員「手動」執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易能夠以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試帳戶。這些測試帳戶是已預先設定要搭配使用綜合交易的一對使用者帳戶。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。針對集區設定這些測試帳戶之後，系統管理員可以針對該集區執行綜合交易，而不必指定測試中涉及之使用者帳戶的身分識別 (以及提供其認證)。但是，綜合交易在執行其檢查時，會自動使用預先設定的測試帳戶。

或者，系統管理員可以使用實際的使用者帳戶執行綜合交易。例如，如果有兩個使用者無法交換立即訊息，系統管理員可以使用上述兩個使用者帳戶 (而非一組測試帳戶) 執行綜合交易。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每個使用者的認證。

**New-CsHealthMonitoringConfiguration** Cmdlet 會提供一種方式，讓您建立登錄或 Director 集區的新運作狀況監視組態設定。建立新的狀況監控組態設定集合時，您必須指定集區的完整網域名稱 (FQDN)，以及將會當做集區測試帳戶之兩個帳戶的 SIP 位址。(不過，您不需要提供那些測試帳戶的密碼)。請注意，每個集區最多都可以裝載一個單一的運作狀況監視組態設定集合。如果您嘗試建立集區 atl-cs-001.litwareinc.com 的新集合，而且已為此集區指派登錄器，則您的命令將會失敗。

執行 **New-CsHealthMonitoringConfiguration** Cmdlet 時，如果某些集區尚未指派測試使用者，則可能會收到警告；這可能包括 Director 集區和 Office Communications Server 集區。您可以略過這些警告。想要的話，您可以將隸屬於其他集區的測試使用者指派給 Director 集區；這樣做可讓您針對 Director 執行 **Test-CsRegistration** Cmdlet。但是，您不能將測試使用者指派給 Office Communications Server 集區。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsHealthMonitoringConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsHealthMonitoringConfiguration"}

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
<td><p><em>FirstTestUserSipUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>設定為由此運作狀況監視設定集合使用之第一個測試使用者的 SIP 位址。請注意，SIP 位址必須包含 sip:首碼。例如：-FirstTestUserSipUri &quot;sip:kenmyer@litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要指派之運作狀況監視組態設定之集區的 FQDN (例如：-Identity atl-cs-001.litwareinc.com)。如果指定的集區已經裝載一個運作狀況監視組態設定集合，您的命令將會失敗。</p>
<p>Identity 相當於 TargetFqdn 參數。建立新的設定集合時，您可以使用其中一個參數。如果您遺漏這兩個參數，<strong>New-CsHealthMonitoringConfiguration</strong> Cmdlet 將會提示您輸入 Identity。</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondTestUserSipUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>設定為由此運作狀況監視設定集合使用之第二個測試使用者的 SIP 位址。請注意，SIP 位址必須包含 sip:首碼。例如：-SecondTestUserSipUri &quot;sip:pilar@litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之運作狀況監視組態設定之集區的 FQDN (例如：-TargetFqdn atl-cs-001.litwareinc.com)。如果指定的集區已經裝載一個運作狀況監視組態設定集合，您的命令將會失敗。</p>
<p>TargetFqdn 相當於 Identity 參數。建立新的設定集合時，您可以使用其中一個參數。如果您遺漏這兩個參數，<strong>New-CsHealthMonitoringConfiguration</strong> Cmdlet 將會提示您輸入 Identity。</p></td>
</tr>
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
<td><p>第一個測試使用者的 SamAccountName。輸入 FirstTestSamAccountName 時，必須使用「網域\使用者名稱」的格式，例如：</p>
<p>-FirstTestSamAccountName litwareinc\kenmyer</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondTestSamAccountName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>第二個測試使用者的 SamAccountName。輸入 SecondTestSamAccountName 時，必須使用「網域\使用者名稱」的格式，例如：</p>
<p>-SecondTestSamAccountName litwareinc\pilar</p></td>
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

無。**New-CsHealthMonitoringConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsHealthMonitoringConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)


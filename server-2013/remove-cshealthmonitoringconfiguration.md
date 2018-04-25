---
title: Remove-CsHealthMonitoringConfiguration
TOCTitle: Remove-CsHealthMonitoringConfiguration
ms:assetid: 2e401908-2366-4e67-ba5b-68ba7ece166e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425794(v=OCS.15)
ms:contentKeyID: 49290463
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHealthMonitoringConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有之健康狀況監視組態設定的集合。這些設定讓系統管理員無須提供所需測試帳戶的使用者名稱與密碼，即可執行品質保證測試。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsHealthMonitoringConfiguration -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 atl-cs-001.litwareinc.com 之運作狀況監視組態設定的集合。Identity 必須是唯一的，因此這個命令最多只會刪除單一設定集合。

    Remove-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com

## 範例 2

範例 2 會刪除目前所使用的所有運作狀況監視組態設定。為達成此目的，此命令會先呼叫不含任何參數的 **Get-CsHealthMonitoringConfiguration** Cmdlet；這樣會傳回組織中所有狀況監控組態設定的集合。然後，此集合會管線傳送到 **Remove-CsHealthMonitoringConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsHealthMonitoringConfiguration | Remove-CsHealthMonitoringConfiguration 

## 範例 3

範例 3 會刪除針對 litwareinc.com 網域所建立的所有運作情況監控組態設定。為達成此目的，命令會呼叫 **Get-CsHealthMonitoringConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "\*.litwareinc.com" 可確保只會傳回 Identity 結尾為 ".litwareinc.com" 字串值的設定。然後再將篩選後的集合管線傳送到 **Remove-CsHealthMonitoringConfiguration** Cmdlet，以刪除集合中的各個項目。

    Get-CsHealthMonitoringConfiguration -Filter *.litwareinc.com  | Remove-CsHealthMonitoringConfiguration 

## 範例 4

範例 4 所示的命令會刪除所有運作狀況監視組態設定，這些設定會將其 SIP 位址為 sip:kenmyer@litwareinc.com 的使用者加入為其中一個測試使用者。為了執行此工作，此命令會先呼叫不含任何參數的 **Get-CsHealthMonitoringConfiguration** Cmdlet；這樣做會傳回組織目前所使用之所有狀況監控組態設定的集合。然後再將此集合管線傳送至 **Where-Object** Cmdlet，這會只挑出 FirstTestUserSipUri 屬性等於 "sip:kenmyer@litwareinc.com" 或 (SecondTestUserSipUri 屬性等於 "sip:kenmyer@litwareinc.com" 的設定。接著將這些設定管線傳送到 **Remove-CsHealthMonitoringConfiguration** Cmdlet 加以移除。

    (Get-CsHealthMonitoringConfiguration | Where-Object {$_.FirstTestUserSipUri -eq "sip:kenmyer@litwareinc.com" -or $_.SecondTestUserSipUri -eq " sip:kenmyer@litwareinc.com"}) | Remove-CsHealthMonitoringConfiguration

## 詳細描述

Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易能夠以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試帳戶。這些測試帳戶是已預先設定要搭配使用綜合交易的一對使用者帳戶。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。針對集區設定這些測試帳戶之後，系統管理員可以針對該集區執行綜合交易，而不必指定測試中涉及之使用者帳戶的身分識別 (以及提供其認證)。但是，綜合交易在執行其檢查時，會自動使用預先設定的測試帳戶。

或者，系統管理員可以使用實際的使用者帳戶執行綜合交易。例如，如果有兩個使用者無法交換立即訊息，系統管理員可以使用上述兩個使用者帳戶 (而非一組測試帳戶) 執行綜合交易。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每個使用者的認證。

**Remove-CsHealthMonitoringConfiguration** Cmdlet 可讓您移除設定供組織使用的所有狀況監控組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsHealthMonitoringConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientPolicy"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要刪除之主控狀況監控組態設定之集區的完整網域名稱 (FQDN)。例如：-Identity atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings 物件。**Remove-CsHealthMonitoringConfiguration** Cmdlet 接受運作狀況監視組態物件的管線傳送執行個體。

## 傳回類型

無。反之，**Remove-CsHealthMonitoringConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)


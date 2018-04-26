---
title: New-CsBandwidthPolicyServiceConfiguration
TOCTitle: New-CsBandwidthPolicyServiceConfiguration
ms:assetid: 0cb07eda-ffbe-48e2-b6bc-995737e5ba32
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398175(v=OCS.15)
ms:contentKeyID: 49290071
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsBandwidthPolicyServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的頻寬原則服務組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsBandwidthPolicyServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableLogging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-MaxLogFileSizeMb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會在 Redmond 網站 (-Identity site:Redmond) 建立新的頻寬原則服務組態。由於未指定其他參數，因此所有組態值皆會使用預設值。

    New-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

## 範例 2

在此範例中，我們再次建立新的頻寬原則服務組態，但這次是針對 Dublin 網站 (-Identity site:Dublin)。針對這個網站，我們不接受預設值，而是希望啟用記錄並將記錄檔清除前的保留天數設為 30 天。我們透過傳遞 True ($True) 值給 EnableLogging 參數，然後傳遞 30.00:00:00 值給 LogCleanupInterval 參數來完成此工作。LogCleanupInterval 值是一個 TimeSpan 物件，其格式為 dd.hh:mm:ss，其中 d 為天數、h 為小時數、m 為分鐘數、s 為秒數。

    New-CsBandwidthPolicyServiceConfiguration -Identity site:Dublin -EnableLogging $True -LogCleanupInterval 30.00:00:00

## 詳細描述

通話許可控制 (CAC) 是一種根據頻寬限制，判斷是否允許建立即時通訊工作階段 (例如語音或視訊通話) 的方式。在 Lync Server 的 CAC 實作中，地區、網站及子網路是在網路中與這些實體之間的關係和連結一起定義，以便對它們之間的頻寬加上限制。頻寬原則服務是在 Lync Server 部署中執行 CAC 功能的元件，能判斷目前是否有足夠的頻寬可建立通話。此 Cmdlet 會在網站層級設定新的頻寬原則服務。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsBandwidthPolicyServiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsBandwidthPolicyServiceConfiguration"}

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
<td><p>包含組態之範圍與名稱的唯一識別碼。此組態只能在網站範圍建立，因此 Identity 的格式如下：site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是套用組態的網站名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLogging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此參數設為 True 可產生與頻寬原則服務相關的 CAC 失敗及連結狀態記錄檔。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>LogCleanUpInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>CAC 失敗及連結狀態記錄檔的保留時間，超過此時間之後，將會移除記錄檔。</p>
<p>此值必須介於 1 天至 60 天的範圍內。此值必須以 dd.hh:mm:ss 格式輸入，其中 d 為天數、h 為小時數、m 為分鐘數、s 為秒數。</p>
<p>預設值：10 天 (10.00:00:00)</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxLogFileSizeMb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>允許記錄檔達到的大小上限。此參數的值必須是正值，用以指定檔案的大小，單位為 MB。</p>
<p>預設值：3 (MB)</p></td>
</tr>
<tr class="even">
<td><p><em>MaxTokenLifetime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>寬頻原則驗證服務發出的權杖將存在的時間長度上限。</p>
<p>此值必須介於 1 小時至 24 小時的範圍內。此值必須以 dd.hh:mm:ss 格式輸入，其中 d 為天數、h 為小時數、m 為分鐘數、s 為秒數。</p>
<p>預設值：8 小時 (08:00:00)</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsBandwidthPolicyServiceConfiguration](remove-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)


---
title: Set-CsBandwidthPolicyServiceConfiguration
TOCTitle: Set-CsBandwidthPolicyServiceConfiguration
ms:assetid: b39af1ca-465d-4598-96a3-e19283ddf731
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412863(v=OCS.15)
ms:contentKeyID: 49292056
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsBandwidthPolicyServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的頻寬原則服務組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsBandwidthPolicyServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsBandwidthPolicyServiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLogging <$true | $false>] [-Force <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-MaxLogFileSizeMb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改 Redmond 網站 (-Identity site:Redmond) 的頻寬原則服務組態。組態修改為啟用記錄、變更權杖存留期上限為三小時，以及將記錄清除前的保留天數改為五天。這些都可以在這一個命令中完成。若要啟用記錄，將 EnableLogging 參數設為 True ($true)。接下來的 MaxTokenLifetime 參數收到 3:00:00 這個值，表示三小時。最後，LogCleanUpInterval 參數收到 5.00:00:00 這個值，表示五天。

    Set-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond -EnableLogging $true -MaxTokenLifetime 3:00:00 -LogCleanUpInterval 5.00:00:00

## 詳細描述

通話許可控制 (CAC) 是一種根據頻寬限制，判斷是否允許建立即時通訊工作階段 (例如語音或視訊通話) 的方式。在 Lync Server 的 CAC 實作中，地區、網站及子網路是在網路中與這些實體之間的關係和連結一起定義，以便對它們之間的頻寬加上限制。頻寬原則服務是在 Lync Server 部署中執行 CAC 功能的元件，能判斷目前是否有足夠的頻寬可建立通話。這個 Cmdlet 會修改現有的頻寬原則服務組態。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsBandwidthPolicyServiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsBandwidthPolicyServiceConfiguration"}

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
<td><p><em>EnableLogging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此參數設為 True 會產生與頻寬原則服務相關的 CAC 錯誤和連結狀態記錄。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要變更的組態的唯一識別碼。此識別碼將由範圍 (全域組態) 或是範圍和名稱 (網站層級組態，如 site:Redmond) 所組成。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>BandwidthPolicyServiceConfiguration</p></td>
<td><p>指向頻寬原則服務組態物件的參考。此物件必須是 BandwidthPolicyServiceConfiguration 類型，呼叫 <strong>Get-CsBandwidthPolicyServiceConfiguration</strong> Cmdlet 即可擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>LogCleanUpInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>時間間隔，過了這段時間就會移除 CAC 錯誤和連結狀態記錄。</p>
<p>此值必須是整數，介於 1 天到 60 天。此值的輸入格式必須是 格式 dd.hh:mm:ss，其中 d 是天數，h 是 時數，m 是分鐘數，s 是秒數。例如，20 天表示為 20.00:00:00。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxLogFileSizeMb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>記錄檔可達的大小上限。此參數的值必須是正值，用以指定檔案的大小，單位為 MB。例如，若要讓記錄檔最大可以到 10 MB，請輸入 10 這個值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxTokenLifetime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>寬頻原則驗證服務發出的權杖將存在的時間長度上限。</p>
<p>此值必須是整數，介於 1 小時到 24 小時。此值的輸入格式必須是 格式 dd.hh:mm:ss，其中 d 是天數，h 是 時數，m 是分鐘數，s 是秒數。例如，12 小時表示為 12:00:00。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration 物件。接受頻寬原則服務組態物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Remove-CsBandwidthPolicyServiceConfiguration](remove-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)


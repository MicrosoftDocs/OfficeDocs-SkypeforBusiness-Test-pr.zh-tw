---
title: Get-CsBandwidthPolicyServiceConfiguration
TOCTitle: Get-CsBandwidthPolicyServiceConfiguration
ms:assetid: 9cb9cf59-c47e-40f6-9f9e-235b83329a69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412727(v=OCS.15)
ms:contentKeyID: 49291806
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBandwidthPolicyServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個頻寬原則服務組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsBandwidthPolicyServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsBandwidthPolicyServiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會擷取在 Lync Server 實作中定義的所有頻寬原則服務組態。

    Get-CsBandwidthPolicyServiceConfiguration

## 範例 2

此範例會擷取針對 Redmond 網站 (-Identity site:Redmond) 定義的頻寬原則服務組態。

    Get-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

## 範例 3

在此範例中，我們使用 Filter 參數來擷取在網站層級定義的所有頻寬原則服務組態。作法是將值 site:\* 傳遞到 Filter 參數。這會搜尋所有頻寬原則服務組態的 Identity 屬性，找出開頭為 site: 且緊接著任何其他字元的值。由於所有網站層級的組態都具備開頭為 site: 且緊接著網站名稱的 Identity 值，因此，此篩選將會尋找所有網站的所有組態。

    Get-CsBandwidthPolicyServiceConfiguration -Filter site:*

## 範例 4

範例 4 會擷取允許記錄檔大小大於 4 MB 的所有頻寬原則服務組態。此範例會先呼叫 **Get-CsBandwidthPolicyServiceConfiguration** Cmdlet。如同範例 1，此 Cmdlet 會擷取在 Lync Server 部署中定義之所有組態的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會一次一個項目，循環整個集合。針對集合中的每個項目，**Where-Object** Cmdlet 會檢查 MaxLogFileSizeMb 屬性的值是否大於 (-gt) 4。如果是的話，該項目會保留為集合的一部分，並且成為命令輸出的一部分。如果 MaxLogFileSizeMb 的值沒有大於 4，則會忽略該項目，且不會傳回。

    Get-CsBandwidthPolicyServiceConfiguration | Where-Object {$_.MaxLogFileSizeMb -gt 4}

## 詳細描述

通話許可控制 (CAC) 是一種根據頻寬限制，判斷是否允許建立即時通訊工作階段 (例如語音或視訊通話) 的方式。在 Lync Server 的 CAC 實作中，地區、網站及子網路是在網路中與這些實體之間的關係和連結一起定義，以便對它們之間的頻寬加上限制。頻寬原則服務是在 Lync Server 部署中執行 CAC 功能的元件，能判斷目前是否有足夠的頻寬可建立通話。**Get-CsBandwidthPolicyServiceConfiguration** Cmdlet 會擷取一或多個頻寬原則服務的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsBandwidthPolicyServiceConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBandwidthPolicyServiceConfiguration"}

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
<td><p>包含一或多個萬用字元的一個字串，用來搜尋所有頻寬原則服務組態的 Identity 屬性，以尋找 Identity 符合萬用字元模式的所有組態。例如，Filter 值 site:* 將會擷取其 Identity 值開頭字串為 site:，且結尾為任何字元集的所有組態。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之組態的唯一識別碼。此識別碼將會包含範圍 (針對全域組態) 或範圍與名稱 (針對網站層級組態，例如 site:Redmond)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取頻寬原則服務組態，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration 類型的一或多個物件。

## 請參閱

#### 其他資源

[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Remove-CsBandwidthPolicyServiceConfiguration](remove-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)


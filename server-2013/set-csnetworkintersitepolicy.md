---
title: Set-CsNetworkInterSitePolicy
TOCTitle: Set-CsNetworkInterSitePolicy
ms:assetid: 973979bc-db2c-47a6-909e-5949a927f51c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398772(v=OCS.15)
ms:contentKeyID: 49291753
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterSitePolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有通話許可控制 (CAC) 組態中，定義直接連結之網站間的頻寬限制的網站間原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterSitePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkSiteID1 <String>] [-NetworkSiteID2 <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改其 Identity 為 Reno\_Portland 的網站原則。我們使用 BWPolicyProfileID 參數，將與此網站原則相關聯的頻寬原則設定檔變更為 HighBWLimits。

    Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

## 詳細描述

當網站共用直接連結時，您可以定義這兩個網站之間音訊與視訊連線的頻寬限制。此 Cmdlet 會修改對兩個直接連接的網站套用頻寬限制原則的網站間原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkInterSitePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterSitePolicy"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>頻寬原則設定檔的 Identity，此頻寬原則設定檔將定義此網站原則的限制。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 擷取可用的設定檔清單。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>您要修改之網站原則的唯一識別碼。由於網站原則只在全域範圍建立，因此這個識別碼不需要指定範圍，而是包含一個字串，代表該網站原則的唯一識別名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>InterNetworkSitePolicyType</p></td>
<td><p>已在記憶體中修改之網站原則的物件參考。此物件必須屬於 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 類型，而且可以藉由呼叫 <strong>Get-CsNetworkInterSitePolicy</strong> Cmdlet 來擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>與此原則相關聯之兩個網站其中一個的 Identity (NetworkSiteID)。NetworkSiteID1 與 NetworkSiteID2 的組合必須是唯一的 (例如，您無法定義兩個連接 Reno 和 Portland 的網站原則)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>與此原則相關聯之兩個網站其中一個的 Identity (NetworkSiteID)。NetworkSiteID1 與 NetworkSiteID2 的組合必須是唯一的 (例如，您無法定義兩個連接 Reno 和 Portland 的網站原則)。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 物件。接受網站間原則物件管線傳送的輸入。

## 傳回類型

這個 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)


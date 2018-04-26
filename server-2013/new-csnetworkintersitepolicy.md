---
title: New-CsNetworkInterSitePolicy
TOCTitle: New-CsNetworkInterSitePolicy
ms:assetid: e127153f-a1c3-4a31-8dd3-f08d45eca800
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398994(v=OCS.15)
ms:contentKeyID: 49292583
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkInterSitePolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的網站間原則，以定義通話許可控制 (CAC) 組態中，直接連結之網站間的頻寬限制。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkInterSitePolicy -InterNetworkSitePolicyID <String> <COMMON PARAMETERS>

    New-CsNetworkInterSitePolicy -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkSiteID1 <String> -NetworkSiteID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會建立一個新網站間原則，其會限制連線網站 Reno 與 Portland 之間的頻寬。根據頻寬原則設定檔 LowBWLimits 的設定，這些網站間的音訊與視訊連線的頻寬限制是有限的。

    New-CsNetworkInterSitePolicy -Identity Reno_Portland -NetworkSiteID1 Reno -NetworkSiteID2 Portland -BWPolicyProfileID LowBWLimits

## 詳細描述

當網站共用直接連結時，您可以定義這兩個網站之間音訊與視訊連線的頻寬限制。此 Cmdlet 可建立使頻寬限制原則和兩個直接連線之網站相關聯的網站原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkInterSitePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkInterSitePolicy"}

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
<td><p>新建立網站間原則的唯一識別碼。由於網站間原則只在全域範圍建立，因此這個識別碼不需要指定範圍，而是包含一個字串，代表該網站原則的唯一識別名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicyID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>這個值與 Identity 相同。您無法指定 Identity 與 InterNetworkSitePolicyID 兩者；輸入至其中一個的值將會自動用於兩者。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此原則相關聯之兩個網站其中一個的 Identity (NetworkSiteID)。NetworkSiteID1 與 NetworkSiteID2 的組合必須是唯一的 (例如，您無法定義兩個連接 Reno 和 Portland 的網站原則)。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此原則相關聯之兩個網站其中一個的 Identity (NetworkSiteID)。NetworkSiteID1 與 NetworkSiteID2 的組合必須是唯一的 (例如，您無法定義兩個連接 Reno 和 Portland 的網站原則)。</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>頻寬原則設定檔的 Identity，此頻寬原則設定檔將定義此網站原則的限制。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 擷取可用的設定檔清單。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)


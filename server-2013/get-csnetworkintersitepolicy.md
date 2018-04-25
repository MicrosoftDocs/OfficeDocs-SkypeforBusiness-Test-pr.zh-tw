---
title: Get-CsNetworkInterSitePolicy
TOCTitle: Get-CsNetworkInterSitePolicy
ms:assetid: a4a64048-f8d7-483a-9565-0c6f3b0937b7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412769(v=OCS.15)
ms:contentKeyID: 49291880
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterSitePolicy

 

_**上次修改主題的時間：** 2015-03-09_

擷取通話許可控制 (CAC) 組態中，一或多項定義直接連結之網站間的頻寬限制的網站間原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterSitePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

呼叫不含任何參數的 **Get-CsNetworkInterSitePolicy** Cmdlet，以擷取在兩個直接連線的網站之間定義的所有網站原則。

    Get-CsNetworkInterSitePolicy

## 範例 2

此範例會擷取 Identity 為 Reno\_Portland 的網站原則。

    Get-CsNetworkInterSitePolicy -Identity Reno_Portland

## 範例 3

範例 3 會擷取在 Identity 值中出現 Reno 字串的所有網站原則。傳遞給 Filter 參數的值中帶有萬用字元(\*)，表示「任何字元或字元組」。換句話說，字串 \*Reno\* 將尋找的 Identity 值，是以任何字元或字元組開頭，之後跟著字串 Reno，之後再跟著任何字元或字元組。

    Get-CsNetworkInterSitePolicy -Filter *Reno*

## 範例 4

此範例會擷取所有未指派頻寬原則設定檔的網站原則。命令首先會呼叫 **Get-CsNetworkInterSitePolicy** Cmdlet (如範例 1 所示)，以擷取所有網站原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會將集合範圍縮小到只包含未指派頻寬原則設定檔的網站原則。作法是比較查看每個網站原則的 BWPolicyProfileID 屬性是否等於 (-eq) Null ($null)。

    Get-CsNetworkInterSitePolicy | Where-Object {$_.BWPolicyProfileID -eq $null}

## 詳細描述

當網站共用直接連結時，您可以定義這兩個網站之間音訊與視訊連線的頻寬限制。此 Cmdlet 會擷取一或多個網站原則，這些原則建立了頻寬限制設定和直接連線網站之間的關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkInterSitePolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterSitePolicy"}

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
<td><p>包含萬用字元的字串，只會搜尋 Identity 值與萬用字元字串相符的原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之網站原則的唯一識別碼。由於網站原則只在全域範圍建立，因此這個識別碼不需要指定範圍，而是包含一個字串，代表該原則的唯一識別名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取網站間原則資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)


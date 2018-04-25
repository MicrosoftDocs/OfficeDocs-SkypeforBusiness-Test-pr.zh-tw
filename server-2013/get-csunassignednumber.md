---
title: Get-CsUnassignedNumber
TOCTitle: Get-CsUnassignedNumber
ms:assetid: a8e5cfc1-e7a0-4917-9cd9-f541fedb3a61
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412792(v=OCS.15)
ms:contentKeyID: 49291938
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUnassignedNumber

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個未指派的號碼範圍，以及套用到這些號碼的路由規則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsUnassignedNumber [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回所有已設定用於您組織的未指派號碼的集合。

    Get-CsUnassignedNumber

## 範例 2

在範例 2 中，Identity 參數用來將擷取的資料限制為 Identity 為 UNSet1 的未指派號碼。由於識別身分必須是唯一的，這個命令只會傳回指定的未指派號碼範圍。

    Get-CsUnassignedNumber -Identity UNSet1

## 範例 3

此範例使用 Filter 參數傳回 Identity 包含字串 Redmond 的所有未指派號碼的集合。例如，此命令傳回的未指派號碼設定，其 Identity 可以是 Redmond Numbers、Unassigned Redmond Numbers、UNRedmond 等等。

    Get-CsUnassignedNumber -Filter *Redmond*

## 範例 4

在範例 4 中，使用 **Get-CsUnassignedNumber**Cmdlet 和 **Where-Object**Cmdlet 擷取的集合，是所有在 Announcement 的名稱中包含 Welcome 之未指派號碼設定的集合。為達成此目的，命令會先使用 **Get-CsUnassignedNumber**Cmdlet 擷取所有未指派的號碼設定。接著將該集合管線傳送到 **Where-Object** Cmdlet，由其套用篩選，以便將傳回的資料限制為在指派的宣告名稱中包含 Welcome 的未指派號碼。

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"}

## 詳細描述

未指派號碼是指已指派給組織，但尚未指派給特定使用者或電話的電話號碼。您可設定 Lync Server 在有人撥打未指派號碼時，會將撥打的電話路由到適當目的地。此 Cmdlet 會擷取定義該路由的一或多個未指派號碼的範圍。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUnassignedNumber** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmin。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUnassignedNumber"}

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
<td><p>執行萬用字元搜尋，讓您可以將結果縮減為只有 Identity 符合指定萬用字元字串的未指派號碼範圍。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要擷取之未指派號碼範圍的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取未指派的號碼資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 類型的物件。

## 請參閱

#### 其他資源

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)


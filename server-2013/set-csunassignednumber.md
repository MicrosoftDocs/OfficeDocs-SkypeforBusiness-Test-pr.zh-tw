---
title: Set-CsUnassignedNumber
TOCTitle: Set-CsUnassignedNumber
ms:assetid: e7f52423-58d1-410a-9071-731bde45d3d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399033(v=OCS.15)
ms:contentKeyID: 49292658
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUnassignedNumber

 

_**上次修改主題的時間：** 2015-03-09_

修改現有未指派號碼的範圍，以及套用到這些號碼的路由規則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改名稱為 UNSet1 的未指派號碼範圍。我們首先將值 UNSet1 (我們想要修改的未指派號碼範圍的名稱) 傳遞給 Identity 參數。接著我們會使用 NumberRangeStart (+14255551000) 和 NumberRangeEnd (+14255551900) 參數，修改指定宣告或自動語音應答適用的未指派號碼範圍。

    Set-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## 範例 2

此範例會修改所有未指派號碼範圍設定的宣告，其為名稱中目前含有字串 "Welcome" 的宣告。我們會先呼叫 **Get-CsUnassignedNumber** Cmdlet，以擷取所有未指派號碼設定。然後將該設定集合管線傳送到 **Where-Object** Cmdlet，以將集合範圍縮小為只有 AnnouncementName 屬性包含 (-match) 字串 Welcome 的設定。有了這些設定之後，會將它們管線傳送到 **Set-CsUnassignedNumber** Cmdlet，以使用 AnnouncementService 參數來修改宣告服務 (ApplicationServer:redmond.litwareinc.com) 的應用程式伺服器識別碼，並使用 AnnouncementName 參數來修改新宣告的名稱 (Help Desk Announcement)。請注意，即使新宣告的名稱不同但服務識別碼相同，您仍然必須以該名稱指定服務識別碼。

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Set-CsUnassignedNumber -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Help Desk Announcement"

## 詳細描述

未指派號碼是指已指派給組織，但尚未指派給特定使用者或電話的電話號碼。您可設定 Lync Server 在有人撥打未指派號碼時，會將撥打的電話路由到適當目的地。這個 Cmdlet 會修改定義該路由的設定。

為了要修改此 Cmdlet 的某些設定，您的系統必須已經定義「宣告」或已經設定 Exchange UM 自動語音應答。若要判斷是否已有宣告，請呼叫 **Get-CsAnnouncement** Cmdlet。若要建立新的宣告，請呼叫 **New-CsAnnouncement** Cmdlet。若要檢查 Exchange UM 自動語音應答設定，請執行 **Get-CsExUmContact** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUnassignedNumber** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要用來處理打給此號碼範圍內之電話的宣告名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>宣告伺服器的完整網域名稱 (FQDN) 或服務識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要轉接打給此範圍內之電話的 Exchange UM 自動語音應答電話號碼。若要對此參數指派值，必須已設定 Exchange UM 自動語音應答連絡人</p></td>
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
<td><p>要修改之未指派號碼範圍的唯一名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayAnnouncementVacantNumberRange</p></td>
<td><p>包含未指派號碼設定之物件的參考。這個物件必須是 Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 類型，呼叫 <strong>Get-CsUnassignedNumber</strong> 即可擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>未指派號碼範圍中的最後一個號碼。必須大於或等於指定給 NumberRangeStart 的號碼。若要指定只有一個號碼的範圍，請在 NumberRangeStart 和 NumberRangeEnd 指定相同的號碼。</p>
<p>此號碼必須符合規則運算式 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?。這表示號碼的開頭可以是字串 tel: (如果您未指定該字串，則會自動新增該字串)、一個加號 (+)，以及數字 1 到 9。電話號碼最多可達 17 位，且後面可以再加分機，格式為 ;ext= 分機號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>未指派號碼範圍中的第一個號碼。必須小於或等於指定給 NumberRangeEnd 的值。</p>
<p>此號碼必須符合規則運算式 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?。這表示號碼的開頭可以是字串 tel: (如果您未指定該字串，則會自動新增該字串)、一個加號 (+)，以及數字 1 到 9。電話號碼最多可達 17 位，且後面可以再加分機，格式為 ;ext= 分機號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>未指派號碼的範圍有可能會重疊。如果有個號碼在多個範圍內，則優先順序最高的範圍會生效。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 物件。接受未指派號碼物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 類型的物件。

## 請參閱

#### 其他資源

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)


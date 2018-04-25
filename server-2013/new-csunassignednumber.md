---
title: New-CsUnassignedNumber
TOCTitle: New-CsUnassignedNumber
ms:assetid: 81b5d355-56d4-4325-8518-653de8e1fab4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398651(v=OCS.15)
ms:contentKeyID: 49291494
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUnassignedNumber

 

_**上次修改主題的時間：** 2015-03-09_

建立新的未指派號碼範圍，以及套用到這些號碼的路由規則。執行此 Cmdlet 會新增項目到未指派號碼的路由規則表格。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> -Identity <XdsGlobalRelativeIdentity> -NumberRangeEnd <String> -NumberRangeStart <String> <COMMON PARAMETERS>

    New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> -Identity <XdsGlobalRelativeIdentity> -NumberRangeEnd <String> -NumberRangeStart <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會建立名為 UNSet1 的未指派號碼範圍。我們會使用 NumberRangeStart (+14255551000) 和 NumberRangeEnd (+14255551100) 參數，定義指定宣告所適用的未指派號碼範圍。最後，我們會指定宣告，方法是先以宣告服務的服務識別碼指定 AnnouncementService 參數，然後將值 "Welcome Announcement" 傳給參數 AnnouncementName。請記住，系統中必須已經存在具有該名稱的「宣告」。

    New-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100" -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Welcome Announcement"

## 範例 2

此範例會建立名為 UNSet2 的未指派號碼範圍。如同在範例 1 中，我們會使用 NumberRangeStart (+14255552100) 和 NumberRangeEnd (+14255552200) 參數來定義指定宣告所適用的未指定號碼範圍。但在此範例中，此號碼範圍將會使用 Exchange UM 自動語音應答而非宣告服務。(自動語音應答是指定做為組織代表號的單一號碼；自動語音應答會透過語音提示協助使用者與適當的人員通話)。我們會將電話號碼傳給 ExUmAutoAttendantPhoneNumber 參數，以完成此命令。請注意，必須已設定 Exchange UM，而且此號碼必須是 Active Directory 網域服務 中現有的連絡人物件電話號碼。連絡人必須為自動語音應答連絡人 (連絡人的 AutoAttendant 屬性必須為 True)。

    New-CsUnassignedNumber -Identity UNSet2 -NumberRangeStart "+14255552100" -NumberRangeEnd "+14255552200" -ExUmAutoAttendantPhoneNumber "+12065551234"

## 範例 3

範例 3 與範例 2 幾乎完全相同：其會建立名為 UNSet2 的未指派號碼範圍。此範例的差別是我們新增了 Priority 參數 (在此範例中其值為 2)。這表示如果定義了另一個與此未指派號碼範圍重疊的未指派號碼範圍，且該未指派號碼範圍具有較高的優先順序 (較低的優先順序號碼，例如 1)，則會根據該範圍 (而非此範圍) 的設定來轉接電話。

    New-CsUnassignedNumber -Identity UNSet2 -NumberRangeStart "+14255552100" -NumberRangeEnd "+14255552200" -ExUmAutoAttendantPhoneNumber "+12065551234" -Priority 2

## 詳細描述

未指派的號碼是指已指派給組織，但尚未指派給特定使用者或電話的電話號碼。您可設定 Lync Server 在有人撥打未指派號碼時，會將撥打的電話路由到適當目的地。此 Cmdlet 會建立定義該路由的設定。

在執行此 Cmdlet 之前，您的系統必須已定義宣告或已設定 Exchange 整合通訊 (UM) 自動語音應答。若要判斷是否已有宣告，請呼叫 **Get-CsAnnouncement** Cmdlet。若要建立新的宣告，請呼叫 **New-CsAnnouncement** Cmdlet。若要檢查 Exchange UM 自動語音應答設定，請執行 **Get-CsExUmContact** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsUnassignedNumber** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUnassignedNumber"}

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
<td><p>System.String</p></td>
<td><p>要用來處理打給此號碼範圍內之電話的宣告名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>宣告服務的完整網域名稱 (FQDN) 或服務識別碼。只有在您未指定 ExUmAutoAttendantPhoneNumber 參數的值時，才需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要轉接打給此範圍內之電話的 Exchange UM 自動語音應答電話號碼。只有在您未使用「宣告服務」(也就是說您未提供 AnnouncementService 或 AnnouncementName 參數值) 時，才需要此欄位。若要對此參數指派值，必須已設定 Exchange UM 自動語音應答連絡人</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要建立之未指派號碼範圍的唯一名稱。所有未指派的號碼皆具有全域範圍，因此此處指定的名稱在整個 Lync Server 部署中必須是唯一。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>未指派號碼範圍中的最後一個號碼。必須大於或等於指定給 NumberRangeStart 的號碼。若要指定只有一個號碼的範圍，請在 NumberRangeStart 和 NumberRangeEnd 指定相同的號碼。</p>
<p>此號碼必須符合規則運算式 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?。這表示號碼的開頭可以是字串 tel: (如果您未指定該字串，則會自動新增該字串)、一個加號 (+)，以及數字 1 到 9。電話號碼最多可達 17 位，且後面可以再加分機，格式為 ;ext= 分機號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>未指派號碼範圍中的第一個號碼。必須小於或等於指定給 NumberRangeEnd 的值。</p>
<p>此號碼必須符合規則運算式 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?。這表示號碼的開頭可以是字串 tel: (如果您未指定該字串，則會自動新增該字串)、一個加號 (+)，以及數字 1 到 9。電話號碼最多可達 17 位，且後面可以再加分機，格式為 ;ext= 分機號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>未指派號碼的範圍有可能會重疊。如果有個號碼在多個範圍內，則優先順序最高的範圍會生效。</p></td>
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

建立 Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)


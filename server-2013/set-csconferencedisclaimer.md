---
title: Set-CsConferenceDisclaimer
TOCTitle: Set-CsConferenceDisclaimer
ms:assetid: 97afce6d-b031-466d-a170-3ca50d6df245
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398776(v=OCS.15)
ms:contentKeyID: 49291765
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceDisclaimer

 

_**上次修改主題的時間：** 2015-03-09_

修改組織所使用之會議免責聲明的屬性值。會議免責聲明是一則訊息，會顯示給使用超連結加入會議之使用者 (例如將會議連結貼入 Windows Internet Explorer 等瀏覽器的使用者) 參閱。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferenceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Header <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會同時修改您組織中會議免責聲明的 Header 和 Body 屬性。因為您只能有一個這類的免責聲明，所以不需要在執行 **Set-CsConferenceDisclaimer** Cmdlet 時指定 Identity。

    Set-CsConferenceDisclaimer -Header "Litwareinc.com Online Conference" -Body "Important note: Conferencing proceedings are recorded and archived."

## 詳細描述

當這些人員參加 Lync Server 託管的會議時，系統管理員可以在設定會議設定時，包含要對參與者顯示的法律免責聲明。此免責聲明通常用來說明有關會議的法律和智慧財產權法。使用者必須同意免責聲明中提到的規定才能參加會議。但是，請注意，這項免責聲明只會顯示給使用超連結加入會議的使用者。

Lync Server 允許單一全域執行個體的會議免責聲明。**Set-CsConferenceDisclaimer** Cmdlet 可讓您修改組織使用之會議免責聲明的屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsConferenceDisclaimer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>會議免責聲明的內容。</p></td>
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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Header</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定給會議免責聲明的標題。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>會議免責聲明的唯一識別。因為您只能有單一、全域的會議免責聲明執行個體，所以不需要在呼叫 <strong>Set-CsConferenceDisclaimer</strong> Cmdlet 時指定 Identity。然而，您可以使用下列語法參考全域的免責聲明：-Identity global。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ConferenceDisclaimer 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer 物件。**Set-CsConferenceDisclaimer** Cmdlet 接受管線傳送的會議免責聲明物件輸入。

## 傳回類型

**Set-CsConferenceDisclaimer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)


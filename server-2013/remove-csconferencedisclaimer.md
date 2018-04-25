---
title: Remove-CsConferenceDisclaimer
TOCTitle: Remove-CsConferenceDisclaimer
ms:assetid: 196252a1-2526-4944-9064-01d1846f3266
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398243(v=OCS.15)
ms:contentKeyID: 49290232
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDisclaimer

 

_**上次修改主題的時間：** 2015-03-09_

清除組織所使用之會議免責聲明標頭和本文中的文字。會議免責聲明是一則訊息，會顯示給使用超連結加入會議之使用者 (例如將會議連結貼入 Windows Internet Explorer 等瀏覽器的使用者) 參閱。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsConferenceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會重設全域免責聲明的屬性值。這表示免責聲明的「標頭」和「本文」都會設為 Null 值，給予您空白的免責聲明。

    Remove-CsConferenceDisclaimer -Identity global

## 詳細描述

當這些人員參加 Lync Server 主控的會議時，系統管理員可以在設定會議設定時，包含要對參與者顯示的法律免責聲明。此免責聲明通常用來說明有關會議的法律和智慧財產權法。使用者必須同意免責聲明中提到的規定才能參加會議。請注意，此免責聲明只會顯示給使用超連結加入會議的使用者參閱。

Lync Server 允許單一全域執行個體的會議免責聲明。**Remove-CsConferenceDisclaimer** Cmdlet 可讓您重設會議免責聲明：執行此 Cmdlet 時，免責聲明標頭和免責聲明本文都會設為 Null 值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsConferenceDisclaimer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDisclaimer"}

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
<td><p>要移除之會議免責聲明的唯一識別。雖然您只能擁有一個會議免責聲明的全域執行個體，但是在呼叫 <strong>Remove-CsConferenceDisclaimer</strong> Cmdlet 時仍需使用 Identity 參數。</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer 物件。**Remove-CsConferenceDisclaimer** Cmdlet 接受會議免責聲明物件管線傳送的輸入。

## 傳回類型

無。反之，**Remove-CsConferenceDisclaimer** Cmdlet 會將現有的 Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer 物件執行個體重設為其預設屬性值。

## 請參閱

#### 其他資源

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)


---
title: Get-CsConferenceDisclaimer
TOCTitle: Get-CsConferenceDisclaimer
ms:assetid: 2382aaef-9c5e-43f8-99de-6c880134db7d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425714(v=OCS.15)
ms:contentKeyID: 49290348
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDisclaimer

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之會議免責聲明的資訊。會議免責聲明是一則訊息，會顯示給使用超連結加入會議之使用者 (例如將會議連結貼入 Windows Internet Explorer 等瀏覽器的使用者) 參閱。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用的會議免責聲明資訊。因為只能有一個免責聲明 (在全域範圍上設定)，所以在執行此命令時無須指定 Identity。

    Get-CSConferenceDisclaimer

## 詳細描述

當這些人員參加 Lync Server 主控的會議時，系統管理員可以在設定會議設定時，包含要對參與者顯示的法律免責聲明。此免責聲明通常是用來說明和會議相關的法律和智慧財產權法規，使用者必須同意免責聲明中提到的規定才能參加會議。請注意，此免責聲明只會顯示給使用超連結加入會議的使用者參閱。

**Get-CsConferenceDisclaimer** Cmdlet 可讓您檢視組織的免責聲明內文和標頭。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsConferenceDisclaimer** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDisclaimer"}

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
<td><p>讓您可以在參考會議免責聲明時，使用萬用字元值。因為會議免責聲明只能有單一的全域執行個體，所以不必使用 Filter 參數。然而，您可以使用下列語法參考全域免責聲明：-Filter &quot;g*&quot;。此語法傳回具有以字母 &quot;g&quot; 為開頭的所有會議免責聲明。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>會議免責聲明的唯一識別。因為會議免責聲明只能有單一的全域執行個體，所以呼叫 <strong>Get-CsConferenceDisclaimer</strong> Cmdlet 時不必指定 Identity。然而，您可以使用下列語法參考全域免責聲明：-Identity global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取會議免責聲明資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsConferenceDisclaimer** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)


---
title: Remove-CsConferencingPolicy
TOCTitle: Remove-CsConferencingPolicy
ms:assetid: 8fe81ace-d167-414b-9455-8be7ddc0cab5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398728(v=OCS.15)
ms:contentKeyID: 49291648
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的會議原則。會議原則可指定會議所能使用的功能，包括會議是否可以加入 IP 音訊和視訊，乃至於會議出席人數的上限等等。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsConferencingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中， **Remove-CsConferencingPolicy** Cmdlet 用來刪除 Identity 為 SalesConferencingPolicy 的會議原則。

    Remove-CsConferencingPolicy -Identity SalesConferencingPolicy

## 範例 2

範例 2 會刪除網站範圍所設定的所有會議原則。為了完成此工作，命令會先使用 **Get-CsConferencingPolicy** Cmdlet 並搭配 Filter 參數，以傳回所有網站層級原則的集合；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為 "site" 字串值的原則。然後再將篩選後的集合管線傳送到 **Remove-CsConferencingPolicy** Cmdlet，以刪除集合中的每個項目。

    Get-CsConferencingPolicy -Filter "site:*" | Remove-CsConferencingPolicy

## 範例 3

範例 3 會刪除允許會議大小上限 (MaxMeetingSize) 超過 100 人的所有原則。為達成此目的，命令會先使用 **Get-CsConferencingPolicy** Cmdlet，以擷取設定供組織使用之所有會議原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選，以將傳回的資料限制在 MaxMeetingSize 值大於 100 的原則。最後將篩選後的集合傳遞到 **Remove-CsConferencingPolicy** Cmdlet，以刪除篩選後之集合中的所有原則。

    Get-CsConferencingPolicy | Where-Object {$_.MaxMeetingSize -gt 100} | Remove-CsConferencingPolicy 

## 詳細描述

會議是 Lync Server 中十分重要的部分，其讓使用者群組可以共同在線上檢視投影片和視訊、共用應用程式、交換檔案，甚至進行通訊及共同作業。

對於系統管理員來說，最重要的是保有對於會議與會議設定的控制權。在某些情況下，可能會有安全性顧慮：預設任何人 (包括未驗證的使用者) 都可以參與會議，並儲存會議期間散佈的任何投影片或講義。在某些情況下，可能會有頻寬顧慮：有許多同時進行的會議，每個會議都包含數百位參與者且都會使用視訊播放和檔案共用，而這可能會在您的網路上造成大混亂。此外，可能還會有法律考量。例如，會議參與者預設可以在共用內容上加上註解；不過封存會議時並不會儲存這些註解。如果您的組織需要保留所有電子通訊的記錄，您可能會想要停用註解。

當然，需要管理會議設定是一回事，實際管理這些設定又是另一回事。在 Lync Server 中，會議是使用會議原則來管理 (在此軟體的舊版中，這些稱為會議原則)。但如上述，會議原則會判斷可在會議中使用的特性與功能；範圍從會議是否可包含 IP 音訊和視訊，到可出席會議的人數上限都涵蓋在內。會議原則可在全域範圍、網站範圍或個別使用者範圍設定。這可為系統管理員在決定哪些使用者可以使用哪些功能時提供了很大的彈性。

您可以使用 **Remove-CsConferencingPolicy** Cmdlet 刪除設定供組織使用的任何會議原則，但有一個例外：您無法刪除全域原則。不過，您仍然可以針對全域原則執行 **Remove-CsConferencingPolicy** Cmdlet。但在該情況下，並不會移除原則；而是將所有全域原則屬性重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsConferencingPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingPolicy"}

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
<td><p>要移除之會議原則的唯一識別碼。會議原則可以在全域、網站或個別使用者範圍設定。若要移除全域原則，請使用下列語法：-Identity global (請注意，實際上無法移除全域原則，而是將所有原則屬性重設為其預設值)。若要移除網站原則，請使用類似下列的語法：-Identity site:Redmond。若要移除個別使用者原則，請使用類似下列的語法：-Identity SalesConferencingPolicy。</p>
<p>指定 Identity 時不允許使用萬元字元。</p></td>
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
<td><p>如果使用此參數，會使 <strong>Remove-CsConferencingPolicy</strong> Cmdlet 刪除個別使用者原則，即使上述原則目前已指派給至少一位使用者也一樣。如果未使用此參數，系統會要求您確認刪除要求，之後才移除原則。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy 物件。**Remove-CsConferencingPolicy** Cmdlet 接受管線傳送的會議原則物件執行個體。

## 傳回類型

**Remove-CsConferencingPolicy** Cmdlet 不會傳回值或物件，而會刪除 Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)


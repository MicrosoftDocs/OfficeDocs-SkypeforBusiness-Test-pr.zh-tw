---
title: Get-CsConferencingPolicy
TOCTitle: Get-CsConferencingPolicy
ms:assetid: 21dc4774-2306-4425-a561-71e0b293f8df
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398293(v=OCS.15)
ms:contentKeyID: 49290328
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回已設定供組織使用之會議原則的資訊。會議原則可決定會議所能使用的功能，包括會議是否可以加入 IP 音訊和視訊，乃至於會議出席人數的上限等等。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsConferencingPolicy [-Identity <XdsIdentity>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    Get-CsConferencingPolicy [-Filter <String>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

第一個範例會傳回設定供組織使用之所有會議原則的集合。

    Get-CsConferencingPolicy

## 範例 2

在範例 2 中，Identity 參數用於將擷取的資訊限制為其 Identity 等於 Global 的會議原則。原則 Identity 必須是唯一的，這個命令才會傳回單一原則：全域會議原則。

    Get-CsConferencingPolicy -Identity Global

## 範例 3

範例 3 會使用 Filter 參數來傳回已經在個別使用者範圍設定之所有會議原則的集合。"tag:\*" 萬用字元值會告知 Windows PowerShell 將傳回的資料限制為 Identity 開頭為 “tag:” 字串值的會議原則。

    Get-CsConferencingPolicy -Filter tag:*

## 範例 4

範例 4 會傳回其 MaxMeetingSize 屬性大於 100 之所有會議原則的集合。此命令會先使用 **Get-CsConferencingPolicy** Cmdlet 傳回設定供組織使用之所有會議原則的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet 套用篩選，將傳回的資料限制在 MaxMeetingSize 屬性大於 100 的原則。

    Get-CsConferencingPolicy | Where-Object {$_.MaxMeetingSize -gt 100}

## 範例 5

範例 5 會傳回符合以下兩個條件的所有會議原則：AllowExternalUsersToSaveContent 屬性等於 True，而且 AllowExternalUserControl 屬性也等於 True。為達成此目的，命令會呼叫不含任何參數的 **Get-CsConferencingPolicy** Cmdlet，傳回設定供組織使用之所有會議原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 AllowExternalUsersToSaveContent 和 AllowExternalUserControl 均為 True 的原則。-and 運算子會指示 **Where-Object** Cmdlet 只能傳回符合所有指定條件的物件。

    Get-CsConferencingPolicy | Where-Object {$_.AllowExternalUsersToSaveContent -eq $True -and $_.AllowExternalUserControl -eq $True}

## 範例 6

範例 6 是範例 5 所示命令的變異命令。在此範例中，命令會傳回至少符合以下其中一個 (但未必兩個都符合) 指定條件的所有原則：AllowExternalUsersToSaveContent 屬性等於True，及/或 AllowExternalUserControl 屬性等於 True。為達成此目的，命令會呼叫不加任何參數的 **Get-CsConferencingPolicy** Cmdlet；此會傳回設定供組織使用之所有會議原則的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，這僅會挑出 AllowExternalUsersToSaveContent 及/或 AllowExternalUserControl 等於 True 的原則。-or operator 運算子會指示 **Where-Object** Cmdlet 傳回只符合一個指定條件的物件。

    Get-CsConferencingPolicy | Where-Object {$_.AllowExternalUsersToSaveContent -eq $True -or $_.AllowExternalUserControl -eq $True}

## 詳細描述

會議是 Lync Server 中十分重要的部分，其讓使用者群組可以共同在線上檢視投影片和視訊、共用應用程式、交換檔案，甚至進行通訊及共同作業。

對於系統管理員來說，最重要的是保有對於會議與會議設定的控制權。在某些情況下，可能會有安全性顧慮：預設任何人 (包括未驗證的使用者) 都可以參與會議，並儲存會議期間散佈的任何投影片或講義。在某些情況下，可能會有頻寬顧慮：有許多同時進行的會議，每個會議都包含數百位參與者且都會使用視訊播放和檔案共用，而這可能會導致您的網路出現問題。此外，有時可能也會有法律顧慮。例如，會議參與者預設可以在共用內容上加上註解；不過封存會議時並不會儲存這些註解。如果您的組織需要保留所有電子通訊的記錄，您可能會想要停用註解。

當然，需要管理會議設定是一回事，實際管理這些設定又是另一回事。在 Lync Server 中，會議是使用會議原則來管理 (在此軟體的舊版中，這些稱為會議原則)。但如上述，會議原則會判斷可在會議中使用的特性與功能；範圍從會議是否可包含 IP 音訊和視訊，到可出席會議的人數上限都涵蓋在內。會議原則可在全域範圍、網站範圍或個別使用者範圍設定。這可為系統管理員在決定哪些使用者可以使用哪些功能時提供了很大的彈性。

**Get-CsConferencingPolicy** Cmdlet 可讓您傳回設定供組織使用之所有會議原則的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsConferencingPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingPolicy"}

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
<td><p>可讓您在指定要傳回的原則時使用萬用字元。例如，下列語法會傳回在網站範圍設定的所有原則：-Filter &quot;site:*&quot;。若要傳回在個別使用者範圍設定的所有原則集合，請使用下列語法：-Filter tag:*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之會議原則的唯一識別碼。會議原則可以在全域、網站或個別使用者範圍設定。若要擷取全域原則，請使用下列語法：-Identity global。若要擷取網站原則，請使用類似下列的語法：-Identity site:Redmond。若要擷取個別使用者原則，請使用類似下列的語法：-Identity SalesConferencingPolicy。</p>
<p>若未加入此參數， <strong>Get-CsConferencingPolicy</strong> Cmdlet 會傳回設定供組織使用之所有會議原則的集合。</p>
<p>請注意，指定 Identity 時不允許使用萬元字元。如果您要在指定會議原則時使用萬用字元，請使用 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取會議原則資料，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsConferencingPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsConferencingPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Meeting.MeetingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)


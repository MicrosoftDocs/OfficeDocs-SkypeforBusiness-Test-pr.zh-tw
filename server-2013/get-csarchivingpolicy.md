---
title: Get-CsArchivingPolicy
TOCTitle: Get-CsArchivingPolicy
ms:assetid: 25d7de86-871d-4f07-8825-028137365435
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425731(v=OCS.15)
ms:contentKeyID: 49290371
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsArchivingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回立即訊息 (IM) 工作階段封存原則的資訊。封存原則可讓您封存內部使用者之間和/或內部使用者與外部使用者之間所發生的所有 IM 及 Web 會議工作階段。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsArchivingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsArchivingPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會直接呼叫不含任何參數的 **Get-CsArchivingPolicy** Cmdlet，這會傳回組織目前所使用之所有封存原則的集合。

    Get-CsArchivingPolicy

## 範例 2

在範例 2 中， **Get-CsArchivingPolicy** Cmdlet 用來傳回 Identity 為 site:Redmond 的封存原則。由於識別身分必須是唯一的，因此這個命令一律最多只傳回一個原則。

    Get-CsArchivingPolicy -Identity site:Redmond

## 範例 3

範例 3 會傳回已經在個別使用者範圍設定之所有封存原則的集合。作法是加入 Filter 參數及篩選值 "tag:\*"。此篩選值會指示 **Get-CsArchivingPolicy** Cmdlet 只傳回其 Identity 開頭為 "tag:" 字串值的原則。

    Get-CsArchivingPolicy -Filter tag:*

## 範例 4

範例 4 會傳回已停用內部 IM 工作階段封存之所有封存原則的集合。為達成此目的，會先使用 **Get-CsArchivingPolicy** Cmdlet 傳回目前所使用之所有封存原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。接著 **Where-Object** 會套用篩選，將傳回的資料限制在 ArchiveInternal 屬性等於 False 的原則。

    Get-CsArchivingPolicy | Where-Object {$_.ArchiveInternal -eq $False}

## 範例 5

範例 5 類似於範例 4，但在此範例中，命令會傳回內部及外部封存皆已停用的所有封存原則。為達成此目的，會先使用 **Get-CsArchivingPolicy** Cmdlet 傳回目前所使用之所有封存原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ArchiveInternal 和 ArchiveExternal 屬性都等於 False 的原則。-and 運算子會指示 **Where-Object** Cmdlet 只選取符合所有指定條件的原則。若要選取只符合一個 (或兩個) 所指定條件的原則，請使用 –or 運算子：

    Get-CsArchivingPolicy | Where-Object {$_.ArchiveInternal -eq $False -and $_.ArchiveExternal -eq $False}

## 詳細描述

許多組織發現保留使用者參與的所有 IM 工作階段封存很有幫助；其他組織則依法必須保留這樣的封存。您必須執行兩項步驟，才能使用 Lync Server 封存 IM 工作階段。首先，您必須使用 **Set-CsArchivingConfiguration** Cmdlet 來啟用全域和/或網站範圍的封存。這讓您可以封存 IM 工作階段；不過，它不會自動開始封存那些工作階段。

但是，若要實際儲存 IM 工作階段的文字記錄，您必須完成步驟 2：建立一或多個 IM 工作階段封存原則。這些原則會決定哪些使用者可記錄 IM 工作階段，以及要封存哪些類型的 IM 工作階段 (內部和/或外部)。內部 IM 工作階段是指，其中的所有參與者都是經過驗證的使用者，他們在組織內擁有 Active Directory 帳戶；外部 IM 工作階段是指，其中至少有一位參與者是未驗證的使用者，他們在組織內沒有 Active Directory 帳戶。您可以選擇只封存內部工作階段、只封存外部工作階段，或是同時封存內部和外部工作階段。

您可以將封存原則 (使用 **New-CsArchivingPolicy** Cmdlet 建立) 指派至全域網站或網站範圍。此外，這些原則還可以指派至個別使用者範圍；也就是說，您可以建立原則，然後將其套用至特定使用者或特定一組使用者。例如，您的全域原則可能會封存所有使用者的內部 IM 工作階段。此外，您可以建立第二個原則 (這個原則會封存內部和外部工作階段)，然後將該原則套用至銷售人員。因為個別使用者原則的優先順序高於全域範圍和網站原則，因此銷售人員的成員將會封存其所有 IM 工作階段。其他使用者 (也就是不在銷售部門且不受銷售原則影響的使用者) 就只會封存其內部 IM 工作階段。

**Get-CsArchivingPolicy** Cmdlet 可讓您傳回設定供組織使用之封存原則的資訊。請注意，只有當全域範圍或網站範圍已啟用 IM 工作階段封存時，才會施行這些原則。若要判斷是否已啟用 IM 工作階段封存，請使用 **Get-CsArchivingConfiguration** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsArchivingPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsArchivingPolicy"}

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
<td><p>System.Strkng</p></td>
<td><p>可讓您在指示要傳回的原則 (或多個原則) 時使用萬用字元。例如，若要傳回在網站範圍設定的所有原則，請使用下列語法：-Filter &quot;site:*&quot;。這會傳回 Identity 開頭為字串值 &quot;site:&quot; 的任何原則 (您篩選可依據的唯一內容)。若要傳回具有開頭為 &quot;Sales&quot; 之 Identity 的所有個別使用者原則集合，請使用下列語法：-Filter &quot;Sales*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之封存原則的唯一識別碼。若要參考全域原則，請使用下列語法：-Identity global。若要參考網站原則，請使用類似下列的語法：-Identity site:Redmond。若要參考個別使用者原則，請使用類似下列的語法：-Identity RedmondArchivingPolicy。如果省略此參數，則會傳回設定為在組織中使用的所有封存原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取封存原則資料，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsArchivingPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsArchivingPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Im.IMArchivingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)


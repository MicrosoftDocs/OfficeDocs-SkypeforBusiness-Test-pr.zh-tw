---
title: Get-CsPersistentChatEligiblePrincipal
TOCTitle: Get-CsPersistentChatEligiblePrincipal
ms:assetid: 541de778-3aca-4d3f-9d46-d9b6d8212987
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204891(v=OCS.15)
ms:contentKeyID: 49290936
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatEligiblePrincipal

 

_**上次修改主題的時間：** 2015-03-09_

傳回常設聊天室類別或聊天室的合格主體。合格主體包含允許的成員或管理員 (針對某個聊天室類別) 以及允許的簡報者 (僅限聊天室)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatEligiblePrincipal -Category <String> <COMMON PARAMETERS>

    Get-CsPersistentChatEligiblePrincipal -Room <String> [-Presenters <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Filter <String>] [-PersistentChatPoolFqdn <String>] [-ResultSize <Int32>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 ITChat 常設聊天室類別之合格主體的資訊。

    Get-CsPersistentChatEligiblePrincipal -PersistentChatPoolFqdn "atl-persistentchat-001.litwareinc.com" -Category "ITChat"

## 範例 2

範例 2 會傳回 HelpDeskChatRoom 聊天室之所有合格簡報者的資訊。

    Get-CsPersistentChatEligiblePrincipal -PersistentChatPoolFqdn "atl-persistentchat-001.litwareinc.com" -Room "HelpDeskChatRoom" -Presenters

## 範例 3

範例 3 是範例 2 所示之命令的變化；但此範例只會傳回非代表使用者帳戶之常設聊天室簡報者的資訊。為達成此目的，命令會先使用 **Get-CsPersistentChatEligiblePrincipal** Cmdlet 傳回 HelpDeskChatRoom 聊天室的所有簡報者。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 PersistentChatPrincipalType 屬性不等於 (-ne) "user" 的簡報者。

    Get-CsPersistentChatEligiblePrincipal -PersistentChatPoolFqdn "atl-persistentchat-001.litwareinc.com" -Room "HelpDeskChatRoom" -Presenters | Where-Object {$_.PersistentChatPrincipalType -ne "user"}

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

聊天室類別可讓您選擇是否要將某些使用者指定為「建立者」(代表這些使用者可以在該類別中建立聊天室)。同樣地，聊天室也可讓您將使用者指定為「管理員」及/或「簡報者」。使用者必須列名於指定類別/聊天室的 AllowedMembers 清單中，才能獲指派上述角色。您可以使用 [Get-CsPersistentChatRoom](get-cspersistentchatroom.md) Cmdlet 與 [Get-CsPersistentChatCategory](get-cspersistentchatcategory.md) Cmdlet，擷取聊天室或類別的允許成員清單。若加入允許成員清單中的是安全性群組、OU 或網域，您將看不到安全性群組中之使用者的名稱。例如，若允許清單中列的是安全性群組 FinanceManagers，您將看不到 FinanceManagers 中的成員名稱，而只會看見群組的名稱。

若要檢視該群組所有使用者的名稱 (以及類別或聊天室之允許成員清單中所有使用者的名稱)，請改用 **Get-CsPersistentChatEligiblePrincipal** 聊天室。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatEligiblePrincipal"}

Lync Server 控制台：**Get-CsPersistentChatEligiblePrincipal** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Category</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要傳回其合格主體之群組聊天類別的名稱。呼叫 <strong>Get-CsPersistentChatEligiblePrincipal</strong> Cmdlet 時，您必須使用 Category 或 Room 參數；不過，您不能在同一個命令中同時使用這些參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Room</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要傳回其合格主體之群組聊天室的名稱。呼叫 <strong>Get-CsPersistentChatEligiblePrincipal</strong> Cmdlet 時，您必須使用 Category 或 Room 參數；不過，您不能在同一個命令中同時使用這些參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>提供一種使用萬用字元搜尋來篩選合格主體的方式。例如：</p>
<p>-Filter &quot;*smith*&quot;</p>
<p>請注意，Filter 參數只能篩選使用者 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室集區的完整網域名稱。例如：</p>
<p>-PersistentChatPoolFqdn &quot;atl-persistentchat-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Presenters</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>當命令中包含此參數時，會傳回常設聊天室的合格簡報者。當命令中未包含時， <strong>Get-CsPersistentChatEligiblePrincipal</strong> Cmdlet 會改為傳回合格的成員和管理員。</p>
<p>此參數只能隨著 Room 參數一起使用，而且只能傳回設定為聽眾席之聊天室的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回七個常設聊天室主體 (不考慮樹系中的使用者數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七個主體。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個主體，則命令會傳回這三個主體，然後執行完成而不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPersistentChatEligiblePrincipal** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**Get-CsPersistentChatEligiblePrincipal** Cmdlet 會傳回 Microsoft.Rtc.Management.GroupChat.Cmdlets.ADPersistentChatPrincipal 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)


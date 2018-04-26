---
title: Get-CsPersistentChatRoom
TOCTitle: Get-CsPersistentChatRoom
ms:assetid: 9826c44b-35a6-473e-97d4-952415d640d1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205123(v=OCS.15)
ms:contentKeyID: 49291739
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatRoom

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之常設聊天室的資訊。聊天室相當於討論區，通常會以特定主題為主。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatRoom [-Addin <String>] [-Category <String>] [-ChatContentExceedsMB <Int32>] [-Disabled <$true | $false>] [-Filter <String>] [-Invitations <False | Inherit>] [-Manager <String>] [-Member <String>] [-PersistentChatPoolFqdn <String>] [-Privacy <Open | Closed | Secret>] [-ResultSize <Int32>] [-SearchDescription <SwitchParameter>] [-Type <Normal | Auditorium>] <COMMON PARAMETERS>

    Get-CsPersistentChatRoom [-Identity <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AsObject <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之常設聊天室的資訊。

    Get-CsPersistentChatRoom

## 範例 2

範例 2 會傳回單一常設聊天室 (Identity 為 atl-cs-001.litwareinc.com\\ITChatRoom 的聊天室) 的資訊。

    Get-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom"

## 範例 3

範例 3 會傳回為 atl-cs-001.litwareinc.com 集區所設定之所有常設聊天室的資訊。

    Get-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室的討論以在各個聊天室張貼訊息的形式進行；這些聊天室各有其討論的主題。根據設計，張貼在聊天室的訊息會永久保存，使用者可以隨時返回聊天室檢視其先前所張貼的所有訊息。

**Get-CsPersistentChatRoom** Cmdlet 可讓您傳回設定供組織使用之所有聊天室的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatRoom"}

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
<td><p><em>Addin</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>傳回與指定之聊天室增益集相關聯的聊天室。</p>
<p>請注意，每個命令只能指定一個增益集。</p></td>
</tr>
<tr class="even">
<td><p><em>AsObject</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，將會在顯示管理員或簡報者清單中的使用者時，使用 Active Directory 顯示名稱。若未指定，將會在顯示使用者時使用 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>Category</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>針對指定類別中的所有常設聊天室傳回資訊。例如：</p>
<p>-Category &quot;ITChat&quot;</p>
<p>使用 Category 參數時，只能指定單一類別。此外，您不能在使用 Category 參數的任何命令中使用 PersistentChatPoolFqdn、Filter 或 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>ChatContentExceedsMB</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>傳回累積聊天內容超過指定值 (MB) 的聊天室。</p></td>
</tr>
<tr class="odd">
<td><p><em>Disabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>可讓您搜尋作用中的聊天室 (使用 $False 參數值) 或已停用的聊天室 (使用 $True 參數值)。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您根據聊天室的 Name 及/或 Description，傳回常設聊天室的資訊。若要針對特定名稱的聊天室傳回資訊，請使用類似下列的語法：</p>
<p>-Filter {Name –like &quot;ITChat&quot;}</p>
<p>該語法只會針對名為 ITChat 的聊天室傳回資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要傳回之常設聊天室的唯一識別碼。聊天室的 Identity 包含常設聊天室集區，其中的聊天室都已設定加上聊天室的名稱；例如：</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\RedmondChatRoom&quot;</p>
<p>您不能在任何使用 Identity 參數的命令中使用 Category、Filter 或 PersistentChatPoolFqdn 參數。若您呼叫不含任何參數的 <strong>Get-CsPersistentChatRoom</strong> Cmdlet，該 Cmdlet 將會傳回設定供組織使用之所有聊天室的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Invitations</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomInvitations</p></td>
<td><p>傳回使用邀請函的聊天室 (使用 Inherit 參數值) 或未使用邀請函的聊天室 (使用 False 參數值)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Manager</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>傳回指定使用者所管理的聊天室。例如：</p>
<p>-Manager &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>請注意，您只能為每個命令各指定一位管理員。</p></td>
</tr>
<tr class="even">
<td><p><em>Member</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>傳回指定使用者所屬的聊天室。例如：</p>
<p>-Member &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>請注意，您只能為每個命令各指定一位成員。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>傳回在指定常設聊天室集區上設定之所有常設聊天室的資訊。例如：</p>
<p>-PersistentChatPoolFqdn &quot;atl-gc-001.litwareinc.com&quot;</p>
<p>您不能在使用 PersistentChatPoolFqdn 參數的任何命令中使用 Category、Filter 或 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Privacy</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomPrivacy</p></td>
<td><p>可讓您傳回符合指定隱私權設定的聊天室。允許的值為：</p>
<p>* Open (所有使用者都可以執行目錄搜尋來尋找聊天室，且所有人都可以參與聊天室活動)</p>
<p>* Secret (只有聊天室成員可以執行目錄搜尋來尋找聊天室，且只有成員可以參與聊天室活動)</p>
<p>* Closed (所有使用者都可以執行目錄搜尋來尋找聊天室，但是只有成員可以參與聊天室活動)</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回 7 個聊天室 (不考慮樹系中的聊天室數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪 7 個聊天室。</p>
<p>結果大小可以設為 0 到 2147483647 的任何整數。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個聊天室，則命令會傳回這三個聊天室，然後完成執行而不會出現錯誤。</p></td>
</tr>
<tr class="even">
<td><p><em>SearchDescription</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您在 Name 聊天室或 Description 聊天室中搜尋指定的文字值。若要同時搜尋 Name 和 Description，請隨著 Filter 參數包含 SearchDescription 參數。例如：</p>
<p>-SearchDescription –Filter &quot;IT chat room&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomType</p></td>
<td><p>依聊天室類型傳回聊天室。允許的值為：</p>
<p>* Normal (所有成員都可以張貼訊息的聊天室)</p>
<p>* Auditorium (只有簡報者可以張貼訊息的聊天室)</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPersistentChatRoom** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatRoom** Cmdlet 會傳回 Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject 物件的執行個體。

## 請參閱

#### 其他資源

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)  
[Remove-CsPersistentChatRoom](remove-cspersistentchatroom.md)  
[Set-CsPersistentChatRoom](set-cspersistentchatroom.md)


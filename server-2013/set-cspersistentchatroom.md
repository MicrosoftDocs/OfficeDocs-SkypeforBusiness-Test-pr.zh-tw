---
title: Set-CsPersistentChatRoom
TOCTitle: Set-CsPersistentChatRoom
ms:assetid: 3774931e-74a9-4189-9dde-3baae2293138
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204801(v=OCS.15)
ms:contentKeyID: 49290588
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatRoom

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的常設聊天室。聊天室相當於討論區，通常會以特定主題為主。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatRoom -Instance <ChatRoom> <COMMON PARAMETERS>

    Set-CsPersistentChatRoom -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Addin <String>] [-AsObject <SwitchParameter>] [-Category <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Disabled <$true | $false>] [-Force <SwitchParameter>] [-Invitations <False | Inherit>] [-Managers <PSListModifier>] [-Members <PSListModifier>] [-Name <String>] [-Presenters <PSListModifier>] [-Privacy <Open | Closed | Secret>] [-Type <Normal | Auditorium>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用 Identity 為 atl-cs-001.litwareinc.com\\ITChatRoom 的常設聊天室。

    Set-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -Disabled $True

## 範例 2

範例 2 會停用 atl-cs-001.litwareinc.com 上的所有常設聊天室。作法是先使用 **Get-CsPersistentChatRoom** Cmdlet 搭配 Identity 參數傳回設定供集區 atl-cs-001.litwareinc.com 使用的所有聊天室。然後再將這些聊天室管線傳送到 **Set-CsPersistentChatRoom** Cmdlet，以將每個聊天室的 Disabled 屬性設為 True ($True)。

    Get-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com" | Set-CsPersistentChatRoom -Disabled $True

## 範例 3

範例 3 會停用組織中的所有常設聊天室。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPersistentChatRoom** Cmdlet，以傳回所有常設聊天室的集合。然後，此集合會管線傳送到 **Set-CsPersistentChatRoom** Cmdlet，以停用集合中的每個聊天室。

    Get-CsPersistentChatRoom | Set-CsPersistentChatRoom -Disabled $True

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室的討論以在各個聊天室張貼訊息的形式進行；這些聊天室各有其討論的主題。根據設計，張貼在聊天室的訊息會永久保存，使用者可以隨時返回聊天室檢視其先前所張貼的所有訊息。

**Set-CsPersistentChatRoom** Cmdlet 可讓您修改設定供組織使用的聊天室，包括指派聊天室的管理員與簡報者。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示中執行下列命令

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatRoom"}

**Lync Server 控制台：**若要使用 Lync Server 控制台來修改現有的常設聊天室，請依序按一下 **\[常設聊天室\]** 及 **\[聊天室\]**，然後按兩下所要修改的聊天室。

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
<td><p>System.Strkng</p></td>
<td><p>要修改之常設聊天室的唯一識別碼。聊天室的 Identity 包含常設聊天室集區，其中的聊天室都已設定加上聊天室的名稱；例如：</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\RedmondChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoom</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Addin</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室增益集的名稱。如已指定，則會與聊天室相關聯。常設聊天室增益集是可在常設聊天室用戶端內嵌的自訂網頁。這些增益集可以使用 <strong>New-CsPersistentChatAddin</strong> Cmdlet 來建立。</p></td>
</tr>
<tr class="even">
<td><p><em>AsObject</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，將會在新增使用者到管理員或簡報者清單，或移除該清單中的使用者時，使用 Active Directory 顯示名稱。若未指定，將會在顯示使用者時使用 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>Category</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>聊天室所屬的類別；例如：</p>
<p>-Category &quot;IT&quot;</p>
<p>請注意，指定的類別必須已存在，否則命令會失敗。類別是聊天室的集合，可以用 <strong>New-CsPersistentChatCategory</strong> Cmdlet 來建立。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>讓系統管理員能夠提供新聊天室的其他資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Disabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，新聊天室在剛建立時會停用，而無法使用。若未使用此參數，就會啟用新聊天室，並可立即使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Invitations</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomInvitations</p></td>
<td><p>指定是否要繼承類別的聊天室邀請。這表示成員清單上的使用者會在新聊天室建立之後，自動收到加入新聊天室的邀請。若將此參數設為 False，聊天室將不會發出邀請。若設為 Inherit，聊天室將會使用該類別所指定的 Invitations 設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Managers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可定義聊天室成員資格的使用者清單，以及設定聊天室的其他設定。</p>
<p>若要將新使用者加入管理員清單，請使用類似下列的語法：</p>
<p>-Managers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要加入多位使用者，請用逗號分隔使用者 SIP 位址：</p>
<p>-Managers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>若要從管理員清單移除使用者，請使用 Remove 方法：</p>
<p>-Managers @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要從管理員清單中移除所有使用者，請將 Managers 屬性的值設為 Null：</p>
<p>-Managers $Null</p>
<p>除了與個別使用者合作，您也可以與整個 OU 合作。例如，下列命令會將 IT OU 中的所有使用者加入管理員清單：</p>
<p>-Managers @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>若要讓通訊群組清單中的所有使用者都成為聊天室管理員，請使用該通訊群組清單的 Active Directory 辨別名稱：</p>
<p>-Managers @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>Members</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>允許存取聊天室的使用者清單。如果 Members 屬性為 Null，則聊天室會繼承其常設聊天室類別的成員資格清單。</p>
<p>若要將新使用者加入成員清單，請使用類似下列的語法：</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要加入多位使用者，請用逗號分隔使用者 SIP 位址：</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>若要從成員清單移除使用者，請使用 Remove 方法：</p>
<p>-Members @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要從成員清單中移除所有使用者，請將 Members 屬性的值設為 Null：</p>
<p>-Members $Null</p>
<p>除了與個別使用者合作，您也可以與整個 OU 合作。例如，下列命令會將 IT OU 中的所有使用者加入成員清單：</p>
<p>-Members @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>若要讓通訊群組清單中的所有使用者都成為聊天室成員，請使用該通訊群組清單的 Active Directory 辨別名稱：</p>
<p>-Members @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室的名稱。每個常設聊天室集區的名稱都必須是唯一的。</p></td>
</tr>
<tr class="even">
<td><p><em>Presenters</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>允許在聽眾席聊天室中張貼訊息的使用者清單。</p>
<p>若要將新使用者加入主持人清單，請使用類似下列的語法：</p>
<p>-Presenters @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要加入多位使用者，請用逗號分隔使用者 SIP 位址：</p>
<p>-Presenters @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>若要從主持人清單移除使用者，請使用 Remove 方法：</p>
<p>-Presenters @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要從主持人清單中移除所有使用者，請將 Presenters 屬性的值設為 Null：</p>
<p>-Presenters $Null</p>
<p>除了與個別使用者合作，您也可以與整個 OU 合作。例如，下列命令會將 IT OU 中的所有使用者加入主持人清單：</p>
<p>-Presenters @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>若要讓通訊群組清單中的所有使用者都成為聊天室主持人，請使用該通訊群組清單的 Active Directory 辨別名稱：</p>
<p>-Presenters @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>Privacy</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomPrivacy</p></td>
<td><p>聊天室的隱私權設定。允許的值為：</p>
<p>* Open (所有使用者都可以執行目錄搜尋來尋找聊天室，且所有人都可以參與聊天室活動)</p>
<p>* Secret (只有聊天室成員可以執行目錄搜尋來尋找聊天室，且只有成員可以參與聊天室活動)</p>
<p>* Closed (所有使用者都可以執行目錄搜尋來尋找聊天室，但是只有成員可以參與聊天室活動)</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomType</p></td>
<td><p>指定要將聊天室設定成 Normal (一般) 聊天室 (所有成員都可以發佈訊息) 還是 Auditorium (聽眾席) (只有主持人可以發佈訊息)。例如：</p>
<p>-Type &quot;Auditorium&quot;</p>
<p>預設值為 Normal。</p></td>
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

**Set-CsPersistentChatRoom** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject 物件執行個體。

## 傳回類型

無。反之，**Set-CsPersistentChatRoom** Cmdlet 會修改現有的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject 物件執行個體。

## 請參閱

#### 其他資源

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[Get-CsPersistentChatRoom](get-cspersistentchatroom.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)  
[Remove-CsPersistentChatRoom](remove-cspersistentchatroom.md)


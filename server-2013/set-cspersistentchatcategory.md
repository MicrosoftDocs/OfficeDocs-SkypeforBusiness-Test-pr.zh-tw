---
title: Set-CsPersistentChatCategory
TOCTitle: Set-CsPersistentChatCategory
ms:assetid: 61f44b61-c1bb-46a8-af12-8d1c543fcda5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204952(v=OCS.15)
ms:contentKeyID: 49291097
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatCategory

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的常設聊天室類別。常設聊天室類別代表常設聊天室的集合。每個聊天室都必須關聯一個類別。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatCategory -Instance <Category> <COMMON PARAMETERS>

    Set-CsPersistentChatCategory -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowedMembers <PSListModifier>] [-AsObject <SwitchParameter>] [-ChatHistory <$true | $false>] [-Confirm [<SwitchParameter>]] [-Creators <PSListModifier>] [-DeniedMembers <PSListModifier>] [-Description <String>] [-FileUpload <$true | $false>] [-Invitations <$true | $false>] [-Name <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會停用常設聊天室類別 atl-cs-001.litwareinc.com\\helpdesk 的檔案上傳功能。

    Set-CsPersistentChatCategory -Identity "atl-cs-001.litwareinc.com\helpdesk" -FileUpload $False

## 範例 2

範例 2 會停用組織目前使用之所有常設聊天室類別的檔案上傳功能。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsPersistentChatCategory** Cmdlet，以傳回所有常設聊天室類別的集合。然後再將該集合中的類別管線傳送到 **Set-CsPersistentChatCategory** Cmdlet，以停用每個類別的檔案上傳功能。

    Get-CsPersistentChatCategory | Set-CsPersistentChatCategory-FileUpload $False

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室類別可讓系統管理員組織及管理常設聊天室。類別可以讓系統管理員將聊天室分門別類地編組，例如將財務部門所用的所有聊天室編入同一個類別。同樣地，類別也可讓系統管理員管理這些聊天室的權限，指定有權存取這些聊天室的使用者，不可存取這些聊天室的使用者，以及可以在類別中建立新聊天室的使用者。

請注意，所有聊天室必須隸屬於相同的類別。您必須先指派聊天室的類別，才可建立聊天室。亦即，您至少須建立一個類別之後，才可在您的常設聊天室實作中新增聊天室。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatCategory"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 修改現有的常設聊天室類別，請按一下 **\[常設聊天室\]**，然後按一下 **\[類別\]**，接著按兩下所要修改的類別。

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
<td><p>聊天室類別的唯一識別碼。此 Identity 由類別所在的常設聊天室集區加類別名稱組成；例如：</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\ITChat&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Category</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedMembers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>列出允許存取該類別中之聊天室的使用者。若要將新使用者加入成員清單，請使用類似下列的語法：</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要加入多位使用者，請用逗號分隔使用者 SIP 位址：</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>若要從成員清單移除使用者，請使用 Remove 方法：</p>
<p>-Members @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要從成員清單中移除所有使用者，請將 Members 屬性的值設為 Null：</p>
<p>-AllowedMembers $Null</p>
<p>除了與個別使用者合作，您也可以與整個 OU 合作。例如，下列命令會讓 IT OU 中的所有使用者存取聊天室：</p>
<p>-Members @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>若要新增通訊群組清單中的所有使用者，請使用該通訊群組清單的 Active Directory 辨別名稱：</p>
<p>-Members @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>AsObject</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，將會在新增使用者到 AllowedMembers、DeniedMembers 與 Creators 清單，或移除這些清單中的使用者時，使用 Active Directory 顯示名稱。若未指定，將會在顯示使用者時使用 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>ChatHistory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 False ($False) 時，會為新類別停用聊天記錄功能。通常只有針對為了發佈過一次後即不再需要參照的宣告而使用的聊天室，才會停用聊天記錄。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Creators</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>列出允許建立該類別中之聊天室的使用者。若要將新使用者加入建立者清單，請使用類似下列的語法：</p>
<p>-Creators @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要加入多位使用者，請用逗號分隔使用者 SIP 位址：</p>
<p>-Creators @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>若要從建立者清單移除使用者，請使用 Remove 方法：</p>
<p>-Creators @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要從成員清單中移除所有使用者，請將 Creators 屬性的值設為 Null：</p>
<p>-Creators $Null</p>
<p>除了與個別使用者合作，您也可以與整個 OU 合作。例如，下列命令會讓 IT OU 中的所有使用者建立聊天室：</p>
<p>-Creators @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>若要新增通訊群組清單中的所有使用者，請使用該通訊群組清單的 Active Directory 辨別名稱：</p>
<p>-Creators @{Add=&quot;CN=ChatSupportGroup.OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>DeniedMembers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>列出不允許存取該類別中之聊天室的使用者。若要將新使用者加入 DeniedMembers 清單，請使用類似下列的語法：</p>
<p>-DeniedMembers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要加入多位使用者，請用逗號分隔使用者 SIP 位址：</p>
<p>-DeniedMembers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>若要從 DeniedMembers 清單移除使用者，請使用 Remove 方法：</p>
<p>-DeniedMembers @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>若要從 DeniedMembers 清單中移除所有使用者，請將 DeniedMembers 屬性的值設為 Null：</p>
<p>-DeniedMembers $Null</p>
<p>除了與個別使用者合作，您也可以與整個 OU 合作。例如，下列命令會拒絕 IT OU 中的所有使用者存取聊天室：</p>
<p>-DeniedMembers @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>若要拒絕通訊群組清單中的所有使用者存取，請使用該通訊群組清單的 Active Directory 辨別名稱：</p>
<p>-DeniedMembers @{Add=&quot;CN=ChatSupportGroup.OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室類別隨附的其他文字。例如，「說明」可能會解釋類別的用途，以及您可以在類別中找到的聊天室類型。</p></td>
</tr>
<tr class="even">
<td><p><em>FileUpload</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，可允許檔案上傳至該類別中的聊天室。</p></td>
</tr>
<tr class="odd">
<td><p><em>Invitations</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 False ($False) 時，會為類別啟用邀請功能。其中一個意義是，在新聊天室建立之後，AllowedMembers 清單上的使用者會自動收到加入新聊天室的邀請。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>提供給常設聊天室類別命名的名稱。每個常設聊天室集區都必須具有專用的名稱。</p></td>
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

**Set-CsPersistentChatCategory** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject 物件執行個體。

## 傳回類型

無。反之， **Set-CsPersistentChatCategory** Cmdlet 會修改現有的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatCategory](get-cspersistentchatcategory.md)  
[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Remove-CsPersistentChatCategory](remove-cspersistentchatcategory.md)


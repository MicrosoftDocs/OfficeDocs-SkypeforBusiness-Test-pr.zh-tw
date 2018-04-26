---
title: New-CsPersistentChatCategory
TOCTitle: New-CsPersistentChatCategory
ms:assetid: 37a6f55d-0fec-480f-8d96-60c313a48c74
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204803(v=OCS.15)
ms:contentKeyID: 49290595
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatCategory

 

_**上次修改主題的時間：** 2015-03-09_

建立新的常設聊天室類別。常設聊天室類別代表常設聊天室的集合。每個聊天室都必須關聯一個類別。請注意，您無法在建立類別時將聊天室指派給類別，而必須在之後使用 **Set-CsPersistentChatRoom** Cmdlet 為現有的聊天室指派類別。但可以在建立聊天室時，指派新聊天室的類別。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatCategory -Name <String> [-Description <String>] [-EnableFileUpload <SwitchParameter>] [-EnableInvitations <SwitchParameter>] [-PersistentChatPoolFqdn <String>] [-RemoveChatHistory <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會在 atl-cs-001.litwareinc.com 集區上建立名為 HelpDesk 的新常設聊天室類別。此範例會藉由加入 EnableFileUpload 參數來啟用檔案上傳。

    New-CsPersistentChatCategory -Name "HelpDesk" -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com" -EnableFileUpload 

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室類別可讓系統管理員組織及管理常設聊天室。類別可以讓系統管理員將聊天室分門別類地編組，例如將財務部門所用的所有聊天室編入同一個類別。同樣地，類別也可讓系統管理員管理這些聊天室的權限，指定有權存取這些聊天室的使用者，不可存取這些聊天室的使用者，以及可以在類別中建立新聊天室的使用者。

請注意，所有聊天室必須隸屬於相同的類別。您必須先指派聊天室的類別，才可建立聊天室。亦即，您至少須建立一個類別之後，才可在您的常設聊天室實作中新增聊天室。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatCategory"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 建立新的常設聊天室類別，請依序按一下 **\[常設聊天室\]**、**\[類別\]** 及 **\[新增\]**。

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>提供給常設聊天室類別命名的名稱。每個常設聊天室集區都必須具有專用的名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室類別隨附的其他文字。例如，「說明」可能會解釋類別的用途，以及您可以在類別中找到的聊天室類型。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFileUpload</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，可允許檔案上傳至該類別中的聊天室。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableInvitations</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>包含此參數時，會為類別啟用邀請功能。其中一個意義是，在新聊天室建立之後，AllowedMembers 清單上的使用者會自動收到加入新聊天室的邀請。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>應建立類別之常設聊天室集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveChatHistory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>包含此參數時，會為新類別停用聊天記錄功能。通常只有針對為了發佈過一次後即不再需要參照的宣告而使用的聊天室，才會停用聊天記錄。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsPersistentChatCategory** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatCategory** Cmdlet 會建立 Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatCategory](get-cspersistentchatcategory.md)  
[Remove-CsPersistentChatCategory](remove-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)


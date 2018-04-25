---
title: Remove-CsPersistentChatCategory
TOCTitle: Remove-CsPersistentChatCategory
ms:assetid: 09d2c1e6-07b6-47c2-b48f-f0c8bdfa1507
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204660(v=OCS.15)
ms:contentKeyID: 49290031
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatCategory

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的常設聊天室類別。常設聊天室類別代表常設聊天室的集合，而其中的每一個聊天室都必須關聯一種類別。 Lync Server 2013 中已導入此 Cmdlet。請注意，除非是空的類別 (亦即，類別中的所有聊天室已在您移除類別前先行移除)，否則無法移除類別。

## 語法

    Remove-CsPersistentChatCategory -Identity <String> <COMMON PARAMETERS>

    Remove-CsPersistentChatCategory -Instance <Category> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Identity 為 "atl-cs-001.litwareinc.com\\helpdesk" 的常設聊天室類別。

    Remove-CsPersistentChatCategory -Identity "atl-cs-001.litwareinc.com\helpdesk"

## 範例 2

在範例 2 中，組織中目前使用的所有常設聊天室類別都會移除。為達成此目的，命令會先使用 **Get-CsPersistentChatCategory** Cmdlet 來擷取所有常設聊天室類別的集合。會將此集合管線傳送到 **Remove-CsPersistentChatCategory** Cmdlet，以刪除集合中的每一個類別。

    Get-CsPersistentChatCategory | Remove-CsPersistentChatCategory

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室類別可讓系統管理員組織及管理常設聊天室。類別可以讓系統管理員將聊天室分門別類地編組，例如將財務部門所用的所有聊天室編入同一個類別。同樣地，類別也可讓系統管理員管理這些聊天室的權限，指定有權存取這些聊天室的使用者，不可存取這些聊天室的使用者，以及可以在類別中建立新聊天室的使用者。

請注意，所有聊天室必須隸屬於相同的類別。您必須先指派聊天室的類別，才可建立聊天室。亦即，您至少須建立一個類別之後，才可在您的常設聊天室實作中新增聊天室。

**Remove-CsPersistentChatCategory** Cmdlet 可用於移除常設聊天室的類別。請注意，只有空的類別才可移除。換言之，必須先移除類別中的所有聊天室，才可移除類別本身。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatCategory"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 移除常設聊天室類別，請依序按一下 **\[常設聊天室\]** 及 **\[類別\]**。選取所要移除的類別，按一下 **\[編輯\]**，然後按一下 **\[刪除\]**。

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
<td><p>要移除之常設聊天室類別的唯一識別碼。Identity 包含 PoolFqdn 加上類別 Name；例如：</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com\helpdesk&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Category</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

**Remove-CsPersistentChatCategory** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject 物件執行個體。此 Cmdlet 也接受代表現有常設聊天室類別之 Identity 的字串值。

## 傳回類型

無。反之， **Remove-CsPersistentChatCategory** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatCategory](get-cspersistentchatcategory.md)  
[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)


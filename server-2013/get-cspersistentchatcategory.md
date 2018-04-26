---
title: Get-CsPersistentChatCategory
TOCTitle: Get-CsPersistentChatCategory
ms:assetid: 2ec14091-cb05-4c4c-b091-b7e88f5ca3cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204771(v=OCS.15)
ms:contentKeyID: 49290470
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatCategory

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之常設聊天室類別的資訊。常設聊天室類別代表常設聊天室的集合。每個聊天室都必須關聯一個類別。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatCategory [-PersistentChatPoolFqdn <String>] <COMMON PARAMETERS>

    Get-CsPersistentChatCategory -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AsObject <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有常設聊天室類別的資訊。

    Get-CsPersistentChatCategory

## 範例 2

範例 2 會傳回所有設定供 atl-cs-001.litwareinc.com 集區使用之所有常設聊天室類別的資訊。

    Get-CsPersistentChatCategory -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"

## 範例 3

範例 3 會傳回所有 Invites 屬性設為 False 之常設聊天室類別的資訊。為達成此目的，命令會先使用 **Get-CsPersistentChatCategory** Cmdlet 傳回所有常設聊天室類別的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 Invites 屬性設為 False ($False) 的類別。

    Get-CsPersistentChatCategory | Where-Object {$_.Invites -eq $False}

## 範例 4

範例 4 會傳回建立者包含 Ken Myer 之所有常設聊天室類別傳回資訊。為達成此目的，命令會先使用 **Get-CsPersistentChatCategory** Cmdlet傳回所有常設聊天室類別的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Creators 屬性包含 (-contains) "Ken Myer" 名稱的類別。

    Get-CsPersistentChatCategory | Where-Object {$_.Creators -contains "Ken Myer"}

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室類別可讓系統管理員組織及管理常設聊天室。類別可以讓系統管理員將聊天室分門別類地編組，例如將財務部門所用的所有聊天室編入同一個類別。同樣地，類別也可讓系統管理員管理這些聊天室的權限，指定有權存取這些聊天室的使用者，不可存取這些聊天室的使用者，以及可以在類別中建立新聊天室的使用者。

請注意，所有聊天室必須隸屬於相同的類別。您必須先指派聊天室的類別，才可建立聊天室。亦即，您至少須建立一個類別之後，才可在您的常設聊天室實作中新增聊天室。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatCategory"}

**Lync Server 控制台：**若要在 Lync Server 控制台 中檢視常設聊天室類別，請按一下 **\[常設聊天室\]**，然後再按一下 **\[類別\]**。

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
<td><p><em>AsObject</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，將會在顯示 AllowedMembers、DeniedMembers 或 Creators 清單中的使用者時，使用 Active Directory 顯示名稱。若未指定，將會在顯示使用者時使用 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>主控常設聊天室類別之常設聊天室集區的完整網域名稱。如果您使用 PoolFqdn 參數，而未包含 Name 參數，則會針對指定集區上的所有常設聊天室類別傳回資訊。如果 Name 和 PoolFqdn 參數都未包含，則會傳回所有常設聊天室類別的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPersistentChatCategory** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatCategory** Cmdlet 會傳回 Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Remove-CsPersistentChatCategory](remove-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)


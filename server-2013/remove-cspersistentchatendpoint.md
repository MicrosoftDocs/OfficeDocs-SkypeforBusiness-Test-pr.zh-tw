---
title: Remove-CsPersistentChatEndpoint
TOCTitle: Remove-CsPersistentChatEndpoint
ms:assetid: 0211850c-b4e7-4bb2-9a82-bfbfbd7de7b7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204626(v=OCS.15)
ms:contentKeyID: 49289901
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的常設聊天室端點。常設聊天室端點是 Active Directory 連絡人物件，是 Lync Server 2013 之常設聊天室集區的易記 URL。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPersistentChatEndpoint -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 "sip:pce@litwareinc.com" 的常設聊天室端點。此範例會以 SIP 位址做為 Identity。

    Remove-CsPersistentChatEndpoint -Identity "sip:pce@litwareinc.com"

## 範例 2

範例 2 會刪除所有為 atl-pcpool-001.litwareinc.com 集區設定的常設聊天室端點。為了執行此工作，命令會先使用 **Get-CsPersistentChatEndpoint** Cmdlet 及 PoolFqdn 參數傳回 atl-pcpool-001.litwareinc.com 集區的所有端點。然後再將該集合中的端點管線傳送到 **Remove-CsPersistentChatEndpoint** Cmdlet 加以移除。

    Get-CsPersistentChatEndpoint -PoolFqdn "atl-pcpool-001.litwareinc.com" | Remove-CsPersistentChatEndpoint

## 範例 3

範例 3 所示的命令會刪除設定供組織使用的所有常設聊天室端點。為達成此目的，命令會先呼叫 **Get-CsPersistentChatEndpoint** Cmdlet 傳回所有常設聊天室端點的集合。然後，此集合會管線傳送到 **Remove-CsPersistentChatEndpoint** Cmdlet，刪除集合中的每個端點。

    Get-CsPersistentChatEndpoint | Remove-CsPersistentChatEndpoint

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

但您若是有使用者執行舊版的用戶端 (例如 Microsoft Lync 2010)，這些使用者在將其舊版用戶端指向集區時，可能會發現預設的常設聊天室 URI 十分不好使用。有鑑於此，系統管理員可以使用 [New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md) Cmdlet 另外建立一個連絡人物件，提供易記易用的 URI。這些端點之後可以使用 **Remove-CsPersistentChatEndpoint** Cmdlet 加以移除。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatEndpoint"}

Lync Server 控制台：**Remove-CsPersistentChatEndpoint** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要移除之常設聊天室端點的唯一識別碼。端點 Identity 通常是以端點的 SIP 位址或顯示名稱來指定；例如：</p>
<p>-Identity &quot;sip:pcEndpoint1@litwareinc.com&quot;</p>
<p>不過，您也可以使用端點的完整 Identity；例如：</p>
<p>-Identity &quot;CN={33e5014b-dcba-46b5-9bf7-48f4d5fca69d}, CN=Application Contacts,CN=RTC Service,CN=Services,CN=Configuration,DC=litwareinc,DC=com&quot;</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

**Remove-CsPersistentChatEndpoint** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.ADConnect.Schema.OCSPersistentChatContact 類別執行個體。

## 傳回類型

無。 **Remove-CsPersistentChatEndpoint** Cmdlet 不會傳回物件或資料。

## 請參閱

#### 其他資源

[Get-CsPersistentChatEndpoint](get-cspersistentchatendpoint.md)  
[New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md)


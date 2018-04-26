---
title: Get-CsPersistentChatAddin
TOCTitle: Get-CsPersistentChatAddin
ms:assetid: 0d6b3283-c73d-4b83-b0f8-8f03aa4bba14
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204670(v=OCS.15)
ms:contentKeyID: 49290077
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatAddin

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之所有常設聊天室增益集的資訊。常設聊天室增益集是自訂的網頁，可以嵌入常設聊天室用戶端中。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatAddin [-PersistentChatPoolFqdn <String>] <COMMON PARAMETERS>

    Get-CsPersistentChatAddin -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

範例 1 會傳回所有設定供組織之用的所有常設聊天室增益集的資訊。

    Get-CsPersistentChatAddin

## 範例 2

範例 2 會傳回特定常設聊天室增益集 (即 Identity 為 atl-cs-001.litwareinc.com\\ITPersistentChatAddin 的增益集) 的資訊。

    Get-CsPersistentChatAddin -Identity "atl-cs-001.litwareinc.com\ITPersistentChatAddin"

## 範例 3

範例 3 會傳回所有設定供 atl-cs-001.litwareinc.com 上的集區之用的常設聊天室的資訊。

    Get-CsPersistentChatAddin -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

增益集是常設聊天室的延伸模組。增益集是和特定聊天室相關的外部應用程式 (亦即常設聊天室的內建項目)。例如「服務台」聊天室可以包含連結到網頁或 Silverlight 應用程式的 URL，以顯示當日協助要求的狀態。 Lync ServerWindows PowerShell 命令列介面 Cmdlet 無法建立這些增益集，而必須使用 **CsPersistentChatAddin** Cmdlet 關聯 (或取消關聯) 聊天室的增益集。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatAddin"}

**Lync Server 控制台：**若要在 Lync Server 控制台 中檢視常設聊天室增益集的資訊，請按一下 **\[常設聊天室\]**，然後再按一下 **\[增益集\]**。

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
<td><p>要傳回之常設聊天室增益集的唯一識別碼。Identity 由增益集所在之常設聊天室集區的完整網域名稱、&quot;\&quot; 字元及增益集名稱組成。例如：</p>
<p>-Identity &quot;atl-gc-001.litwareincom\ITPersistentChatAddin&quot;</p>
<p>若未指定此參數， <strong>Get-CsPersistentChatAddin</strong> Cmdlet 會傳回所有常設聊天室增益集的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室集區的完整網域名稱。如有使用此參數，將只會傳回在指定集區上所找到的常設聊天室增益集。若未使用此參數， <strong>Get-CsPersistentChatAddin</strong> Cmdlet 將會傳回所有常設聊天室集區的增益集。例如：</p>
<p>–PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPersistentChatAddin** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatAddin** Cmdlet 會傳回 Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsPersistentChatAddin](new-cspersistentchataddin.md)  
[Remove-CsPersistentChatAddin](remove-cspersistentchataddin.md)  
[Set-CsPersistentChatAddin](set-cspersistentchataddin.md)


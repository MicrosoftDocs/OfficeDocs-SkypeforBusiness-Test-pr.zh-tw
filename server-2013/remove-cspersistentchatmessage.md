---
title: Remove-CsPersistentChatMessage
TOCTitle: Remove-CsPersistentChatMessage
ms:assetid: 0cb53905-4608-44a9-ba3d-ba51fc90d65e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204668(v=OCS.15)
ms:contentKeyID: 49290078
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatMessage

 

_**上次修改主題的時間：** 2015-03-09_

以預設訊息或系統管理員提供的訊息，取代常設聊天室資料庫中的一或多則常設聊天室訊息。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPersistentChatMessage -ReplaceMessage <String> [-CaseSensitive <$true | $false>] [-EndDate <DateTime>] [-Filter <String>] [-MatchClause <And | Or | Exact>] [-StartDate <DateTime>] [-UserUri <String>] <COMMON PARAMETERS>

    Remove-CsPersistentChatMessage -Remove <SwitchParameter> [-CaseSensitive <$true | $false>] [-EndDate <DateTime>] [-Filter <String>] [-MatchClause <And | Or | Exact>] [-StartDate <DateTime>] [-UserUri <String>] <COMMON PARAMETERS>

    Remove-CsPersistentChatMessage [-CaseSensitive <$true | $false>] [-EndDate <DateTime>] [-Filter <String>] [-MatchClause <And | Or | Exact>] [-StartDate <DateTime>] [-UserUri <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 atl-persistentchat-001.litwareinc.com 伺服器上的 ITChatRoom 聊天室中，移除 2012 年 4 月 1 日當天或之前發佈的所有常設聊天室訊息。

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -EndDate "4/1/2012"

## 範例 2

範例 2 會從 atl-persistentchat-001.litwareinc.com 伺服器上的 ITChatRoom 聊天室中，移除使用者 kenmyer@litwareinc.com 所發佈的所有常設聊天室訊息。

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -UserUri "sip:kenmyer@litwareinc.com"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室的討論以在各個聊天室張貼訊息的形式進行；這些聊天室各有其討論的主題。根據設計，張貼在聊天室的訊息會永久保存，使用者可以隨時返回聊天室檢視其先前所張貼的所有訊息。

系統管理員偶爾可能也需要移除聊天室中的訊息，例如使用者張貼了一些有關即將召開的公司會議訊息，但訊息中卻包含了錯誤資訊時。 **Remove-CsPersisentChatMessage** Cmdlet 可讓系統管理員移除單一聊天訊息，或根據條件 (如訊息的張貼者或訊息中的關鍵字) 移除整組的聊天訊息。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatMessage"}

**Lync Server 控制台：** **Remove-CsPersistentChatMessage** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>包含要刪除之訊息的聊天室的唯一識別碼。例如：</p>
<p>-Identity &quot;atl-persistentchat-001.litwareinc.com\ITChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Remove</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，可不使用任何替換訊息而直接移除常設聊天室訊息。</p>
<p>請勿在同一個命令中同時使用 Remove 參數與 ReplaceMessage 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReplaceMessage</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員指定取代訊息的文字。根據預設，取代訊息為 &quot;This message was replaced by the Persistent Chat administrator&quot; (常設聊天室系統管理員已取代此訊息)。</p></td>
</tr>
<tr class="even">
<td><p><em>CaseSensitive</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如有指定此參數，表示在搜尋所要移除的訊息時，應區分大小寫 (換句話說，大寫 &quot;A&quot; 會視為不同於小寫 &quot;a&quot; 的字元)。根據預設，搜尋不會區分大小寫。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EndDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>可讓您篩選出在指定日期當天或之前發佈的訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可用於識別要刪除之訊息的關鍵字。例如，若要搜尋所有包含關鍵字 &quot;Fabrikam&quot; 的訊息，請使用下列語法：</p>
<p>-Filter &quot;Fabrikam&quot;</p>
<p>若要搜尋多個關鍵字，請將所有關鍵字放在單一字串中，並使用空格分隔：</p>
<p>-Filter &quot;Fabrikam Contoso TailspinToys&quot;</p>
<p>根據預設， <strong>Remove-CsPersistentChatMessage</strong> Cmdlet 會使用所有指定關鍵字來搜尋訊息。若要使用所提供之任一關鍵字來搜尋訊息，請使用 MatchClause 參數，並將參數值設為 &quot;Or&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>MatchClause</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.RemoveOcsMessageChatCmdlet+AndOr</p></td>
<td><p>指定 <strong>Remove-CsPersistentChatMessage</strong> Cmdlet 如何處理多個關鍵字。允許的值為：</p>
<p>* All (訊息必須包含所有指定的關鍵字，才會視為相符)</p>
<p>* Or (只要訊息包含一或多個指定關鍵字，就會視為相符)</p>
<p>* Exact (訊息必須完全符合指定的片語 (含字詞順序)，才會視為相符)</p>
<p>例如，下列語法會搜尋訊息文字中包含完整片語 &quot;For internal use only&quot; 的訊息：</p>
<p>-Filter &quot;For internal use only&quot; –MatchClause &quot;Exact&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>StartDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>可讓您篩選出在指定日期當天或之後發佈的訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>UserUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>發佈所應移除之訊息的使用者的 SIP 位址。</p></td>
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

無。 **Remove-CsPersistentChatMessage** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)


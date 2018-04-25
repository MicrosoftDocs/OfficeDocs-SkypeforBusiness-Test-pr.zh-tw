---
title: Export-CsPersistentChatData
TOCTitle: Export-CsPersistentChatData
ms:assetid: f4855109-26e0-41b8-8a9f-890f8d892645
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205378(v=OCS.15)
ms:contentKeyID: 49292813
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsPersistentChatData

 

_**上次修改主題的時間：** 2015-03-09_

從常設聊天室資料庫匯出資料。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Export-CsPersistentChatData [-FileName <String>] <COMMON PARAMETERS>

    Export-CsPersistentChatData [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -DBInstance <String> [-DBName <String>] [-DisableExportedNodes <SwitchParameter>] [-Level <User | Category | RoomDirectory | Content | All>] [-Report <String>] [-Scope <List>] [-StartDate <DateTime>]

## 範例

## 範例 1

範例 1 所示的命令會從位於伺服器 atl-sql-001.litwareinc.com 的常設聊天室資料庫匯出常設聊天室資料；匯出的資料會儲存在 C:\\Logs\\PersistentChatData.zip 檔案中。由於未指定 Level 參數，因此 **Export-CsPersistentChatData** Cmdlet 會完整匯出常設聊天室資訊。

    Export-CsPersistentChatData -DBInstance "atl-sql-001.litwareinc.com\rtc" -FileName "C:\Logs\PersistentChatData.zip"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

若您目前是使用 Lync Server 2010，可以先使用 **Export-CsPersistentChatData** Cmdlet 匯出現有的群組聊天組態設定，然後再使用 **Import-CsPersistentChatData** Cmdlet 將該資訊匯入 Lync Server 2013 與常設聊天室服務的方式來移轉目前的群組聊天實作。請注意， **Export-CsPersistentChatData** Cmdlet 會讓您選擇要匯入所有的群組聊天設定與資料，或只匯入其中的部分設定與資料。例如，您可以只匯出 (然後匯入) 群組聊天類別與聊天室，而不匯出這些類別與聊天室的所有相關內容。

**CsPersistentChatData** Cmdlet 的主要用途雖在移轉，但也可用於管理 Lync Server 2013 上的常設聊天室資料。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsPersistentChatData"}

Lync Server 控制台：**Export-CsPersistentChatData** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>DBInstance</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server 2013 常設聊天室資料庫所在之 SQL Server 執行個體的完整網域名稱及名稱。例如，下列語法會指定在伺服器 atl-sql-001.litwareinc.com 之 RTC 資料庫執行個體中所找到的資料庫：</p>
<p>-DBInstance &quot;atl-sql-001.litwareinc.com\rtc&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>以位元組陣列的方式傳回常設聊天室資訊；傳回的資料必須儲存在變數中，如此才能供 <strong>Import-CsPersistentChatData</strong> Cmdlet 使用。同一個命令中不可同時使用 AsBytes 和 FileName。</p></td>
</tr>
<tr class="odd">
<td><p><em>DBName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>常設聊天室資料庫的 SQL 執行個體名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableExportedNodes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，將會在匯出完成時停用所有匯出的類別和聊天室。</p></td>
</tr>
<tr class="odd">
<td><p><em>FileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p><strong>Export-CsPersistentChatData</strong> Cmdlet 所建立之 .ZIP 檔案的完整路徑；此檔案包含匯出的使用者資料。例如：</p>
<p>-FileName &quot;C:\Logs\PersistentChatData.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Level</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ExportLevel</p></td>
<td><p>可讓您指定要匯出的常設聊天室資訊。允許的值為：</p>
<p>* All</p>
<p>* User</p>
<p>* Category</p>
<p>* RoomDirectory</p>
<p>* Content</p>
<p>預設值為 All，表示要匯出所有常設聊天室資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行此 Cmdlet 時所建立之記錄檔的完整路徑。例如：</p>
<p>-Report &quot;C:\Logs\ExportPersistentChat.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scope</em></p></td>
<td><p>選用</p></td>
<td><p>System.Collections.Generic.List</p></td>
<td><p>可讓您匯出一組指定類別的資料 (及其對應的聊天室)。預設會匯出所有類別。</p></td>
</tr>
<tr class="odd">
<td><p><em>StartDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>要匯出之常設聊天室內容所在期間的開始日期。例如：</p>
<p>-StartDate &quot;1/1/2012&quot;</p>
<p>當 Level 設為 RoomDirectory 時才可使用此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Export-CsPersistentChatData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Export-CsPersistentChatData** Cmdlet 會建立 .ZIP 檔案。


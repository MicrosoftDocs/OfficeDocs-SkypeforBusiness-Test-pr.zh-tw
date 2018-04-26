---
title: Import-CsPersistentChatData
TOCTitle: Import-CsPersistentChatData
ms:assetid: 17151a25-5dea-498a-93d5-fed3da7d3fa5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204709(v=OCS.15)
ms:contentKeyID: 49290210
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsPersistentChatData

 

_**上次修改主題的時間：** 2015-03-09_

可讓系統管理員將 Microsoft Lync Server 2010 群組聊天資料庫所匯出的資料，匯入 Lync Server 2013 常設聊天室資料庫。此資料必須是使用 **Export-CsPersistentChatData** Cmdlet 從群組聊天資料庫匯出。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Import-CsPersistentChatData -FileName <String> <COMMON PARAMETERS>

    Import-CsPersistentChatData -ByteInput <Byte[]> <COMMON PARAMETERS>

    COMMON PARAMETERS: -DBInstance <String> [-Confirm [<SwitchParameter>]] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 C:\\Logs\\PersistentChatExport.xml 檔案讀取匯出的常設聊天室資料，然後將該資料加入 atl-sql-001.litwareinc.com\\rtc 常設聊天室資料庫 (其中 "atl-sql-001.litwareinc.com" 是 SQL Server 電腦的完整網域名稱，而 "rtc" 是 SQL Server 資料庫執行個體)。

    Import-CsPersistentChatData -DBInstance "atl-sql-001.litwareinc.com\rtc" -FileName "C:\Logs\PersistentChatExport.zip"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

若您目前是使用 Lync Server 2010，可以先使用 E**xport-CsPersistentChatData** Cmdlet 匯出現有的群組聊天組態設定，然後再使用 **Import-CsPersistentChatData** Cmdlet 將該資訊移轉至 Lync Server 2013 與常設聊天室服務，藉此移轉目前的群組聊天實作。請注意，**Export-CsPersistentChatData** Cmdlet 可讓您選擇要匯入所有的群組聊天設定與資料，或只匯入其中的部分設定與資料。例如，您可以只匯出 (然後匯入) 群組聊天類別與聊天室，而不匯出這些類別與聊天室的所有相關內容。

**CsPersistentChatData** Cmdlet 的主要用途雖在移轉，但也可用於管理 Lync Server 2013 上的常設聊天室資料。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsPersistentChatData"}

**Lync Server 控制台：** **Import-CsPersistentChatData** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>ByteInput</em></p></td>
<td><p>必要</p></td>
<td><p>System.Byte[]</p></td>
<td><p>指定此參數時，資料會匯入成位元組陣列，而不是 XML 檔案。</p></td>
</tr>
<tr class="even">
<td><p><em>DBInstance</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>Lync Server 2013 常設聊天室資料庫所在之 SQL Server 執行個體的完整網域名稱及名稱。例如，下列語法會指定在伺服器 atl-sql-001.litwareinc.com 之 RTC 資料庫執行個體中所找到的資料庫：</p>
<p>-DBInstance &quot;atl-sql-001.litwareinc.com\rtc&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>所匯入之 XML 檔案的完整路徑。</p>
<p>-FileName &quot;C:\Logs\PersistentChatExport.xml&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：</p>
<p>-Report &quot;C:\Logs\PersistentChatExport.html&quot;</p>
<p>執行此 Cmdlet 時，若此檔案已存在，便會加以覆寫。</p></td>
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

無。**Import-CsPersistentChatData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。


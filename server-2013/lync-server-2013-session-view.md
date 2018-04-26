---
title: Session 檢視
TOCTitle: Session 檢視
ms:assetid: 49e33f5b-45d0-4146-a5a4-76954d895a98
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688048(v=OCS.15)
ms:contentKeyID: 49890054
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Session 檢視

 

_**上次修改主題的時間：** 2015-03-09_

「工作階段檢視」會儲存在資料庫中有記錄的工作階段的相關資訊。此檢視在 Microsoft Lync Server 2013 中引進。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ConferenceDateTime</p></td>
<td><p>日期時間</p></td>
<td><p>參考來源為 MediaLine 表格。</p></td>
</tr>
<tr class="even">
<td><p>ConferenceURI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>如果是會議則為會議 URI，如果是對等工作階段則為 DialogID。</p></td>
</tr>
<tr class="odd">
<td><p>關聯</p></td>
<td><p>varchar(max)</p></td>
<td><p>工作階段的關聯 ID。</p></td>
</tr>
<tr class="even">
<td><p>DialogCategory</p></td>
<td><p>位元</p></td>
<td><p>對話類別；0 代表 Lync Server 到中繼伺服器 Leg；1 代表中繼伺服器到 PSTN 閘道 Leg。</p></td>
</tr>
<tr class="odd">
<td><p>MediationServerBypassFlag</p></td>
<td><p>位元</p></td>
<td><p>指出通話是否經旁路處理。</p></td>
</tr>
<tr class="even">
<td><p>MediaBypassWarningFlag</p></td>
<td><p>int</p></td>
<td><p>此欄位 (若有) 指出即使旁路識別碼相符，通話為何未經旁路處理。Lync Server 只定義一個值。</p>
<p>0x0001 – 預設網路介面卡未知的旁路識別碼</p></td>
</tr>
<tr class="odd">
<td><p>StartTime</p></td>
<td><p>日期時間</p></td>
<td><p>通話開始時間。</p></td>
</tr>
<tr class="even">
<td><p>EndTime</p></td>
<td><p>日期時間</p></td>
<td><p>通話結束時間。</p></td>
</tr>
<tr class="odd">
<td><p>CallerPool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者集區 FQDN。</p></td>
</tr>
<tr class="even">
<td><p>CalleePool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者集區 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p>CallerPAI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>發話者的 P 聲稱的識別 URI 。</p></td>
</tr>
<tr class="even">
<td><p>CalleePAI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>受話者的 P 聲稱的識別 URI 。</p></td>
</tr>
<tr class="odd">
<td><p>CallerEndpoint</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者的端點名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleeEndpoint</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者的端點名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者的使用者代理程式字串。</p></td>
</tr>
<tr class="even">
<td><p>CallerUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>發話者的使用者代理程式類型。如需詳細資訊，請參閱 <a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserAgentCategory</p></td>
<td><p>nvarchar (64)</p></td>
<td><p>發話者的使用者代理程式類別。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a>。</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者的使用者代理程式字串。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>受話者的使用者代理程式類型。如需詳細資訊，請參閱 <a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserAgentCategory</p></td>
<td><p>nvarchar (64)</p></td>
<td><p>受話者的使用者代理程式類別。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CallerURI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>發話者的 URI。</p></td>
</tr>
<tr class="even">
<td><p>CalleeURI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>受話者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p>CallPrioirty</p></td>
<td><p>int</p></td>
<td><p>通話的優先順序。</p></td>
</tr>
</tbody>
</table>


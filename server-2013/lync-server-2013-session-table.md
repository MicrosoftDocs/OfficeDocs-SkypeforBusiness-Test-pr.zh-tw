---
title: Lync Server 2013：Session 表格
TOCTitle: Session 表格
ms:assetid: 7f05529c-794d-41ed-bca4-2e85b87b2dec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398635(v=OCS.15)
ms:contentKeyID: 49291464
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Session 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄都代表一個包含音訊或音訊與視訊的工作階段。其中包含該工作階段的整體資訊。工作階段定義為兩個端點之間的音訊或視訊工作階段初始通訊協定 (SIP) 對話。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>參考來源： <a href="lync-server-2013-dialog-table.md">Lync Server 2013 中的 Dialog 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>參考來源： <a href="lync-server-2013-dialog-table.md">Lync Server 2013 中的 Dialog 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceKey</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>會議金鑰。參考來源： <a href="lync-server-2013-conference-table.md">Lync Server 2013 中的 Conference 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CorrelationKey</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>關聯索引鍵。參考來源： <a href="lync-server-2013-sessioncorrelation-table.md">Lync Server 2013 中的 SessionCorrelation 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogCategory</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>對話類別；0 代表 Lync Server 到中繼伺服器 Leg；1 代表中繼伺服器到 PSTN 閘道 Leg。</p></td>
</tr>
<tr class="even">
<td><p><strong>MediationServerBypassFlag</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>指出是否略過通話的旗標。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaBypassWarningFlag</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>這個欄位 (如果有出現的話) 會說明為何某通電話未被略過，即便它符合要略過的識別碼。 Lync Server 只定義一個值。</p>
<p>0x0001 – 預設網路介面卡的未知旁路 ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>StartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>通話開始時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>通話結束時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerPool</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的集區。參考來源： <a href="lync-server-2013-pool-table.md">Lync Server 2013 中的 Pool 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleePool</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者的集區。參考來源： <a href="lync-server-2013-pool-table.md">Lync Server 2013 中的 Pool 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleePAI</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話端 SIP p-asserted identity (PAI) 中的 SIP URI。參考來源： <a href="lync-server-2013-user-table.md">Lync Server 2013 中的 User 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerURI</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的 URI。參考來源： <a href="lync-server-2013-user-table.md">Lync Server 2013 中的 User 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerEndpoint</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的端點。參考來源： <a href="lync-server-2013-endpoint-table.md">Lync Server 2013 中的 Endpoint 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerUserAgent</strong></p></td>
<td><p>bit</p></td>
<td><p>外部</p></td>
<td><p>發話者的使用者代理程式。參考來源： <a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallPriority</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>此通話的重要性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClassifiedPoorCall</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>此欄已被取代， Microsoft Lync Server 2013 已不使用。這些資訊將改為以各個媒體行的形式回報。如需詳細資訊，請參閱＜ <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerPAI</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>撥打電話之使用者的 P-Asserted-Identity。P-Asserted-Identity (PAI) 可用來傳達撥打電話之使用者真正的身分。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeEndpoint</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>接到電話的端點。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeUserAgent</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>接到電話的使用者所使用的使用者代理程式。使用者代理程式代表用戶端端點裝置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeUri</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>接到電話之使用者的 SIP URI。</p></td>
</tr>
</tbody>
</table>


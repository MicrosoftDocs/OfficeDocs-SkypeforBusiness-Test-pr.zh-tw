---
title: Lync Server 2013：ErrorReport 表格
TOCTitle: ErrorReport 表格
ms:assetid: ae0287b4-e8ca-4f8c-84ef-502897dcaa2a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412826(v=OCS.15)
ms:contentKeyID: 49292007
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ErrorReport 表格

 

_**上次修改主題的時間：** 2015-06-22_

ErrorReport 表格儲存所發生錯誤的相關資訊。每筆記錄代表發生一次錯誤。錯誤是由前端伺服器上執行的 CDR 代理程式擷取，或是從用戶端傳送。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>索引鍵/索引</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>發生錯誤的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別錯誤報告的識別碼。當和 <strong>ErrorTime</strong> 搭配使用時，可以用於找出特定的錯誤報告。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ErrorId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>錯誤報告的唯一識別碼。如需詳細資訊，請參閱 <a href="lync-server-2013-errordef-table.md">Lync Server 2013 中的 ErrorDef 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromUserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發出造成錯誤之要求的使用者。如需詳細資訊，請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToUserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>造成錯誤之要求的目的地使用者。如需詳細資訊，請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>與錯誤相關的會議 URI。如需詳細資訊，請參閱 <a href="lync-server-2013-conferenceuris-table.md">Lync Server 2013 中的 ConferenceUris 表格</a>。若 ConferenceUriId 不是 null，通常 FromUserId 或 ToUserId 其中一之將會是 null。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>外部</p></td>
<td><p>當和 <strong>SessionIdSeq</strong> 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>識別工作階段的識別碼，其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>傳送錯誤報告的伺服器 (如果報告是從伺服器元件傳送)。如需詳細資訊，請參閱 <a href="lync-server-2013-servers-table.md">Lync Server 2013 中的 Servers 表格</a>。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>ApplicationId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>傳送錯誤報告的伺服器 (如果報告是從伺服器元件傳送)。如需詳細資訊，請參閱 <a href="lync-server-2013-application-table.md">Lync Server 2013 中的應用程式表</a>。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagHeader</strong></p></td>
<td><p>影像</p></td>
<td><p> </p></td>
<td><p>錯誤的詳細資訊。</p>
<p>使用此語法可將此資料轉換為文字格式：</p>
<p><code>cast(cast(Detail as varbinary(max)) as varchar(max)) </code></p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>傳送錯誤報告之端點的用戶端版本。如需詳細資訊，請參閱 <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsCapturedByServer</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>錯誤報告由前端伺服器上執行的 CDR 代理程式所擷取，或由用戶端所傳送。</p></td>
</tr>
<tr class="even">
<td><p><strong>標幟</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>保留供未來使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>唯一識別碼，其與會議牽涉之不同元件的加入時間資訊相關聯。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>特定元件加入會議所需的時間 (以毫秒為單位)。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>代表產生錯誤報告的伺服器的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>代表產生錯誤報告所在的集區完整網域名稱。</p></td>
</tr>
</tbody>
</table>


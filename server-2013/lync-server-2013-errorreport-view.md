---
title: ErrorReport 檢視
TOCTitle: ErrorReport 檢視
ms:assetid: ca873f7e-b18b-4eaf-8db0-5f9d5a9b60a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721887(v=OCS.15)
ms:contentKeyID: 49890311
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ErrorReport 檢視

 

_**上次修改主題的時間：** 2015-03-09_

ErrorReport 檢視存放了所報告錯誤的相關資訊。每筆記錄代表發生一次錯誤。錯誤是由前端伺服器上執行的 CDR 代理程式擷取，或是從用戶端傳送。此檢視已於 Microsoft Lync Server 2013 引進使用。


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
<td><p><strong>ErrorTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>發生錯誤的時間。當和 ErrorReportSeq 搭配使用時，可以用於找出特定的錯誤。</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>用於識別錯誤的識別碼。當和 ErrorTime 搭配使用時，可以用於找出特定的錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p>錯誤報告的診斷識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>錯誤源自的使用者 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的使用者 URI 類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的使用者租用戶。如需詳細資訊，請參閱 <a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>錯誤報告的目標使用者 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤報告的目標使用者 URI 類型。如需詳細資訊，請參閱＜UriTypes 表格＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤報告的目標使用者租用戶。如需詳細資訊，請參閱 <a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>錯誤報告的目標會議 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤報告的目標會議 URI 類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>使錯誤報告產生的工作階段要求時間。當和 SessionIdSeq 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別使錯誤報告產生的工作階段要求用的識別碼。當和 SessionIdTime 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogId</strong></p></td>
<td><p>varstring(775)</p></td>
<td><p>錯誤源自的工作階段 SIP 對話方塊識別碼。格式為：</p>
<p>dialog;from-tag;to-tag</p>
<p>使用此語法可將此資料轉換為文字格式：</p>
<p>cast(cast(ExternalId as varbinary(max)) as varchar(max))</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的使用者所用的用戶端版本。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p>錯誤源自的使用者所用的用戶端。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>錯誤源自的使用者所用的用戶端類別名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>Source</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的伺服器名稱 (如果報告是從伺服器元件傳送)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Application</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的應用程式名稱 (如果報告是從伺服器元件傳送)。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p>SIP 訊息 (包含錯誤報告) 的工作階段 SIP 回應碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RequestType</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>失敗之要求的類型。</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentType</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>失敗之要求的內容類型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>工作階段的類型。如需詳細資訊，請參閱 <a href="lync-server-2013-calltype-table.md">Lync Server 2013 中的 CallType 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>唯一識別碼，其與會議牽涉之不同元件的加入時間資訊相關聯。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p>特定元件加入會議所需的時間 (以毫秒為單位)。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsCapturedByServer</strong></p></td>
<td><p>bit</p></td>
<td><p>指出錯誤報告是由前端伺服器上執行的 CDR 代理程式所擷取，還是由用戶端所傳送。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p>保留供未來使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>MsDiagHeader</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>錯誤的其他資訊。</p></td>
</tr>
</tbody>
</table>


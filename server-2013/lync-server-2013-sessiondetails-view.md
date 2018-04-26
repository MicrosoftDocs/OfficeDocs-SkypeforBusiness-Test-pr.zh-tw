---
title: SessionDetails 檢視
TOCTitle: SessionDetails 檢視
ms:assetid: ea328c6f-cf22-48dd-8f7f-f1666c9148c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721924(v=OCS.15)
ms:contentKeyID: 49890365
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# SessionDetails 檢視

 

_**上次修改主題的時間：** 2015-03-09_

SessionDetails 檢視存放了對等工作階段的相關資訊，例如 VoIP-VoIP 通話、雙方 IM 工作階段，或其他工作階段。Microsoft Lync Server 2013 採用此檢視。


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>工作階段要求的時間，會與 SessionIdSeq 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞表格。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別工作階段的識別碼，會與 SessionIdTime 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InviteTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>第一個 INVITE 要求的時間。此欄位通常是由工作階段中第一個 INVITE 訊息產生的資料填入。如果沒有 INVITE 訊息，欄位則會填入第一個相關 SIP 訊息的日期與時間 (BYE、CANCEL、MESSAGE 或 INFO)。此欄位通常是由工作階段中第一個 INVITE 訊息產生的資料填入。如果沒有 INVITE 訊息，欄位則會填入第一個相關 SIP 訊息的日期與時間 (BYE、CANCEL、MESSAGE 或 INFO)。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>啟動工作階段之使用者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>加入工作階段之使用者的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>啟動工作階段之使用者的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>加入工作階段之使用者的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromTenant</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>啟動工作階段之使用者的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>加入工作階段之使用者的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromEndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>啟動工作階段之使用者的端點唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToEndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>加入工作階段之使用者的端點唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>EndTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>工作階段的結束時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromMessageCount</strong></p></td>
<td><p>int</p></td>
<td><p>啟動工作階段之使用者所傳送的訊息數。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToMessageCount</strong></p></td>
<td><p>int</p></td>
<td><p>加入工作階段之使用者所傳送的訊息數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>啟動工作階段之使用者所使用的用戶端版本。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromClientType</strong></p></td>
<td><p>int</p></td>
<td><p>啟動工作階段之使用者所使用的用戶端。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>啟動工作階段之使用者所使用的用戶端類別名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>加入工作階段之使用者所使用的用戶端版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToClientType</strong></p></td>
<td><p>int</p></td>
<td><p>加入工作階段之使用者所使用的用戶端。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>加入工作階段之使用者所使用的用戶端類別名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TargetUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>工作階段之目標使用者的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>TargetUriType</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>工作階段之目前使用者的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnBehalfOfUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>啟動工作階段之使用者代表的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>OnnnBehalfOfUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>啟動工作階段之使用者代表的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnBehalfOfTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>啟動工作階段之使用者代表的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReferredByUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>提交工作階段之使用者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReferredByUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>提交工作階段之使用者的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReferredByTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>提交工作階段之使用者的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogId</strong></p></td>
<td><p>varchar(775)</p></td>
<td><p>SIP 對話方塊 ID。格式為：</p>
<p>dialog;from-tag;to-tag</p></td>
</tr>
<tr class="even">
<td><p><strong>CorrelationId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>要與多個工作階段相互關聯的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReplaceDialogIdTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>工作階段所取代的對話方塊時間，與 ReplaceDialogIdSeq 搭配使用，專門用於識別此工作階段所取代的對話方塊。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReplaceDialogIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別工作階段的識別碼，會與 ReplaceDialogIdTime 搭配使用，專門用於識別工作階段所取代的對話方塊。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReplacesDialogId</strong></p></td>
<td><p>varchar(775)</p></td>
<td><p>工作階段所取代的 SIP 對話方塊 ID。格式為：</p>
<p>dialog;from-tag;to-tag</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>回應第一個 INVITE 訊息的時間。此欄位通常是由工作階段中第一個 INVITE 訊息產生的資料填入。如果沒有 INVITE 訊息，欄位則會填入第一個相關 SIP 訊息的日期與時間 (BYE、CANCEL、MESSAGE 或 INFO)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p>對工作階段邀請的 SIP 回應碼。此欄位通常是由工作階段中第一個 INVITE 訊息產生的資料填入。如果沒有 INVITE 訊息，欄位則會填入第一個相關 SIP 訊息的日期與時間 (BYE、CANCEL、MESSAGE 或 INFO)。</p></td>
</tr>
<tr class="even">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p>從 SIP 標頭擷取的診斷識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ContentType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>工作階段的內容類型。</p></td>
</tr>
<tr class="even">
<td><p><strong>FrontEnd</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>擷取工作階段資料的前端伺服器 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[集區]</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>擷取工作階段資料的集區 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromEdgeServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>啟動工作階段之使用者所使用的 Edge 伺服器 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToEdgeServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>啟動工作階段之使用者所使用的 Edge 伺服器 FQDN</p></td>
</tr>
<tr class="even">
<td><p><strong>IsFromInternal</strong></p></td>
<td><p>bit</p></td>
<td><p>顯示啟動工作階段的使用者是否從內部網路登入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsToInternal</strong></p></td>
<td><p>bit</p></td>
<td><p>顯示加入工作階段的使用者是否從內部網路登入。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallPriority</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>工作階段的通話優先順序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromUserFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p>顯示啟動工作階段之使用者的屬性。下列為允許的屬性定義：</p>
<p>0x01 - 與桌上電話整合</p></td>
</tr>
<tr class="even">
<td><p><strong>ToUserFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p>顯示啟動工作階段之使用者的屬性。下列為允許的屬性定義：</p>
<p>0x01 - 與桌上電話整合</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p>顯示通話屬性。下列為允許的屬性定義：</p>
<p>0x01 - 重試的工作階段</p>
<p>0x02 - 代理程式代表回應群組所撥的通話</p></td>
</tr>
<tr class="even">
<td><p><strong>位置</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>緊急電話的位置。</p></td>
</tr>
</tbody>
</table>


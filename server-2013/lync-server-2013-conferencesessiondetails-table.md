---
title: Lync Server 2013：ConferenceSessionDetails 表格
TOCTitle: ConferenceSessionDetails 表格
ms:assetid: 9eae6a54-69fd-4966-aa17-7ecee1297ad8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412741(v=OCS.15)
ms:contentKeyID: 49291821
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ConferenceSessionDetails 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄都代表一個會議工作階段，它可以是有「焦點」的工作階段，或是特定會議伺服器的工作階段。


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>主要，外部</p></td>
<td><p>工作階段要求的時間。與 <strong>SessionIdSeq</strong> 搭配使用，來唯一識別會議工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>識別工作階段的識別碼。與 <strong>SessionIdTime</strong> 搭配使用，來唯一識別會議工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>與此工作階段相關的 Focus 會議 URI。如需詳細資訊，請參閱＜ <a href="lync-server-2013-conferenceuris-table.md">Lync Server 2013 中的 ConferenceUris 表格</a>＞。此 URI 是 Focus 會議的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConfInstance</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>可區分週期性會議的執行個體的識別碼。每個週期性會議執行個體都會有相同的 ConferenceURI 且不同的 ConfInstance 值。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="odd">
<td><p><strong>McuConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>與此工作階段相關的會議伺服器會議 URI。如需詳細資訊，請參閱＜ <a href="lync-server-2013-conferenceuris-table.md">Lync Server 2013 中的 ConferenceUris 表格</a>＞。此 URI 是會議伺服器會議的 URI。若是 Focus 會議工作階段，此欄會是 Null。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>會議工作階段中一位使用者的識別碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserEndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p></p></td>
<td><p>用來識別端點之執行個體的 GUID。例如，若一位使用者以同一帳戶登入不同機器，則每台機器都會有不同的端點識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>OnBehalfOfId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>指出來電者所代表之使用者的識別碼。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReferredById</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>轉接此通話之使用者的識別碼。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>會議使用者所使用的用戶端版本。如需詳細資訊，請參閱＜ <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConfClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>會議伺服器所使用的用戶端版本。如需詳細資訊，請參閱＜ <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReplaceDialogIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>外部</p></td>
<td><p>用來識別目前工作階段所取代之對話的識別碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReplaceDialogIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>用來識別工作階段的識別碼。其會與 <strong>ReplacesDialogIdTime</strong> 搭配使用，專門用於識別此工作階段所取代的工作階段。請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsStartedByConfServer</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>表示工作階段是否由會議伺服器所啟動。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsEndedByConfServer</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>表示工作階段是否由會議伺服器所終止。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsUserInternal</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>使用者是否由內部登入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>工作階段邀請的工作階段初始通訊協定 (SIP) 回應碼。此欄位一般會填入工作階段中的初始 INVITE 訊息所產生的資料。如果沒有 INVITE 訊息，則此欄位將填入第一個相關聯 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>從 SIP 標頭擷取而來的診斷識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>用於此工作階段之前端伺服器的識別碼。請參閱 <a href="lync-server-2013-servers-table.md">Lync Server 2013 中的 Servers 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>擷取工作階段之集區的識別碼。請參閱 <a href="lync-server-2013-pools-table.md">Lync Server 2013 中的 Pools 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話正在使用的中繼伺服器。如需詳細資訊，請參閱 <a href="lync-server-2013-mediationservers-table.md">Lync Server 2013 中的 MediationServers 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>GatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話正在使用的閘道。如需詳細資訊，請參閱＜ <a href="lync-server-2013-gateways-table.md">Lync Server 2013 中的 Gateways 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話正在使用的 Edge Server。如需詳細資訊，請參閱 <a href="lync-server-2013-edgeservers-table.md">Lync Server 2013 中的 EdgeServers 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>工作階段中所使用的內容類型。請參閱 <a href="lync-server-2013-contenttypes-table.md">Lync Server 2013 中的 ContentTypes 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InviteTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>第一個 INVITE 要求的時間。此欄位一般會填入工作階段中的初始 INVITE 訊息所產生的資料。如果沒有 INVITE 訊息，則此欄位將填入第一個相關聯 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>第一個 SIP RESPONSE 的時間。此欄位一般會填入工作階段中的初始 INVITE 訊息所產生的資料。如果沒有 INVITE 訊息，則此欄位將填入第一個相關聯 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期和時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>工作階段結束的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>UriTypeId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>外部</p></td>
<td><p>包含 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>中的 MCU URI 類型值。此欄位用於改善查詢效能。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>指出使用者屬性的位元設定。下列是屬性的定義：</p>
<ul>
<li><p>已與桌上電話整合 - 1</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>CallFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>指出通話屬性的位元設定。下列是屬性的定義：</p>
<ul>
<li><p>重試的工作階段 - 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


\* 大部分工作階段的 SessionIdSeq 值皆會是 1。如有多個工作階段的啟動時間完全相同，將只有一個工作階段的 SessionIdSeq 值會是 1，其餘工作階段皆是 2，依此類推。


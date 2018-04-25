---
title: Lync Server 2013：SessionDetails 表格
TOCTitle: SessionDetails 表格
ms:assetid: 783d2508-e31f-4b54-be0c-63aa5ec21c04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398589(v=OCS.15)
ms:contentKeyID: 49291378
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SessionDetails 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表一個對等工作階段，可以是 VoIP 對 VoIP 電話、雙方 IM 工作階段或其他工作階段類型。您可以聯結 [Lync Server 2013 中的媒體資料表格](lync-server-2013-media-table.md)執行表格，以尋找此工作階段中每個相關媒體的詳細資料。

請注意，IsUser1IntegratedWithDeskPhone 和 IsUser2IntegratedWithDeskPhone 欄位已從 Microsoft Lync Server 2013 中所使用的 SessionDetails 表格上捨棄。


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
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>工作階段要求的時間，會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>用來識別工作階段的識別碼。其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。*請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CorrelationId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p></p></td>
<td><p>與多個工作階段相互關聯的 GUID。</p></td>
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
<td><p><strong>User1Id</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>工作階段中某位使用者的識別碼。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>，以取得更多詳細資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>User2Id</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>工作階段中其他使用者的識別碼。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>，以取得更多詳細資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>User1EndpointId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>識別工作階段中第一位使用者所使用之端點的 GUID。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="odd">
<td><p><strong>User2EndpointId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>識別工作階段中第二位使用者所使用之端點的 GUID。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>TargetUserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>SIP 要求中原始的目標使用者 URI。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>，以取得更多詳細資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionStartedById</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>起始工作階段之使用者的識別碼。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>，以取得更多詳細資訊。</p></td>
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
<td><p><strong>ServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>用於此工作階段之前端伺服器的識別碼。請參閱 <a href="lync-server-2013-servers-table.md">Lync Server 2013 中的 Servers 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>擷取工作階段之集區的識別碼。請參閱 <a href="lync-server-2013-pools-table.md">Lync Server 2013 中的 Pools 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentTypeID</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>工作階段中所使用的內容類型。請參閱 <a href="lync-server-2013-contenttypes-table.md">Lync Server 2013 中的 ContentTypes 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>User1ClientVerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用者1 所使用的用戶端版本。請參閱 <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>User2ClientVerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用者2 所使用的用戶端版本。請參閱 <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>User1EdgeServerid</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用者 1 所使用的 Edge Server。請參閱 <a href="lync-server-2013-edgeservers-table.md">Lync Server 2013 中的 EdgeServers 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>User2EdgeServerid</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用者 2 所使用的 Edge Server。請參閱 <a href="lync-server-2013-edgeservers-table.md">Lync Server 2013 中的 EdgeServers 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsUser1Internal</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>使用者 1 是否由內部登入。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsUser2Internal</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>使用者 2 是否由內部登入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InviteTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>第一個 INVITE 要求的時間。此欄位通常會使用從工作階段之初始 INVITE 訊息中產生的資料來填入。如果沒有 INVITE 訊息，則會使用第一個相關 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期與時間來填入。此欄位通常會使用從工作階段之初始 INVITE 訊息中產生的資料來填入。如果沒有 INVITE 訊息，則會使用第一個相關 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期與時間來填入。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>回應第一個 INVITE 訊息的時間。此欄位通常會使用從工作階段之初始 INVITE 訊息中產生的資料來填入。如果沒有 INVITE 訊息，則會使用第一個相關 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期與時間來填入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>對工作階段邀請的 SIP 回應碼。此欄位通常是由工作階段中第一個 INVITE 訊息產生的資料填入。如果沒有 INVITE 訊息，欄位則會填入第一個相關 SIP 訊息的日期與時間 (BYE、CANCEL、MESSAGE 或 INFO)。</p></td>
</tr>
<tr class="even">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>從 SIP 標頭擷取而來的診斷識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallPriority</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話優先順序。請參閱 <a href="lync-server-2013-callpriorities-table.md">Lync Server 2013 中的 CallPriorities 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>User1MessageCount</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>工作階段期間使用者 1 所傳送的訊息數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>User2MessageCount</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>工作階段期間使用者 2 所傳送的訊息數。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>工作階段結束的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaTypes</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指出此工作階段之媒體類型的位元集。下列為類型的定義：</p>
<h3 id="section-1"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>IM</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>FILE_TRANSFER</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>REMOTE_ASSISTANCE</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p>APP_SHARING</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>AUDIO</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>VIDEO</p></td>
<td><p>32</p></td>
</tr>
<tr class="odd">
<td><p>APP_INVITE</p></td>
<td><p>64</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p><strong>User1Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>指出使用者 1 屬性的位元集。下列是屬性的定義：</p>
<ul>
<li><p>0x01 - 與桌上電話整合</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>User2Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>指出使用者 2 屬性的位元集。下列是屬性的定義：</p>
<ul>
<li><p>0x01 - 與桌上電話整合</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>CallFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>指出通話屬性的位元設定。下列是屬性的定義：</p>
<ul>
<li><p>0x01 - 重試的工作階段</p></li>
<li><p>0x02 - 由代理人代替回應群組撥出的通話</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Processed</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>供監控服務內部使用。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>


\* 大部分工作階段的 SessionIdSeq 值皆會是 1。如有多個工作階段的啟動時間完全相同，將只有一個工作階段的 SessionIdSeq 值會是 1，其餘工作階段皆是 2，依此類推。


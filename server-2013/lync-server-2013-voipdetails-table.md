---
title: Lync Server 2013：VoipDetails 表格
TOCTitle: VoipDetails 表格
ms:assetid: 74ffbb71-569b-4018-be1f-4db2bbafcf36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398566(v=OCS.15)
ms:contentKeyID: 49291346
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 VoipDetails 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表一通雙方通話，其中至少一位使用者為 VoIP 使用者。


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
<td><p>主要</p></td>
<td><p>工作階段要求的時間，會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別工作階段的識別碼，其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromNumberId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的 <strong>PhoneId</strong> 。請參閱 <a href="lync-server-2013-phones-table.md">Lync Server 2013 中的 Phones 表格</a> 以取得更多資訊。若非 NULL，且 <strong>FromGatewayId</strong> 亦非 NULL，代表發話者為 PSTN 使用者。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConnectedNumberId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者的 <strong>PhoneId</strong> 。請參閱 <a href="lync-server-2013-phones-table.md">Lync Server 2013 中的 Phones 表格</a> 以取得更多資訊。若非 NULL，且 <strong>ToGatewayId</strong> 亦非 NULL，代表受話者為 PSTN 使用者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromMediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話的來源中繼伺服器。請參閱 <a href="lync-server-2013-mediationservers-table.md">Lync Server 2013 中的 MediationServers 表格</a> 以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToMediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話的目標中繼伺服器。請參閱 <a href="lync-server-2013-mediationservers-table.md">Lync Server 2013 中的 MediationServers 表格</a> 以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromGatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話的來源閘道。請參閱 <a href="lync-server-2013-gateways-table.md">Lync Server 2013 中的 Gateways 表格</a> 以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToGatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話的目標閘道。請參閱 <a href="lync-server-2013-gateways-table.md">Lync Server 2013 中的 Gateways 表格</a> 以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisconnectedbyURIId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>中斷通話之使用者的 URI (若該使用者有 URI 的話)。請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a> 以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>DisconnectedbyPhoneId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>中斷通話之電話的識別碼 (若通話是從電話所中斷的話)。請參閱 <a href="lync-server-2013-phones-table.md">Lync Server 2013 中的 Phones 表格</a> 以取得更多資訊。</p></td>
</tr>
</tbody>
</table>


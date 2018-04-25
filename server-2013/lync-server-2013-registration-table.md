---
title: Lync Server 2013：登錄表格
TOCTitle: 登錄表格
ms:assetid: 05ff9dd3-1aaa-4af0-bd69-8789fb8eaeb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398114(v=OCS.15)
ms:contentKeyID: 49289970
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的登錄表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄都代表一個使用者註冊事件。


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
<td><p>識別工作階段的識別碼，其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用者識別碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>EndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p></p></td>
<td><p>識別註冊端點的 GUID。通常，來自相同使用者電腦的註冊事件會具備相同的端點識別碼，不同的機器則會有不同的端點識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndpointEra</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>用於區分相同使用者和相同端點相關之登錄的識別碼。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>目前使用者的用戶端版本。如需詳細資訊，請參閱＜ <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RegistrarId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>登錄伺服器用於登錄的識別碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-servers-table.md">Lync Server 2013 中的 Servers 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>擷取工作階段之集區的識別碼。請參閱 <a href="lync-server-2013-pools-table.md">Lync Server 2013 中的 Pools 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeServerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>登錄通過的 Edge Server。如需詳細資訊，請參閱＜ <a href="lync-server-2013-edgeservers-table.md">Lync Server 2013 中的 EdgeServers 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsInternal</strong></p></td>
<td><p>位元</p></td>
<td><p></p></td>
<td><p>使用者是否從內部登入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsUserServiceAvailable</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>UserService 是否可供使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsPrimaryRegistrar</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>是否登錄至主要登錄器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsPrimaryRegistrarCentral</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>表示是否使用 Survivable Branch Appliance 登錄使用者。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>RegisterTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>登錄時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeRegisterTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>解除登錄時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>回應碼</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>登錄要求的回應碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>登錄要求的診斷識別碼。這會指出診斷資訊類型。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>登錄要求的來源裝置。如需詳細資訊，請參閱＜ <a href="lync-server-2013-devices-table.md">Lync Server 2013 中的 Devices 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeRegisterTypeId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>外部</p></td>
<td><p>解除登錄的原因，例如「由用戶端起始」、「註冊到期」或「用戶端失敗」等。如需詳細資訊，請參閱＜ <a href="lync-server-2013-deregistertype-table.md">Lync Server 2013 中的 DeRegisterType 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>IPAddress</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>使用者登錄所使用的端點 IP 位址。可以是 IPv4 位址或 IPv6 位址。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>


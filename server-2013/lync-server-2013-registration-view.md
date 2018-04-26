---
title: Registration 檢視
TOCTitle: Registration 檢視
ms:assetid: 8a42bc7d-3d4f-43c1-9e15-89b2ee419ade
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688120(v=OCS.15)
ms:contentKeyID: 49890192
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Registration 檢視

 

_**上次修改主題的時間：** 2015-03-09_

註冊檢視儲存關於使用者註冊的資訊。此檢視由 Lync Server 2013 提供。


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
<td><p>工作階段要求的時間。當和 SessionIdSeq 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別工作階段的識別碼。當和 SessionIdTime 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RegisterTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>進行註冊的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>註冊的使用者 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>註冊的使用者 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>註冊的使用者承租人。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>使用者的端點註冊使用的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>EndpointEra</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>將涉及相同使用者及相同端點的註冊相區隔所用的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeRegisterType</strong></p></td>
<td><p>日期時間</p></td>
<td><p>進行取消註冊的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeRegisterReason</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>取消註冊的原因。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>註冊的使用者所用的用戶端版本。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p>註冊的使用者所用的用戶端。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>註冊的使用者所用的用戶端類別。</p></td>
</tr>
<tr class="even">
<td><p><strong>IpAddress</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>使用者註冊所用的 IP 位址。這可能是 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogId</strong></p></td>
<td><p>varstring(775)</p></td>
<td><p>SIP 對話方塊 ID。格式為：</p>
<p>dialog;from-tag;to-tag</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p>SIP 對工作階段邀請的回應碼。此欄位一般會填入工作階段中的初始 INVITE 訊息所產生的資料。如果沒有 INVITE 訊息，則此欄位將填入第一個相關聯 SIP 訊息 (BYE、CANCEL、MESSAGE 或 INFO) 的日期和時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p>從 SIP 標頭擷取而來的診斷識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>Registrar</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>登錄器的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>擷取工作階段資料的集區 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>註冊的使用者所用的 Edge Server FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsInternal</strong></p></td>
<td><p>bit</p></td>
<td><p>指出使用者是否從內部網路登入。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsUserServiceAvailable</strong></p></td>
<td><p>bit</p></td>
<td><p>指出註冊時是否可使用 UserService。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsPrimaryRegistrar</strong></p></td>
<td><p>bit</p></td>
<td><p>指出是否向主要登錄器註冊。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceMacAddress</strong></p></td>
<td><p>bigint</p></td>
<td><p>註冊裝置的 MAC 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceManufacturer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>註冊裝置的製造商。如需詳細資訊，請參閱＜<a href="lync-server-2013-manufacturers-table.md">Lync Server 2013 中的 Manufacturers 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceHardwareVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>註冊裝置的硬體版本。如需詳細資訊，請參閱＜<a href="lync-server-2013-hardwareversions-table.md">Lync Server 2013 中的 HardwareVersions 表格</a>＞。</p></td>
</tr>
</tbody>
</table>


---
title: VoIPDetails 檢視
TOCTitle: VoIPDetails 檢視
ms:assetid: 14c44736-71ba-4fc5-82c7-1df65bf6261c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687973(v=OCS.15)
ms:contentKeyID: 49889953
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# VoIPDetails 檢視

 

_**上次修改主題的時間：** 2015-03-09_

VoIPDetails 檢視會儲存對等工作階段的相關資訊，其中至少有一個使用者是 VoIP 使用者。Microsoft Lync Server 2013 中即引入了此檢視。

> [!NOTE]  
> VoIPDetails 檢視包含＜<a href="lync-server-2013-sessiondetails-view.md">SessionDetails 檢視</a>＞中的所有欄，以及下列所示的欄。




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
<td><p><strong>FromPhone</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>起始工作階段之使用者的電話 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToPhone</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>參加工作階段之使用者的電話 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisconnectedByUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>中斷連線工作階段之使用者的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>DisconnectedByUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>中斷連線工作階段之使用者的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisconnectedByTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>中斷連線工作階段之使用者的租用戶。</p></td>
</tr>
<tr class="even">
<td><p><strong>DisconnectedByPhone</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>中斷連線工作階段之使用者的電話 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromMediationServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>起始工作階段之使用者所使用的中繼伺服器。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToMediationServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>參加工作階段之使用者所使用的中繼伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromGateway</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>起始工作階段之使用者所使用的閘道。</p></td>
</tr>
<tr class="even">
<td><p><strong>ToGateway</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>參加工作階段之使用者所使用的閘道。</p></td>
</tr>
</tbody>
</table>


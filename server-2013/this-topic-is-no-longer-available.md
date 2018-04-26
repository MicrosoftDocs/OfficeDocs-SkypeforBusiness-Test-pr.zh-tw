---
title: DNS 摘要 - Public Instant Messaging 連線
TOCTitle: DNS 摘要 - Public Instant Messaging 連線
ms:assetid: ddf42a25-5ac4-4643-a10a-9fbd433fc2d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618375(v=OCS.15)
ms:contentKeyID: 49292551
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# DNS 摘要 - Public Instant Messaging 連線

 

_**上次修改主題的時間：** 2015-03-09_

設定適用於公用立即訊息連線的網域名稱系統 (DNS) 時，您會發現支援外部使用者的設定將支援公用 IM 連線。如果您已經設定 Edge Server 或 Edge 集區，則必須有 DNS 記錄才能支援公用 IM 連線。

## DNS 摘要 – 公用立即訊息連線


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>位置/類型/連接埠</th>
<th>FQDN/DNS 記錄</th>
<th>IP 位址/FQDN</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Access Edge Service 介面</p></td>
<td><p>Access Edge Service 外部介面 (Contoso)。必要時，重複用於含有啟用 Lync 之使用者的所有 SIP 網域。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)


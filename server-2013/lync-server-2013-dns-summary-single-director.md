---
title: Lync Server 2013：DNS 摘要 - 單一 Director
TOCTitle: DNS 摘要 - 單一 Director
ms:assetid: 790ecb56-92cd-41f4-baf6-c290a707aa4d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205021(v=OCS.15)
ms:contentKeyID: 49291392
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 單一 Director

 

_**上次修改主題的時間：** 2015-03-09_

下表包含 DNS 記錄摘要，需要有這類記錄才能支援單一 Director。 Director 的記錄需要有類似的 DNS 記錄做為 前端伺服器。所需的記錄數會反映於 Director 憑證上所需的主體替代名稱中。不同於 前端伺服器， Director 不會裝載使用者帳戶或裝載行動服務。

### Director 所需的 DNS 記錄

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
<td><p>內部 DNS/A</p></td>
<td><p>dir01.contoso.net</p></td>
<td><p>Director</p></td>
<td><p>複寫和伺服器對伺服器適用的 Director 主機記錄</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Director</p></td>
<td><p>來自 Edge Server 之內部 Edge 介面的輸入工作階段初始通訊協定 (SIP)</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS/A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>Director</p></td>
<td><p>從反向 Proxy 發行的 Dialin Web 服務</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>Director</p></td>
<td><p>從反向 Proxy 發行的會議 Web 服務</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS/A</p></td>
<td><p>webdirexternal.contoso.com</p></td>
<td><p>Director</p></td>
<td><p>透過 Director 適用的反向 Proxy Web 票證外部 Web 服務來發行和定義</p></td>
</tr>
</tbody>
</table>


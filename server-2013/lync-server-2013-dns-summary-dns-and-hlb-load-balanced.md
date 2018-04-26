---
title: Lync Server 2013：DNS 摘要 - DNS 與 HLB 負載平衡
TOCTitle: DNS 摘要 - DNS 與 HLB 負載平衡
ms:assetid: d2132695-1956-4190-a98e-cd7255cbded6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205273(v=OCS.15)
ms:contentKeyID: 49292397
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - DNS 與 HLB 負載平衡

 

_**上次修改主題的時間：** 2015-03-09_

下表包含支援 DNS 負載平衡與硬體負載平衡 Director 所需的 DNS 記錄摘要。 Director 的角色需要和 前端伺服器類似的 DNS 記錄。需要的記錄數目會反映在 Director 憑證上所需的主體替代名稱。和 前端伺服器不同， Director 集區 不會裝載使用者帳戶，或是裝載 Mobility Services。

### 使用 DNS 負載平衡與硬體負載平衡器的 Director 集區所需的 DNS 記錄

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
<td><p>dirpool01.contoso.net</p></td>
<td><p>Director 集區</p></td>
<td><p>伺服器對伺服器適用的 DNS 負載平衡 Director 集區主機記錄</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Director 集區</p></td>
<td><p>Edge Server 內部介面的輸入工作階段初始通訊協定 (SIP)</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>Director 集區 HLB VIP</p></td>
<td><p>硬體負載平衡、發行來自反向 Proxy 的 dialin Web 服務</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS/A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>Director 集區 HLB VIP</p></td>
<td><p>硬體負載平衡、發行來自反向 Proxy 的 meet Web 服務</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>webdirexternal.contoso.com</p></td>
<td><p>Director 集區 HLB VIP</p></td>
<td><p>Director 集區的 Web 票證外部 Web 服務由反向 Proxy 硬體負載平衡、發行和定義</p></td>
</tr>
</tbody>
</table>


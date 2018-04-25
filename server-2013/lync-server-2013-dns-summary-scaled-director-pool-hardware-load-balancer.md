---
title: Lync Server 2013：DNS 摘要 - 調整式 Director 集區 (硬體負載平衡器)
TOCTitle: DNS 摘要 - 調整式 Director 集區 (硬體負載平衡器)
ms:assetid: 08ba48e6-bfa1-4ab0-bc89-d58ddb9c20af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204655(v=OCS.15)
ms:contentKeyID: 49290015
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 調整式 Director 集區 (硬體負載平衡器)

 

_**上次修改主題的時間：** 2015-03-09_

下表包含支援硬體負載平衡 Director 所需之 DNS 記錄的摘要。 Director 角色需要與 前端伺服器類似的 DNS 記錄。所需的記錄數目會反映在 Director 憑證上所需的主體別名中。與 前端伺服器不同的是， Director 集區不主控使用者帳戶或主控 Mobility Services。

### 使用硬體負載平衡器和 DNS 負載平衡之 Director 集區所需的 DNS 記錄

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
<td><p>用於複寫及伺服器對伺服器通訊的 Director 主機記錄</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>dirpool01.contoso.net</p></td>
<td><p>Director 集區 HLB VIP</p></td>
<td><p>DNS 負載平衡 Director 集區的主機記錄</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Director 集區 HLB VIP</p></td>
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
<td><p>反向 Proxy Web 票證外部 Web 服務為 Director 集區發行及定義的硬體負載平衡</p></td>
</tr>
</tbody>
</table>


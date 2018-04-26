---
title: Lync Server 2013：Edge 元件支援的伺服器組合
TOCTitle: Edge 元件支援的伺服器組合
ms:assetid: 435c4dd8-36af-4b71-9b88-3ffcf0fc5c65
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425934(v=OCS.15)
ms:contentKeyID: 49290750
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Edge 元件支援的伺服器組合

 

_**上次修改主題的時間：** 2012-09-08_

Access Edge Service、Web Conferencing Edge Service 和 A/V Edge Service 組合都在 Edge Server。下列伺服器提供外部使用者存取所需的各項功能，而且必須部署在專用伺服器：

  - Edge Server

  - Director (選擇性)

  - 反向 Proxy

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 不需要有專門的反向 Proxy。例如，您可以提供服務以發佈 Lync Server Web 服務，並同時為其他無須負擔 Lync Server 的網站提供已發佈的網站。 若您在周邊網路中已經擁有反向 Proxy 可支援其他服務，您可以將它用於 Lync Server 2013。</td>
</tr>
</tbody>
</table>


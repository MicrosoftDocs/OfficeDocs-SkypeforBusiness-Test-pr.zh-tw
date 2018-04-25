---
title: 連接埠摘要 -  可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
TOCTitle: 連接埠摘要 -  可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
ms:assetid: 62e98fab-7add-4983-a3fa-dbe74e1c3849
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618371(v=OCS.15)
ms:contentKeyID: 49291107
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 連接埠摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟

 

_**上次修改主題的時間：** 2015-03-09_

針對部署於 Edge Server 之 Extensible Messaging and Presence Protocol (XMPP) Proxy 定義的連接埠及通訊協定，允許 XMPP 同盟協力廠商通訊至 Edge Server，也允許 Edge Server 通訊至 XMPP 同盟協力廠商。在對內防火牆中也定義從前端伺服器或前端集區至 Edge Server 或 Edge 集區的規則。

## Extensible Messaging and Presence Protocol 的防火牆摘要


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 (IP 位址)</th>
<th>目的地 (IP 位址)</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XMPP/TCP/5269</p></td>
<td><p>任何</p></td>
<td><p>Access Edge Service 介面 IP 位址</p></td>
<td><p>XMPP 的標準伺服器對伺服器通訊連接埠。允許進行從同盟 XMPP 協力廠商至 Edge Server XMPP Proxy 的通訊</p></td>
</tr>
<tr class="even">
<td><p>XMPP/TCP/5269</p></td>
<td><p>Access Edge Service 介面 IP 位址</p></td>
<td><p>任何</p></td>
<td><p>XMPP 的標準伺服器對伺服器通訊連接埠。允許進行從 Edge Server XMPP Proxy 至同盟 XMPP 協力廠商的通訊</p></td>
</tr>
<tr class="odd">
<td><p>XMPP/MTLS/23456</p></td>
<td><p>任何</p></td>
<td><p>內部 Edge Server 介面 IP</p></td>
<td><p>從前端伺服器或前端集區上的 XMPP 閘道至 Edge Server 的內部 XMPP 流量</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[Lync Server 2013 中的範例 XMPP 設定 – XMPP 與 Google Talk 的同盟](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### 其他資源

[在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)


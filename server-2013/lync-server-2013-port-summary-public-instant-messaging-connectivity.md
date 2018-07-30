---
title: 連接埠摘要 - Public Instant Messaging 連線
TOCTitle: 連接埠摘要 - Public Instant Messaging 連線
ms:assetid: f46756ec-1401-4ca2-a4a4-5cd28bcfdc7f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618376(v=OCS.15)
ms:contentKeyID: 49292809
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 連接埠摘要 - Public Instant Messaging 連線

 

_**上次修改主題的時間：** 2015-03-09_

如要設定支援公用立即訊息連線的必要連接埠與通訊協定防火牆，您應注意到 SIP/MTLS/TCP 5061 是雙向，會同時影響公用 IM 提供者的連絡人連絡 Lync 用戶端或 Lync 連絡公用 IM 連絡人的功能。

Windows Live Messenger 可加入與 Lync 用戶端之間的音訊/視訊通訊。這表示連接埠與通訊協定防火牆的設定，與支持 Lync 為外部使用者時的一般防火牆設定非常相似。

> [!IMPORTANT]
> 更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard Client Access License (CAL) 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。<br />
> 與 Messenger 用戶端的合約將在 2013 年 3 月 15 日正式終止 (中國大陸除外)。之前使用 Messenger 的同盟使用者，將由 Skype 取代為同盟用戶端。


## 防火牆摘要 – 公用即時訊息連線


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>角色/通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 IP 位址</th>
<th>目的地 IP 位址</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>公共 IM 連線夥伴</p></td>
<td><p>Edge Server 存取介面</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線。</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Edge Server 存取介面</p></td>
<td><p>公共 IM 連線夥伴</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線。</p></td>
</tr>
<tr class="odd">
<td><p>存取/SIP(TLS)/TCP/443</p></td>
<td><p>用戶端</p></td>
<td><p>Edge Server 存取介面</p></td>
<td><p>供外部使用者存取的用戶端對伺服器 SIP 流量。</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>Edge Server 存取介面</p></td>
<td><p>Live Messenger 用戶端</p></td>
<td><p>如果設定的是公共 IM 連線，則用於 Windows Live Messenger 的 A/V 工作階段。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Edge Server 存取介面</p></td>
<td><p>Live Messenger 用戶端</p></td>
<td><p>Windows Live Messenger 的公用 IM 連線必須使用。</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Live Messenger 用戶端</p></td>
<td><p>Edge Server 存取介面</p></td>
<td><p>Windows Live Messenger 的公用 IM 連線必須使用。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)  
[決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)


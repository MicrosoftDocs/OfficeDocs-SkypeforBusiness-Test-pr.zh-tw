---
title: Lync Server 2013：設定媒體旁路
TOCTitle: 設定媒體旁路
ms:assetid: f50a7a13-c6a0-48f1-bee1-e45fa2b2f9b8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413028(v=OCS.15)
ms:contentKeyID: 49292822
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定媒體旁路

 

_**上次修改主題的時間：** 2013-02-24_

本節假設您已發佈且設定至少一部或多部中繼伺服器 (分別如部署文件中的＜ [在 Lync Server 2013 的拓撲產生器中定義中繼伺服器](lync-server-2013-define-a-mediation-server-in-topology-builder.md)＞及＜ [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)＞，或＜ [在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md)＞及＜ [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)＞所述)。

本節也會假設您至少已定義一個閘道對等實體來提供 PSTN 連線，如[在 Lync Server 2013 中於拓撲產生器內定義閘道](lync-server-2013-define-a-gateway-in-topology-builder.md)中所述。如果您連接的對等實體為 SIP 主幹連線提供者的 SBC，請確定該提供者為合格的提供者，而且該提供者支援媒體旁路。例如，許多 SIP 主幹連線提供者只允許其 SBC 接收來自中繼伺服器的流量。若是如此，就不得啟用所述主幹的旁路。另外，除非您的組織對 SIP 主幹連線提供者透露內部網路 IP 位址，否則您無法啟用媒體旁路。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>媒體旁路不會與每個 PSTN 閘道、IP-PBX 以及 SBC 相互溝通。Microsoft 已經與認證的合作夥伴測試了一組 PSTN 閘道和 SBC，並用 Cisco IP-PBX 完成部分測試。只有列在 Unified Communications Open Interoperability Program – Lync Server 中的產品和版本支援媒體旁路，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=214406">http://go.microsoft.com/fwlink/p/?linkId=214406</a>。</td>
</tr>
</tbody>
</table>


本節說明如何啟用媒體旁路來減少中繼伺服器所需進行的處理。在您啟用媒體旁路前，請確定您的環境符合支援媒體旁路所需的條件，如規劃文件中的[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)所述。另外，務必使用[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)中的資訊決定是否啟用媒體旁路全域設定以便永遠略過中繼伺服器，或是使用網站和區域資訊決定是否略過中繼伺服器。

如果您已選擇性地設定通話許可控制 (CAC) (這是另一項進階的 Enterprise Voice 功能)，請注意，通話許可控制所執行的頻寬保留不會套用至採用媒體旁路的任何通話。首先會驗證是否採用媒體旁路，如果採用媒體旁路，就不會針對該通話使用通話許可控制；只有在媒體旁路檢查失敗時，才會檢查通話許可控制。因此，在任何路由傳送至 PSTN 的通話上，這兩項功能會互斥。這種邏輯是因為媒體旁路假設通話的媒體端點之間不存在頻寬限制；媒體旁路無法在頻寬受限制的連結上執行。因此，下列其中一項會套用至 PSTN 通話：a) 媒體略過中繼伺服器，而且通話許可控制不會為通話保留頻寬；或者 b) 通話許可控制對通話套用頻寬保留，而媒體會由通話中內含的中繼伺服器處理。

## 後續步驟：在主幹連線上啟用媒體旁路

完成 PSTN 連線的初始設定 (撥號對應表、語音原則、PSTN 使用方式記錄、撥出電話路由和轉譯規則) 後，使用[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)中的步驟開始進行啟用媒體旁路的程序。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[在 Lync Server 2013 中設定媒體旁路以一律略過中繼伺服器](lync-server-2013-configure-media-bypass-to-always-bypass-the-mediation-server.md)  
[在 Lync Server 2013 中設定媒體旁路全域設定以使用網站和區域資訊](lync-server-2013-configure-media-bypass-global-settings-to-use-site-and-region-information.md)  

#### 概念

[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)  

#### 其他資源

[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)


---
title: 監控伺服器記憶體容量限制
TOCTitle: 監控伺服器記憶體容量限制
ms:assetid: 1697ea71-6fcf-480d-b4e9-cd79f94d247e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh689982(v=OCS.15)
ms:contentKeyID: 49290204
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 監控伺服器記憶體容量限制

 

_**上次修改主題的時間：** 2013-02-16_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題中涉及容量規劃的資訊僅與 Lync 2010 Mobile 用戶端和 Mobility Service (Mcx) 有關。針對整合通訊 Web API (UCWA) 的容量規劃 (用於 Lync 2013 Mobile 用戶端) 是由 Lync Server 2013 規劃工具所提供。</td>
</tr>
</tbody>
</table>


兩個行動效能計數器可協助您確定目前使用量，並有助於規劃 Lync Server 2013 Mobility Service (Mcx) 的容量，還可監控 UCWA 的記憶體使用量。對於 UCWA，計數器類別為 \[LS:WEB – UCWA\]。對於行動服務 (Mcx)，計數器的類別為 \[LS:WEB - Mobile Communication Service\]。要監控的計數器為︰

  - \[Currently Active Session Count with Active Presence Subscriptions\]，這是透過 UCWA 或 Mobility Service (Mcx) 登錄，含有使用中目前狀態訂閱的目前端點數 (自動連線的行動使用者數)

  - \[Currently Active Session Count\]，這是透過 UCWA 或 Mobility Service 登錄的目前端點數

在一段時間過後，如果 \[Currently Active Session Count with Active Presence Subscriptions\] 與 \[Currently Active Session Count\] 之間的差異不大，則表示大部分行動裝置使用者都有自動連線裝置，例如 Android 或 Nokia 行動裝置 (僅限 Mcx)。(UCWA 自動連線裝置包括執行 Lync 2013 Mobile 用戶端的 Apple 和 Android 裝置。) 如果 \[Currently Active Session Count\] 比 \[Currently Active Session Count with Active Presence Subscriptions\] 高很多，則表示有較多使用者使用背景端點裝置，如 Mcx 下的 Apple iOS 裝置或 Windows Phone。(Windows Phone 是唯一會登錄為 Lync 2013 Mobile 用戶端的裝置。)

您應依據所預期的使用狀況、容量規劃結果，以及 Mobility Service 和其他前端伺服器計數器的持續監控，設定 \[Currently Active Session Count with Active Presence Subscriptions\] 與 \[Currently Active Session Count\] 的限制。所設定的限制應該可以讓您評估伺服器容量，並且在超出容量時發出警示。

若要確定適當的限制，您需要先確定前端伺服器上有多少記憶體可用於 Mobility Service。請監控計數器，根據下列公式來判斷需要規劃額外容量的時機：

Mobility Service (Mcx) 使用的總記憶體 (MB) = 164 + (400 + 134) / 1024 \* \[Currently Active Session Count with Active Presence Subscriptions\] + 400 / 1024 \* (\[Currently Active Session Count\] – \[Currently Active Session Count with Active Presence Subscriptions\])

> [!IMPORTANT]  
> Microsoft Lync Server 2010 Capacity Calculator 試算表已預先填入可讓規劃人員確定伺服器需求 (包括 CPU、記憶體和硬碟) 的所有公式。您可下載該試算表和相關文件，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=212657" class="uri">http://go.microsoft.com/fwlink/?linkid=212657</a>。



前端伺服器需要足夠的可用記憶體，才能在容錯移轉的狀況中支援 Mobility Service。您可以使用 \[Memory\\Available Mbytes\] 計數器來監控前端伺服器上目前可用的記憶體，或是使用上述方程式來規劃您預期 Mobility Service 會使用的記憶體數量。

當您規劃預期的行動使用者數量時，如果前端伺服器上的可用的記憶體數量低於 1,500 MB，則需要增加更多的硬體來支援 Mobility Service。如需詳細資訊，請參閱作業文件中的＜[在 Lync Server 2013 中針對效能監控行動性](lync-server-2013-monitoring-mobility-for-performance.md)＞。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中針對效能監控行動性](lync-server-2013-monitoring-mobility-for-performance.md)


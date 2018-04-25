---
title: 監控 Mobility Service 與 UCWA 使用方式
TOCTitle: 監控 Mobility Service 與 UCWA 使用方式
ms:assetid: 8389b37a-ca3e-4047-8b51-85bc07da87e8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690025(v=OCS.15)
ms:contentKeyID: 49291511
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 監控 Mobility Service 與 UCWA 使用方式

 

_**上次修改主題的時間：** 2013-02-14_

您應持續監控 Lync Server Mobility Service (Mcx) 與 Unified Communications Web API (UCWA) 所使用的 CPU 和記憶體。若要監控使用量，您可以使用下列項目：

**對於 Unified Communications Web API (UCWA)：**

  - Internet Information Services (IIS) 管理員中的 **LyncUcwa** 工作者處理序。在 \[工作者處理序\] 窗格中，查看 \[CPU %\] 和 \[私用位元組 (KB)\] (記憶體) 欄。

  - \[CPU\] 和 \[Processor\] 效能計數器。

針對大部分部署，UCWA CPU 使用量平均應低於 15%。記憶體使用量應落在＜[監控伺服器記憶體容量限制](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)＞描述的限制內。

除了 CPU 和記憶體使用量計數器，您也可以使用下列效能計數器來協助判斷伺服器何時超載要求：

  - **LS:WEB – Throttling and Authentication\\WEB – Total Requests in Processing**，指出伺服器上的擱置 Web 要求數。當此計數器達到 10,000 時，後續的要求將會失敗，並出現「503 – 服務無法使用」錯誤訊息。

  - **ASP.NET\\Requests Queued** (應該永遠為零)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果達到或超過這些值，應該重新造訪並重新計算容量規劃的正確 CPU 大小、核心數，以及主控 Web 服務的電腦記憶體。</td>
</tr>
</tbody>
</table>


**對於 Mobility Service (Mcx)：**

  - Internet Information Services (IIS) 管理員 中的 **CSIntMcxAppPool** 和 **CSExtMcxAppPool** 工作者處理序。在 \[工作者處理序\] 窗格中，查看 \[CPU %\] 和 \[私用位元組 (KB)\] (記憶體) 欄。

  - \[CPU\] 和 \[Processor\] 效能計數器。

針對大部分部署，Mobility Service CPU 使用量平均應低於 15%。記憶體使用量應落在＜[監控伺服器記憶體容量限制](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)＞描述的限制內。

除了 CPU 和記憶體使用量計數器，您也可以使用下列 ASP.NET 效能計數器來協助判斷伺服器何時超載要求：

  - **ASP.NET v2.0.50727\\Requests Current**，指出伺服器上的擱置 Web 要求數。當此計數器達到 5,000 時，後續的要求將會失敗，並出現「503 – 服務無法使用」錯誤訊息。

  - **ASP.NET\\Requests Queued** (應該永遠為零)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果達到或超過這些值，應該重新造訪並重新計算容量規劃的正確 CPU 大小、核心數，以及主控 Web 服務的電腦記憶體。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[監控伺服器記憶體容量限制](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)


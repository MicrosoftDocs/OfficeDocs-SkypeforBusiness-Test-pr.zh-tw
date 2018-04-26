---
title: Lync Server 2013：連接埠摘要 - 調整式 Director 集區 (硬體負載平衡器)
TOCTitle: 連接埠摘要 - 調整式 Director 集區 (硬體負載平衡器)
ms:assetid: 6ae2f4ac-5b64-4e45-8253-133308f5812d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204983(v=OCS.15)
ms:contentKeyID: 49291219
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 調整式 Director 集區 (硬體負載平衡器)

 

_**上次修改主題的時間：** 2015-03-09_

Director 集區的防火牆連接埠需求是由連接埠所組成，這些連接埠是用來從 Edge Server 的內部介面或從反向 Proxy 的向內介面建立與 Director 的通訊。根據預設， Microsoft Lync Server 2013 預期連接埠 HTTP/TCP 8080 和 HTTPS/TCP 4443 會從反向 Proxy 開放至 Director，以及 前端集區和 前端伺服器。另外，也一定會有從 Edge Server 內部介面至 Director 和至 前端集區及 前端伺服器的工作階段初始通訊協定 (SIP) 通訊。SIP 通訊協定使用從 Edge Server 至 前端集區和 前端伺服器的 SIP/MTLS/TCP 5061。您也必須建立規則，以用來進行從 Director、 前端集區和 前端伺服器至 Edge Server 內部介面的 SIP/MTLS/TCP 5061 通訊。

### 適用於防火牆的 Director 連接埠和通訊協定定義

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
<td><p>HTTP/TCP 8080</p></td>
<td><p>反向 Proxy 內部介面</p></td>
<td><p>Director 硬體負載平衡器 VIP</p></td>
<td><p>通訊一開始會由反向 Proxy 的外部端接收，並傳送至 Director HLB VIP 和 前端伺服器 Web 服務上</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP 4443</p></td>
<td><p>反向 Proxy 內部介面</p></td>
<td><p>Director 硬體負載平衡器 VIP</p></td>
<td><p>通訊一開始會由反向 Proxy 的外部端接收，並傳送至 Director HLB VIP 和 前端伺服器 Web 服務上</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 444</p></td>
<td><p>Director</p></td>
<td><p>前端伺服器 或 前端集區</p></td>
<td><p>Director HLB VIP 和 前端伺服器之間的伺服器間通訊</p></td>
</tr>
<tr class="even">
<td><p>HTTP/TCP 80</p></td>
<td><p>內部用戶端</p></td>
<td><p>Director 硬體負載平衡器 VIP</p></td>
<td><p>Director 提供 Web 服務給內部與外部用戶端。</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 443</p></td>
<td><p>內部用戶端</p></td>
<td><p>Director 硬體負載平衡器 VIP</p></td>
<td><p>Director 提供 Web 服務給內部與外部用戶端。</p></td>
</tr>
<tr class="even">
<td><p>SIP/MTLS/TCP 5061</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>Director 硬體負載平衡器 VIP</p></td>
<td><p>從 Edge Server 至 Director 和 前端伺服器的 SIP 通訊。</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50001</p></td>
<td><p>任何一個</p></td>
<td><p>Director</p></td>
<td><p>集中記錄服務控制器 (ClsController.exe) 或代理 (ClsAgent.exe) 命令與記錄收集</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50002</p></td>
<td><p>任何一個</p></td>
<td><p>Director</p></td>
<td><p>集中記錄服務控制器 (ClsController.exe) 或代理 (ClsAgent.exe) 命令與記錄收集</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50003</p></td>
<td><p>任何一個</p></td>
<td><p>Director</p></td>
<td><p>集中記錄服務控制器 (ClsController.exe) 或代理 (ClsAgent.exe) 命令與記錄收集</p></td>
</tr>
</tbody>
</table>


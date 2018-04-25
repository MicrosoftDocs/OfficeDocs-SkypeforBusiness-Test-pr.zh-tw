---
title: Lync Server 2013：連接埠摘要 - DNS 與 HLB 負載平衡
TOCTitle: 連接埠摘要 - DNS 與 HLB 負載平衡
ms:assetid: b07c37e4-820e-46ee-a678-1da95d1b87af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205179(v=OCS.15)
ms:contentKeyID: 49292016
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - DNS 與 HLB 負載平衡

 

_**上次修改主題的時間：** 2015-03-09_

單一 Director 的防火牆連接埠需求包含數個連接埠，這些連接埠用來從反向 Proxy 的內部介面或向內網路建立與 Director 的通訊。依預設， Microsoft Lync Server 2013 會預期從反向 Proxy 開啟連接埠 HTTP/TCP 8080 與 HTTPS/TCP 4443 以連接至 Director，還有 前端集區和 前端伺服器，此外，從 Edge Server 內部介面到 Director 與到 前端集區與 前端伺服器，必須有工作階段初始通訊協定 (SIP) 通訊。SIP 通訊協定使用 SIP/MTLS/TCP 5061 從 Edge Server 到 前端集區與 前端伺服器。同時也必須建立允許從 Director、 前端集區與 前端伺服器到 Edge Server 內部介面的 SIP/MTLS/TCP 5061 通訊的規則。

### 防火牆定義的單一 Director 連接埠與通訊協定

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
<td><p>一開始由反向 Proxy 的外部端接收，通訊會傳送到 Director HLB VIP 與 前端伺服器 Web 服務。</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP 4443</p></td>
<td><p>反向 Proxy 內部介面</p></td>
<td><p>Director 硬體負載平衡器 VIP</p></td>
<td><p>一開始由反向 Proxy 的外部端接收，通訊會傳送到 Director HLB VIP 與 前端伺服器 Web 服務。</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 444</p></td>
<td><p>Director</p></td>
<td><p>前端集區 或 前端伺服器</p></td>
<td><p>Director HLB VIP 與 前端伺服器或 前端伺服器之間的伺服器內通訊。</p></td>
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
<td><p>Director</p></td>
<td><p>從 Edge Server 到 Director 的 SIP 通訊，以及 前端伺服器。</p></td>
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


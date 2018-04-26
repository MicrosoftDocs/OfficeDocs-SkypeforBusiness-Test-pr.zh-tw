---
title: Lync Server 2013：連接埠摘要 - 單一 Director
TOCTitle: 連接埠摘要 - 單一 Director
ms:assetid: 079c1414-723f-4499-b7d4-a0d7121c1626
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204648(v=OCS.15)
ms:contentKeyID: 49289995
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 單一 Director

 

_**上次修改主題的時間：** 2015-03-09_

單一 Director 的防火牆連接埠需求，包含從反向 Proxy 內部介面或內部對向網路來建立與 Director 通訊所使用的連接埠。 Microsoft Lync Server 2013 預設會開啟連接埠 HTTP/TCP 8080 和 HTTPS/TCP 4443，以從反向 Proxy 連線至 Director 以及 前端集區和 前端伺服器。此外，從 Edge Server 內部介面到 Director 以及 前端集區和 前端伺服器，必須使用工作階段初始通訊協定 (SIP) 通訊。SIP 通訊協定使用 SIP/MTLS/TCP 5061 從 Edge Server 連線至 前端集區和 前端伺服器。您也必須建立規則，以允許從 Director、 前端集區和 前端伺服器到 Edge Server 內部介面的 SIP/MTLS/TCP 5061 通訊。

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
<td><p>Director</p></td>
<td><p>先由反向 Proxy 的外部端接收，再將通訊傳送至 Director 和 前端伺服器 Web 服務</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP 4443</p></td>
<td><p>反向 Proxy 內部介面</p></td>
<td><p>Director</p></td>
<td><p>先由反向 Proxy 的外部端接收，再將通訊傳送至 Director 和 前端伺服器 Web 服務</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 444</p></td>
<td><p>Director</p></td>
<td><p>前端伺服器或前端集區</p></td>
<td><p>Director 和 前端伺服器之間的伺服器間通訊</p></td>
</tr>
<tr class="even">
<td><p>HTTP/TCP 80</p></td>
<td><p>內部用戶端</p></td>
<td><p>Director Web 服務</p></td>
<td><p>Director 提供內部和外部用戶端 Web 服務。</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 443</p></td>
<td><p>內部用戶端</p></td>
<td><p>Director Web 服務</p></td>
<td><p>Director 提供內部和外部用戶端 Web 服務。</p></td>
</tr>
<tr class="even">
<td><p>SIP/MTLS/TCP 5061</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>Director</p></td>
<td><p>從 Edge Server 到 Director 以及 前端伺服器的 SIP 通訊。</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50001</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>集中記錄服務控制站 (ClsController.exe) 或代理程式 (ClasAgent.exe) 命令和記錄檔收集</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50002</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>集中記錄服務控制站 (ClsController.exe) 或代理程式 (ClasAgent.exe) 命令和記錄檔收集</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50003</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>集中記錄服務控制站 (ClsController.exe) 或代理程式 (ClasAgent.exe) 命令和記錄檔收集</p></td>
</tr>
</tbody>
</table>


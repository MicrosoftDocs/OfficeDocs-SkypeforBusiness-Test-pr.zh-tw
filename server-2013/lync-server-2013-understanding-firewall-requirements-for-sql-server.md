---
title: Lync Server 2013：瞭解 SQL Server 的防火牆需求
TOCTitle: 瞭解 SQL Server 的防火牆需求
ms:assetid: 31d7df2c-589f-465e-be74-cf6767db190d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425818(v=OCS.15)
ms:contentKeyID: 49290515
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 瞭解與 Lync Server 2013 搭配使用時之 SQL Server 的防火牆需求

 

_**上次修改主題的時間：** 2015-03-09_

進行 Standard Edition 部署時，會在 Lync Server 2013 安裝期間自動建立防火牆例外。但在進行 Enterprise Edition 部署時，則必須以手動方式在 SQL Server 後端伺服器上設定防火牆例外。根據 TCP/IP 通訊協定，一個連接埠一次只能供一個 IP 位址使用。也就是說，對於 SQL Server 型伺服器，您可以為預設的資料庫執行個體指派預設的 TCP 連接埠 1433。對於任何其他執行個體，您都必須使用 \[SQL Server 組態管理員\] 指派唯一而未使用的連接埠。本主題將說明：

  - 使用預設執行個體時的防火牆例外需求

  - SQL Server Browser 服務的防火牆例外需求

  - 使用具名執行個體時的靜態聆聽連接埠需求

## 使用預設執行個體時的防火牆例外需求

如果您在部署 Lync Server 2013 時為任何資料庫使用了 SQL Server 預設執行個體，則需要使用下列防火牆規則，以協助確保前端集區能夠與 SQL Server 預設執行個體進行通訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定</th>
<th>[Port] (連接埠)</th>
<th>方向</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP</p></td>
<td><p>1433</p></td>
<td><p>輸入至 SQL Server</p></td>
</tr>
</tbody>
</table>


## SQL Server Browser 服務的防火牆例外需求

SQL Server Browser 服務會尋找資料庫執行個體，然後與執行個體 (具名或預設) 依設定要使用的連接埠進行通訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定</th>
<th>[Port] (連接埠)</th>
<th>方向</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UDP</p></td>
<td><p>1434</p></td>
<td><p>Inbound</p></td>
</tr>
</tbody>
</table>


## 使用具名執行個體時的靜態聆聽連接埠需求

在 SQL Server 設定中針對支援 Lync Server 2013 的資料庫使用具名執行個體時，您應使用 \[SQL Server 組態管理員\] 設定靜態連接埠。在指派靜態連接埠給每個具名執行個體後，您應在防火牆中為每個靜態連接埠建立例外。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定</th>
<th>[Port] (連接埠)</th>
<th>方向</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP</p></td>
<td><p>靜態定義</p></td>
<td><p>Inbound</p></td>
</tr>
</tbody>
</table>


## SQL Server 文件

Microsoft SQL Server 2012 文件提供如何設定資料庫的防火牆存取之詳細指示。如需 Microsoft SQL Server 2012 的詳細資訊，請參閱＜設定 Windows 防火牆以允許 SQL Server 存取＞，網址為 [http://go.microsoft.com/fwlink/?linkid=218031\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=218031%26clcid=0x404)。


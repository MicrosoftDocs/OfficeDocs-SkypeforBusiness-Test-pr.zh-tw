---
title: Standard Edition Server 部署中的 Lync Server 2013 伺服器組合
TOCTitle: Standard Edition Server 部署中的伺服器組合
ms:assetid: 0763ffab-4fd6-463a-8e62-d97876b376d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398131(v=OCS.15)
ms:contentKeyID: 49289992
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Standard Edition Server 部署中 Lync Server 2013 的伺服器組合

 

_**上次修改主題的時間：** 2013-01-20_

本節說明您可以在 Lync Server 2013 Standard Edition Server 部署中組合的伺服器角色、資料庫以及檔案共用。

## 伺服器角色

在 Lync Server 2013 中，音訊/視訊會議服務、中繼服務、監控及封存可以組合在 Standard Edition Server 上，但是需要其他設定才能啟用這些服務。您可以選擇在其他伺服器上部署中繼服務。

您可以將信任的應用程式伺服器與 Standard Edition Server 組合在一起。

下列伺服器角色必須分別部署到個別的電腦上：

  - Director

  - Edge Server

  - 中繼伺服器 (如果未與 Standard Edition Server 組合在一起)

  - Office Web Apps Server

## 資料庫

根據預設，SQL Server Express 後端資料庫會在 Standard Edition Server 組合。您無法將它移至其他電腦。除了一個例外狀況外，您無法在 Standard Edition Server 上組合其他資料庫。如果您選擇在 Standard Edition Server 上部署 常設聊天室伺服器，您可以在相同的 Standard Edition Server 上組合常設聊天室資料庫和常設聊天室規範資料庫。

您可以在單一資料庫伺服器中組合下列每一個資料庫：

  - 監控資料庫

  - 封存資料庫

  - Enterprise Edition 前端集區的後端資料庫

您可以在單一 SQL 執行個體上組合任何或全部的資料庫，或者讓每一個資料庫使用個別的 SQL 執行個體，不過有下列限制：

  - 每個 SQL 執行個體僅能包含一個後端資料庫 (用於 Enterprise Edition 前端集區)、一個監控資料庫、一個封存資料庫、一個常設聊天室資料庫，以及一個常設聊天室規範資料庫。

  - 資料庫伺服器不支援一個以上的 Enterprise Edition 前端集區、執行封存的伺服器、執行監控的伺服器、 常設聊天室資料庫以及 常設聊天室規範資料庫，但是每種可支援一個，而不論資料庫是否使用相同的 SQL Server 執行個體或個別的 SQL Server 執行個體。

您可以如本節後面所述，將檔案共用與資料庫組合在一起。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Lync Server 2013 中，您可以選擇為部署中的某些或所有使用者，整合監控和封存存放區與 Exchange 2013 存放區。您無法在與 Exchange 存放區所在的相同伺服器上，部署任何執行 Lync Server 或元件的伺服器。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然支援資料庫的組合，但是資料庫大小可能會快速增加。例如，當您考慮將封存資料庫與其他資料庫組合在一起時，請注意，如果您要封存較多使用者的訊息，封存資料庫所需的磁碟空間可能會變得極大。因此，不建議組合多個資料庫，特別是將封存資料庫、 常設聊天室資料庫及 常設聊天室規範資料庫，與 Enterprise Pool 的後端資料庫組合在一起。</td>
</tr>
</tbody>
</table>


## 檔案共用

檔案共用可以是個別的伺服器，或是在相同的伺服器上組合為下列任何一種或所有情況：

  - 資料庫伺服器，包括 Enterprise Edition 前端集區的後端伺服器

  - 封存資料庫

  - 監控資料庫

  - 常設聊天室資料庫

  - 常設聊天室規範資料庫

單一檔案共用可以用於多個前端集區、Standard Edition Server (全部在同一個網站中)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Lync Server 2013 中，監控和封存使用 Lync Server 檔案共用作為 Standard Edition Server。</td>
</tr>
</tbody>
</table>


## 其他元件

如果您想使用任何 Lync Server 2013 伺服器角色來支援同盟使用者的 Web 內容共用，則您無法組合不是 Lync Server 2013 元件但卻是部署時所需的反向 Proxy 伺服器。不過，您可以在用於其他應用程式之組織的現有反向 Proxy 伺服器上設定支援，即可為 Lync Server 2013 部署實作反向 Proxy 支援。

您無法將任何 Exchange UM 元件或 SharePoint 元件與任何 Lync Server 2013 角色組合在一起。


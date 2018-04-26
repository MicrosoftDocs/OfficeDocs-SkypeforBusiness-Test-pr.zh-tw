---
title: Lync Server 2013：封存的元件與拓撲
TOCTitle: 封存的元件與拓撲
ms:assetid: 5893063d-a44a-4034-aba9-cbe883ecf710
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204916(v=OCS.15)
ms:contentKeyID: 49290984
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中封存的元件與拓撲

 

_**上次修改主題的時間：** 2012-10-09_

如果要封存 Lync Server 2013 IM 和會議內容，您可以在 Lync Server 中實作封存。

## 封存元件

封存功能包括下列元件：

  - **封存代理程式**。封存代理程式 (亦稱為整合資料收集代理程式) 會自動安裝在每個前端集區和 Standard Edition Server 上並啟動。儘管封存代理程式會自動啟動，但在啟用封存並進行適當設定之前，還是不會實際擷取任何訊息。

  - **封存資料存放區**。適用於 Lync Server 2013 的資料存放區可以是下列其中一項：
    
      - Exchange 2013 存放區。如果您啟用 Microsoft Exchange 整合選項，位於 Exchange 2013 伺服器的使用者信箱便可使用 Exchange 2013 存放區來存放封存的資料，但是唯有當信箱設為 \[就地保留\] 才適用。
    
      - SQL Server 存放區。如果您在部署中的使用者位於 Lync Server 2013 上，則可設定執行支援之 SQL Server 版本的封存資料庫，以針對這些使用者啟用封存。

封存也會要求檔案存放區，但封存會使用與前端伺服器或 Standard Edition Server 相同的檔案存放區。

如需適用於封存的硬體和軟體需求清單，請參閱支援文件中的 [Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)和 [Lync Server 2013 中的伺服器軟體和基礎結構支援](lync-server-2013-server-software-and-infrastructure-support.md)。

## 支援的拓撲

您在每個使用者要求支援封存的集區中部署封存。封存會在 Enterprise Edition 集區的 前端伺服器上和 Standard Edition 伺服器上執行。封存資料存放區可以是下列項目：

  - 與 Exchange 2013 存放區整合

  - 使用個別的 SQL Server 資料庫進行部署

如果您的 Exchange 2013 部署未包含 Lync Server 部署中的所有使用者，則您必須針對信箱位於 Exchange 2013 伺服器上的使用者，使用 Microsoft Exchange 整合，而且必須針對所有其他 Lync 使用者部署個別 SQL Server 資料庫來用於封存。

## 支援的組合

Lync Server 2013 支援各種組合案例：如果是小型組織，可讓您彈性地在一部伺服器上執行多個元件來節省硬體成本；如果是需要延展性和效能的大型組織，可以在不同的伺服器上執行個別的元件。當您決定是否要組合元件之前，請務必考慮延展性因素。

封存是部署於集區的 前端伺服器或 Standard Edition 伺服器上。如需有關可在該處組合之元件的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md)。

如果您針對封存使用個別的 SQL Server 資料庫，來替代存放區與 Exchange 2013 存放區的整合，或者在執行這項作業之外，您還可以將封存資料庫與下列任一項進行組合：

  - 監控資料庫

  - Enterprise Edition 前端集區的後端資料庫

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>裝載封存資料庫的伺服器可以裝載其他資料庫。不過，當您考慮將封存資料庫與其他資料庫組合時，請注意，如果您要封存較多使用者的訊息，封存資料庫所需的磁碟空間可能會變得極大。基於這項因素，建議您不要將封存資料庫與後端資料庫整合。</td>
</tr>
</tbody>
</table>


如果您將封存資料庫與監控資料庫、後端資料庫 (或兩者) 組合在一起，即可將單一 SQL 執行個體使用於任一或所有資料庫；或者，您可以將個別 SQL 執行個體使用於每一個資料庫，但具有以下限制：

  - 每個 SQL 執行個體僅能包含單一後端資料庫、單一監控資料庫和單一封存資料庫。

如需有關所有伺服器角色和資料庫組合的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md)。


---
title: Lync Server 2013：新封存功能
TOCTitle: 新封存功能
ms:assetid: c002e367-41ad-498d-9d23-8b117ac435b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205225(v=OCS.15)
ms:contentKeyID: 49292187
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的新封存功能

 

_**上次修改主題的時間：** 2012-10-09_

Lync Server 2013 的封存功能可以封存下列類型的內容：

  - 對等立即訊息

  - 使用多方立即訊息的會議

  - 會議內容，包括上傳的內容 (例如，講義) 和事件相關內容 (例如，加入、離開、上傳共用，以及可見度變更)

此外， Lync Server 2013 的封存功能也提供新功能來提升部署和操作效率，這些新功能包括：

  - **將封存共置於前端伺服器上。**Lync Server 2013 沒有獨立的封存伺服器角色。在 Enterprise Edition 部署中，封存是所有前端伺服器上都有的選用功能，而在 Standard Edition Server 上，這可透過為集區或網站進行設定來實作。

  - **Microsoft Exchange 整合。**當您部署封存時，可為所有隸屬於 Exchange 2013 並將信箱設為「就地保留」的使用者，將封存的資料儲存區與現有的 Exchange 2013 儲存區整合，如此您就無須另行部署 SQL Server 資料庫來封存 Lync 資料。如果您沒有 Exchange 2013 部署、不想與其整合，或是有 Lync 2013 使用者不隸屬於 Exchange 2013 並將信箱設為就地保留，則可使用 SQL Server 部署獨立的封存資料庫，以儲存來自 Lync 通訊的封存資料。如果您想讓位於部署中的部分使用者 (而非全部使用者) 使用 Microsoft Exchange 整合，可以同時使用 Microsoft Exchange 整合和 Lync Server 2013 封存資料庫。如需就地保留的詳細資訊，請參閱位於 [http://go.microsoft.com/fwlink/?linkid=267500\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267500%26clcid=0x404) 的＜就地保留＞(可能為英文網頁)。

  - **SQL 存放區鏡像。**當您部署封存時，可以為封存資料庫啟用 SQL Server 資料庫鏡像。

  - **白板與投票的封存。**封存的會議內容現在包括會議期間分享的白板與投票。

不會封存下列類型的內容：

  - 對等檔案傳輸

  - 對等立即訊息和會議的音訊/視訊

  - 對等立即訊息與會議的應用程式共用

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)


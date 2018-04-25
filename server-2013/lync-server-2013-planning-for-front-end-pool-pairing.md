---
title: Lync Server 2013：規劃前端集區配對
TOCTitle: 規劃前端集區配對
ms:assetid: cca5773d-57ff-45ce-a7b4-f82ae697c477
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205293(v=OCS.15)
ms:contentKeyID: 49292347
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃前端集區配對

 

_**上次修改主題的時間：** 2012-09-28_

若要在 Lync Server 2013 中得到最佳的災難復原功能，請在地理上不同的兩個網站部署前端集區配對。每個網站包含一個前端集區，該集區與另一個網站的對應前端集區為一對。兩個網站都在作用中，且 Lync Server 備份服務提供即時的資料複寫，以維持集區同步。備份服務是 Lync Server 2013 中專為支援災難復原解決方案而設計的新功能。當您將前端集區與另一個前端集區相配對時，它會安裝在該集區上。

如果一個網站的集區失敗，您可以將使用者從該集區容錯移轉到另一個網站的集區，另一個網站的集區便會提供服務給這兩個集區的所有使用者。進行容量規劃時，應該將每個集區都設計為能在發生災害時，處理兩個集區中所有使用者的工作負載。

## 本節內容

  - [Lync Server 2013 之支援的集區配對選項與最佳作法](lync-server-2013-supported-pool-pairing-options-and-best-practices.md)

  - [Lync Server 2013 中的備份登錄器關聯](lync-server-2013-backup-registrar-relationships.md)

  - [Lync Server 2013 中的集區容錯回復與集區容錯移轉的復原時間](lync-server-2013-recovery-time-for-pool-failover-and-pool-failback.md)

  - [Lync Server 2013 中的中央管理存放區容錯移轉](lync-server-2013-central-management-store-failover.md)

  - [Lync Server 2013 中前端集區配對資料安全性](lync-server-2013-front-end-pool-pairing-data-security.md)


---
title: Lync Server 2013 支援的集區配對選項與最佳作法
TOCTitle: 支援的集區配對選項與最佳作法
ms:assetid: 142caf34-0f20-47f3-9d32-ce25ab622fad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204697(v=OCS.15)
ms:contentKeyID: 49290176
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 之支援的集區配對選項與最佳作法

 

_**上次修改主題的時間：** 2013-02-19_

將要包含與彼此配對之前端集區的兩個資料中心之間，並沒有距離的限制。建議您在相同的地區設定中使用兩個資料中心，彼此以高速連結。兩個資料中心最好分隔得夠遠，以避免單一災害同時衝擊到兩個資料中心。

擁有跨地理區域的兩個資料中心是可行的，但是可能會因為資料複寫延遲，而導致資料遺失的風險較高。

在規劃要將哪些集區配對時，請謹記，系統只支援下列配對：

  - Enterprise Edition 集區只能與其他 Enterprise Edition 集區配對。同樣地，Standard Edition 集區只能與其他 Standard Edition 集區配對。

  - 實體集區只能與其他實體集區配對。同樣地，虛擬集區只能與其他虛擬集區配對。

拓撲產生器或拓撲驗證都不會禁止以非建議的方式來將兩個集區配對。例如，拓撲產生器可讓您將 Enterprise Edition 集區與 Standard Edition 集區配對。不過，系統並不支援這些配對類型。

配對中的每個集區都有在發生災害時，從這兩個集區服務所有使用者的能力。

如果您將 Enterprise Edition 集區配對，也可以在後端伺服器上實作高可用性，但若是 Standard Edition 集區配對，就只有災害復原措施可用。


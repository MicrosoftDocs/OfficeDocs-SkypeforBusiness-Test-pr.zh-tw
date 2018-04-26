---
title: 在 Lync Server 2013 中將子網路與 CAC 上的網站關聯
TOCTitle: 在 Lync Server 2013 中將子網路與 CAC 上的網站關聯
ms:assetid: a749c9b3-15f3-4e74-9f43-1507d3c2c940
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412786(v=OCS.15)
ms:contentKeyID: 49291923
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將子網路與 CAC 上的網站關聯

 

_**上次修改主題的時間：** 2012-10-20_

網路中的每個子網路都必須與特定網路網站關聯。這是因為我們需要子網路資訊來判斷端點所在的網路網站。如果知道某工作階段中雙方的位置，通話許可控制 (CAC) 就能判斷是否有足夠的頻寬可以建立通話。

通話許可控制在將子網路與網路網站產生關聯方面，並沒有任何特殊需求。若要在拓撲中建立子網路與網路網站的關聯，請遵循[在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)中的步驟進行。若要檢視通話許可控制的範例網路拓撲中的網站 (及其個別子網路)，請參閱規劃文件中的[範例：在 Lync Server 2013 中收集通話許可控制服務需求](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)。


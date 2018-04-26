---
title: 從集區中移除前端伺服器
TOCTitle: 從集區中移除前端伺服器
ms:assetid: 767225c9-7c0b-4d54-a407-d77134ba2abe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688095(v=OCS.15)
ms:contentKeyID: 49890119
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從集區中移除前端伺服器

 

_**上次修改主題的時間：** 2012-10-04_

Microsoft Lync Server 2010 Enterprise Edition 前端伺服器無法存在作為獨立的電腦。即使在集區內只有單一電腦，它仍必須定義為 前端集區。

本主題將引導您逐步完成從現有的 前端集區完成移除個別 前端伺服器的流程。如果 前端伺服器為集區內最後一個伺服器，或者如果您正在完全移除該集區，請參閱＜ [移除前端集區或 Standard Edition Server](remove-front-end-pool-or-standard-edition-server.md)＞。移除 前端集區之前，無需移除個別 前端伺服器。當您移除該集區時，您將移除每一個 前端伺服器。

## 從集區移除前端伺服器

1.  開啟 Lync Server 2013 前端伺服器，再開啟拓撲建置器。

2.  瀏覽至 Lync Server 2010 節點。

3.  展開 **\[Enterprise Edition 前端集區\]** ，然後展開具有您希望移除 前端伺服器的 前端集區，在您想移除的 前端伺服器上按一下滑鼠右鍵，然後按一下 **\[刪除\]** 。


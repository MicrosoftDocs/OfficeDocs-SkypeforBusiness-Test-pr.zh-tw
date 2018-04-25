---
title: Lync Server 2013：變更與前端集區相關聯的 Edge 集區
TOCTitle: 變更與前端集區相關聯的 Edge 集區
ms:assetid: 369468c7-2c0b-48cc-bbc3-825dad7b85aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688023(v=OCS.15)
ms:contentKeyID: 49890022
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中變更與前端集區相關聯的 Edge 集區

 

_**上次修改主題的時間：** 2012-09-21_

如果 Edge 集區失效但相同網站上的前端集區仍在執行，您將需要設定前端集區來使用其他網站上的 Edge 集區，直到失敗的 Edge 集區還原為止。

## 變更與前端集區相關聯的 Edge 集區

1.  在拓撲產生器中，瀏覽至您需要變更的前端集區名稱。

2.  以滑鼠右鍵按一下集區，然後按一下 \[編輯屬性\] 。

3.  在 **\[關聯\]** 區段的 **\[關聯 Edge 集區 (適用於媒體元件)\]** 下方，使用下拉式方塊來選取您要與此前端集區產生關聯的 Edge 集區。

4.  按一下 \[確定\] 。

## 請參閱

#### 概念

[Lync Server 2013 中的 Edge Server 災害復原](lync-server-2013-edge-server-disaster-recovery.md)


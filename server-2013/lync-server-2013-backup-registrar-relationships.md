---
title: Lync Server 2013 備份登錄器關聯
TOCTitle: 備份登錄器關聯
ms:assetid: 7e078271-84b9-4666-989c-c4507a0cdf4a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205033(v=OCS.15)
ms:contentKeyID: 49291447
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的備份登錄器關聯

 

_**上次修改主題的時間：** 2012-06-28_

除了提供災害復原能力之外，兩個配對的集區也可作為彼此的備份登錄器。在 Lync Server 2013 中， 前端集區之間的備份登錄器關係始終保持 1:1，而且相互對等。這表示，如果 P1 是 P2 的備份，則 P2 必須是 P1 的備份，而且兩者之中的任一個不可成為其他任何前端集區的備份。這是 Lync Server 2010 的變更，原先 前端集區備份關係可以是多對一。

即使兩個 前端集區之間的備份關係必須是 1:1，而且相互對等，但各個 前端集區仍然可以成為任何數量 Survivable Branch Appliance 的備份登錄器，這一點與 Lync Server 2010 相同。

請注意， Lync Server 2013 不會將災害復原支援延伸到 Survivable Branch Appliance 上的使用者。如果作為 Survivable Branch Appliance 備份的前端集區停止運作，登入 Survivable Branch Appliance 的使用者將進入恢復模式，即使前端集區上的使用者容錯移轉到備份 前端集區 後，也會進入恢復模式。


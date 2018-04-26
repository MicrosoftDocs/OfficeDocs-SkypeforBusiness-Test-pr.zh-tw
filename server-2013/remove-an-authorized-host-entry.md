---
title: 移除已獲授權的主機項目
TOCTitle: 移除已獲授權的主機項目
ms:assetid: 56a04140-347e-4eef-bede-0e858534f71e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204902(v=OCS.15)
ms:contentKeyID: 49290968
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除已獲授權的主機項目

 

_**上次修改主題的時間：** 2012-09-26_

本主題說明如何移除舊有授權主機項目 (在 Lync Server 2013 中稱為「信任的應用程式項目」 )。當您將遠端呼叫控制移轉到 Lync Server 2013 部署時，在 Office Communications Server 2007 R2 部署中必須移除所有 SIP/CSTA 閘道的現有授權主機項目。您必須使用 Office Communications Server 2007 R2 隨附的管理工具，移除現有的授權主機項目。

## 在 Office Communications Server 2007 R2 部署中移除授權的主機項目

1.  開啟 Office Communications Server 2007 R2 系統管理主控台。

2.  展開樹狀結構，並且以滑鼠右鍵按一下授權主機建立所在的集區。

3.  按一下 **\[屬性\]** ，再按一下 \[前端屬性\] 。

4.  按一下 **\[主機授權\]** 索引標籤。

5.  選取伺服器，然後按一下 **\[移除\]** 。

6.  在 **\[屬性\]** 中，按一下 **\[確定\]** 。


---
title: 還原 Lync Server 集區
TOCTitle: 還原 Lync Server 集區
ms:assetid: 6fe80fb3-38ad-4931-a07b-1763b61aa448
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202176(v=OCS.15)
ms:contentKeyID: 52056150
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原 Lync Server 集區

 

_**上次修改主題的時間：** 2013-02-18_

您的 Lync Server 部署可能包含下列類型的集區：

  - 前端伺服器

  - 中繼伺服器

  - 常設聊天室伺服器

  - Edge Server

如果整個集區遭受中斷，請遵循程序來還原集區中的每部成員伺服器。

  - 若為前端集區，請先還原後端伺服器，再還原每部前端伺服器。如需詳細資訊，請參閱＜[還原 Enterprise Edition 後端伺服器](lync-server-2013-restoring-an-enterprise-edition-back-end-server.md)＞和＜[還原 Enterprise Edition 成員伺服器](lync-server-2013-restoring-an-enterprise-edition-member-server.md)＞。

  - 若是所有其他類型的集區，則請還原每個成員伺服器。如需詳細資訊，請參閱＜[還原 Enterprise Edition 成員伺服器](lync-server-2013-restoring-an-enterprise-edition-member-server.md)＞。


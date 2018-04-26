---
title: 設定要監控的 Lync Server 電腦
TOCTitle: 設定要監控的 Lync Server 電腦
ms:assetid: 9f1b2b91-d5af-42ad-a27d-b0815f762ad8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205118(v=OCS.15)
ms:contentKeyID: 49291843
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定要監控的 Lync Server 電腦

 

_**上次修改主題的時間：** 2012-10-20_

因為 Lync Server 2013 未使用 Microsoft Lync Server 2010 中使用的集中探索程序，所以您要監控的每部 Lync Server 2013 電腦都必須能夠自行對管理伺服器回報其存在。若要達到此目的，您必須在要監控的每部電腦上安裝 Operations Manager 代理程式檔案。安裝代理程式檔案之後，您必須將電腦設定成做為 System Center Proxy 使用。請注意，您在這些電腦上安裝及設定 Lync Server 之後，才能執行這些程序。


---
title: 確認組態設定
TOCTitle: 確認組態設定
ms:assetid: 51c2d1d9-63f7-43ab-88ca-b8913da7cede
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204885(v=OCS.15)
ms:contentKeyID: 49290912
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認組態設定

 

_**上次修改主題的時間：** 2012-09-06_

您可以在 中央管理存放區所在的內部電腦 (或安裝 Lync Server 2013 核心元件 (OcsCore.msi) 的任何加入網域電腦) 上，執行 Lync Server 2013**Get-CsManagementStoreReplicationStatus** Cmdlet，即可驗證對 Edge Server 的設定資訊複寫。

初始結果可能會指出複寫的狀態為「False」，而非「True」。若是如此，請執行 **Invoke-CsManagementStoreReplication** Cmdlet，等候複寫完成，然後再次執行 **Get-CsManagementStoreReplicationStatus**。


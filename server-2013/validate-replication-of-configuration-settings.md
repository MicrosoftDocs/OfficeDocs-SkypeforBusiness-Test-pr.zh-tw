---
title: 驗證複製組態設定
TOCTitle: 驗證複製組態設定
ms:assetid: 81a3c21d-b28a-4287-adac-11791e8db56d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205042(v=OCS.15)
ms:contentKeyID: 49291491
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證複製組態設定

 

_**上次修改主題的時間：** 2012-10-19_

您可以在中央管理存放區所在的內部電腦或任何加入網域並安裝 Lync Server 2013 核心元件的電腦上，執行 Lync Server 2013**Get-CsManagementStoreReplicationStatus** Cmdlet，即可驗證對 Edge Server 的設定資訊複寫。

初始結果可能會指出複寫的狀態為「False」，而非「True」。若是如此，請執行 **Invoke-CsManagementStoreReplication** Cmdlet，並等候複寫完成，然後再次執行 **Get-CsManagementStoreReplicationStatus** Cmdlet。


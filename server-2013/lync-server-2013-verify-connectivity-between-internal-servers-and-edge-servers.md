---
title: Lync Server 2013：驗證內部伺服器和 Edge Server 之間的連線
TOCTitle: 驗證內部伺服器和 Edge Server 之間的連線
ms:assetid: 219f706e-2b8a-46c5-b394-c384240eef50
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398292(v=OCS.15)
ms:contentKeyID: 49290327
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中驗證內部伺服器和 Edge Server 之間的連線

 

_**上次修改主題的時間：** 2012-09-08_

在 Lync Server 2013 中，可使用個別的 \[驗證精靈\] 來協助驗證 Edge Server 和內部伺服器之間的連線。在 Lync Server 2013 中，當您安裝 Edge Server 後，連線驗證會自動進行。

您可以在 中央管理存放區所在的內部電腦 (或安裝 Lync Server 2013 核心元件 (OcsCore.msi) 的任何已加入網域電腦) 上，執行 Windows PowerShell**Get-CsManagementStoreReplicationStatus** Cmdlet，即可驗證對 Edge 的設定資訊複寫。初始結果可能會指出複寫的狀態為 "False"，而非 "True"。若是如此，請執行 **Invoke-CsManagementStoreReplication** Cmdlet、等候複寫完成，然後再次執行 **Get-CsManagementStoreReplicationStatus**。

您可以單獨驗證外部使用者連線，包括使用 Office Communications Server 遠端連線分析程式來驗證遠端使用者連線。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中驗證外部使用者的連線能力](lync-server-2013-verify-connectivity-for-external-users.md)＞。


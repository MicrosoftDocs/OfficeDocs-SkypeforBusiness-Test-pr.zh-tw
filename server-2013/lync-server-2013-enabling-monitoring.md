---
title: 在 Lync Server 2013 中啟用監控
TOCTitle: 在 Lync Server 2013 中啟用監控
ms:assetid: 244df419-d0a8-4b1d-aedd-a92114172ab6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687994(v=OCS.15)
ms:contentKeyID: 49889978
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用監控

 

_**上次修改主題的時間：** 2012-10-17_

雖然系統會自動安裝和啟動每部前端伺服器上的整合資料收集代理程式，但這並不表示您在完成安裝 Microsoft Lync Server 2013 之後就能自動開始收集監視資料。您還必須執行下列兩個動作：將前端伺服器/前端集區與監控資料庫建立關聯，且您必須啟用全域範圍及/或網站範圍的詳細通話記錄 (CDR) 及/或經驗品質 (QoE) 監視。

如需將前端伺服器或前端集區與監控資料庫建立關聯的逐步指引，請參閱部署指南中的＜[在 Lync Server 2013 中讓監控儲存區與前端集區產生關聯](lync-server-2013-associating-a-monitoring-store-with-a-front-end-pool.md)＞主題。即使建立好這些關聯並發行新的 Lync Server 拓撲之後，您還是不能收集監視資料。這是因為當您安裝 Lync Server 2013 時，系統預設會停用 CDR 和 QoE 資料收集。

若要開始收集資料，您必須啟用 CDR 及/或 QoE 監視。(請注意，您不需要同時啟用 CDR 和 QoE 監視；若有需要的話，您可以只啟用其中一種監視，並停用另一種類型。) 若要啟用全域範圍的 CDR 監視，請從 Lync Server 管理命令介面執行下列命令：

    Set-CsCdrConfiguration -Identity "global" -EnableCDR $True

或者，您可從 Lync Server 2013 控制台啟用 CDR 監視。請從 Lync Server 控制台，完成下列程序：

1.  按一下 \[監視\]。

2.  在 \[詳細通話記錄\] 索引標籤上，按兩下 \[全域\] 設定。

3.  在 \[編輯詳細通話記錄 (CDR) 設定\] 窗格中，選取 \[啟用 CDR 監視\]，然後按一下 \[認可\]。

若要啟用全域範圍的 QoE 監視，請從 Lync Server 管理命令介面執行下列命令：

    Set-CsQoEConfiguration -Identity "global" -EnableQoE $True

若有需要的話，您也可以從 Lync Server 控制台啟用 QoE 監視。請從控制台，完成下列程序：

1.  按一下 \[監視\]。

2.  在 \[經驗品質資料\] 索引標籤上，按兩下 \[全域\] 設定。

3.  在 \[編輯經驗品質 (QoE) 設定\] 窗格中，選取 \[啟用 QoE 資料監視\]，然後按一下 \[認可\]。

如前所述，上述的範例可啟用全域範圍的監視；也就是說，其可啟用您整個組織的 CDR 和 QoE 監視。此外，您也可以在網站範圍建立個別的 CDR 和 QoE 組態設定，然後再分別針對每個網站啟用或停用監視。例如，您可以啟用 Redmond 網站的 CDR 監視，然後停用 Dublin 網站的 CDR 監視。如需管理監視組態設定的詳細資訊，請參閱部署指南的＜[在 Lync Server 2013 中設定詳細通話記錄及經驗品質設定](lync-server-2013-configuring-call-detail-recording-and-quality-of-experience-settings.md)＞主題。


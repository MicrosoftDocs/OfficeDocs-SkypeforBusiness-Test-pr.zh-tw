---
title: 視訊會議的互通性考量
TOCTitle: 視訊會議的互通性考量
ms:assetid: 31ead3b5-ed95-42d4-96e2-7d9403d5c026
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204790(v=OCS.15)
ms:contentKeyID: 49290516
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 視訊會議的互通性考量

 

_**上次修改主題的時間：** 2012-10-02_

本章節說明當舊版用戶端及 Lync Server 2013 集區之間，或 Lync Server 2013 用戶端與舊版集區之間具有互通性時，移轉共存階段期間的使用者經驗。

## Lync Server 2013 集區

當 Lync Server 2013 集區中使用舊版用戶端時，使用者會遇到下列行為：

  - 若為雙方通話，則視訊解析度和舊版集區中相同。

  - 若為多方會議，則視訊解析度及視訊會議功能和舊版集區中相同。不提供圖庫檢視及高解析度。

## 舊版集區

當舊版集區中使用 Lync Server 2013 用戶端時，使用者會遇到下列行為：

  - 若為雙方通話，Lync Server 2013 用戶端可使用如下的新功能：
    
      - 若雙方參與者皆使用 Lync Server 2013 用戶端，就可以使用 H.264。
    
      - 因為舊版伺服器不會透過 Inband 佈建傳送此資訊，所以 Lync Server 2013 用戶端會使用 TotalReceiveVideoBitRateKb 的預設值。

  - 若為多方會議，則視訊解析度及視訊功能和舊版集區中舊版使用者所經歷的相同。

> [!NOTE]
> 當舊版伺服器主控 Lync Server 2013 用戶端時，可以設定視訊會議頻寬，使集區上的所有使用者僅會收到低解析度的視訊，但可傳送高解析度的視訊。此情況的範例即是在媒體組態中將 MaxVideoRateAllowed 設為 CIF-250K，在會議原則中將 VideoBitRateKb 設為 2000 kbps。此情況所產生的影響就是集區中的使用者無法收到高解析度。<br />
> 由於 Lync Server 2013 用戶端已不再使用 MaxVideoRateAllowed，所以無法阻擋 Lync Server 2013 用戶端要求高解析度視訊。改成在會議原則中針對集區的所有使用者，將 VideoBitRateKb 設定為與 MaxVideoRateAllowed 相同的值 (亦即將 CIF 設為 250 kbps，或將 VGA 設為 600 kbps，或將 HD 設為 1500 kbps)。


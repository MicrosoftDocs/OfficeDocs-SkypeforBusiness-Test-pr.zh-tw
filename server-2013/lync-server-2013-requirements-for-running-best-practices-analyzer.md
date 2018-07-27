---
title: 執行最佳做法分析程式的需求
TOCTitle: 執行最佳做法分析程式的需求
ms:assetid: 3c7dc44e-5f8a-40a7-9ebb-9ad707ac0007
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg591345(v=OCS.15)
ms:contentKeyID: 49290657
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 執行最佳做法分析程式的需求

 

_**上次修改主題的時間：** 2012-09-19_

您可以使用 Lync Server 2013 最佳做法分析程式來掃描 Lync Server 2013 環境。無法使用它來掃描舊版的環境，而必須使用舊版工具來掃描那些環境。如需下載及使用 Lync Server 2010 和 Office Communications Server 2007 R2 版本之最作做法分析程式的詳細資訊，請參閱＜Lync Server 2010 最佳做法分析程式＞，網址為 [http://go.microsoft.com/fwlink/?linkid=210536\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=256358%26clcid=0x404) 以及＜Office Communications Server 2007 與 Office Communications Server 2007 R2 的最佳做法分析程式＞，網址為 [http://go.microsoft.com/fwlink/?linkid=256358\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=210651%26clcid=0x404)。

開始掃描之前，應該確定 Lync Server 2013 環境中所有的元件都在執行並在線上。

> [!NOTE]  
> 取決於 Edge Server 的組態及任何的相關周邊網路設定 (包括防火牆設定及權限)，最佳做法分析程式有可能無法存取並掃描 Edge Server。如果將 Edge Server 涵蓋在掃描中，而報告指出存取 Edge Server 發生問題，最好將 Edge Server 從掃描選項中移除，然後再次執行掃描，報告就不會顯示這個問題。



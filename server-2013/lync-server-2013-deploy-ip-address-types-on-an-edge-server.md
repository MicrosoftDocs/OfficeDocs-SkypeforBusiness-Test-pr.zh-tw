---
title: Lync Server 2013：在 Edge Server 上部署 IP 位址類型
TOCTitle: 在 Edge Server 上部署 IP 位址類型
ms:assetid: 6e2fe7e8-6e90-4d1a-8fc5-e3be92c46571
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204984(v=OCS.15)
ms:contentKeyID: 49291242
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 在 Edge Server 上部署 IP 位址類型

 

_**上次修改主題的時間：** 2012-06-14_

使用 拓撲產生器執行下列程序的步驟，以部署 Edge Server 上的 IP 位址類型。

## 部署 Edge Server 上的 IP 位址類型

1.  在 拓撲產生器中 **\[Edge 集區\]** 下方以滑鼠右鍵按一下集區中的伺服器，然後選取 **\[編輯內容\]** 。(或者，選取伺服器，然後從 **\[動作\]** 功能表按一下 **\[編輯內容\]** 。)

2.  在 **\[編輯內容\]** 視窗中，選取您要支援的 IP 位址設定。下列圖例展示內部介面與外部介面的雙重堆疊設定。
    
    **雙重堆疊的 Edge Server 內部介面**
    
    ![\[Lync Server 一般內容\] 頁面](images/JJ204984.5b0883ee-b9f2-4a21-91a9-3286d0beb63b(OCS.15).png "[Lync Server 一般內容] 頁面")
    
    **雙重堆疊的 Edge Server 外部介面**
    
    ![\[Lync Server 下一個躍點/外部組態\] 頁面](images/JJ204984.2aa00ce2-ba50-40aa-bbf1-78636016daf9(OCS.15).png "[Lync Server 下一個躍點/外部組態] 頁面")

3.  您必須針對所選取的每個位址類型提供適當的內部及外部位址。


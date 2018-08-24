---
title: 在 Lync Server 2013 設定視訊頻寬
TOCTitle: 在 Lync Server 2013 設定視訊頻寬
ms:assetid: 446bed91-b26f-4ab2-b2f5-36e6810b405b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204842(v=OCS.15)
ms:contentKeyID: 49290762
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 設定視訊頻寬

 

_**上次修改主題的時間：** 2012-10-02_

Lync Server 2013 包含數項設定，可管理雙方通話和多方會議的視訊。當您部署 Lync Server 2013 時，應評估預設設定是否適合您的組織，並視需要修改。

本節所述的參數適用於雙方通話和多方會議。請使用下列其中一個 Cmdlet 來檢視或修改這些設定：

  - **Get-CsConferencingPolicy**

  - **Set-CsConferencingPolicy**

  - **New-CsConferencingPolicy**

在您的會議原則中確認下列設定：

  - **VideoBitRateKb** 這個設定指定最大視訊位元速率，單位為 kbps，用於由使用者所傳送的視訊。預設值為 50000 kbps。有效值為 0 至 50000。
    
    這個設定分別套用至主要視訊和全景視訊。
    
    範例：如果您指定 2000 kbps，Lync Server 則可為主要視訊資料流傳送 2000 kbps，為全景視訊資料流傳送 2000 kbps。
    
    > [!NOTE]  
    > Lync 2013 端點的最大視訊網路頻寬為主要視訊 8000 kbps 及全景視訊 2500 kbps。只有當接收或傳送多個視訊時，才會達到上述最大值。如需詳細資訊，請參閱＜<a href="lync-server-2013-network-bandwidth-requirements-for-media-traffic.md">媒體流量的網路頻寬需求</a>＞中的＜媒體流量網路使用量＞一節。這一節列出所有支援的解析度的最大及一般視訊資料流頻寬。
    


  - **TotalReceiveVideoBitRateKb** 這是 Lync Server 2013 中的新設定，指定用戶端接收的所有視訊資料流的最大允許位元速率 (單位為 kbps)；也就是指定用戶端可以接收的所有視訊資料流的總和，全景視訊資料流除外。例如，如果您指定 1500 kbps，則用戶端最高可接收 1500 kbps 的視訊，其中可能包含多個視訊資料流或單一個視訊資料流。這個設定只套用至 Lync Server 2013 用戶端。
    
    **TotalReceiveVideoBitRateKb** 的預設值為 50000 kbps。如果「圖庫檢視」的 **EnableMultiviewJoin** 設定為 True，**TotalReceiveVideoBitRateKb** 的設定就不得低於 420 kbps。如果「圖庫檢視」的 **EnableMultiviewJoin** 設定為 False，**TotalReceiveVideoBitRateKb** 的設定就不得低於 100 kbps。如果 **EnableMultiviewJoin** 設定為 True，但您將值設定為低於 420 kbps，該值將會預設為臨界值。這個臨界值有助於防止意外的錯誤設定，避免造成不佳的使用者體驗。
    
    > [!NOTE]  
    > 如需有關 <strong>EnableMultiviewJoin</strong> 設定的詳細資訊，請參閱＜<a href="lync-server-2013-configuring-gallery-view.md">設定圖庫檢視</a>＞。
    


  - **MaxVideoConferencingResolution** 這個參數已不再用於 Lync Server 2013 會議中的 Lync Server 2013 用戶端。Lync Server 2013 會議使用本節稍早所述的位元速率控制項。這個設定仍用於加入 Lync Server 2013 會議的舊版用戶端。這個參數會決定在隸屬於 Lync Server 2013 的使用者所安排的會議中，舊版用戶端的最大允許解析度。也就是說，對於舊版用戶端的處理方式和在舊版的 Lync Server 或 Office Communications Server 中是一樣的。

除了套用至使用者的會議原則設定，也要評估媒體組態設定。請使用下列其中一個 Cmdlet 來檢視或修改這些設定：

  - **Get-CsMediaConfiguration**

  - **Set- CsMediaConfiguration**

  - **New- CsMediaConfiguration**

確認下列設定：

  - **MaxVideoRateAllowed** 這個個別集區的設定指定用戶端端點上傳送視訊訊號的最高速率，且只會套用至舊版的 Lync Server 用戶端。
    
    > [!NOTE]  
    > Lync Server 2013 用戶端會忽略這個設定，而在會議原則中使用 TotalReceiveVideoBitRateKb 設定。
    
    
    預設值為 HD720P。有效值為 HD720p15M、VGA600K 和 CIF250K。
    
    範例：如果您指定 1500 kbps，則集區中所有舊版用戶端在雙方或多方會議中都可以接收高達 1500 kbps 的視訊。

下列程序是使用 Lync Server 管理命令介面來修改本節所述設定的範例。

## 修改視訊設定的會議原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列上執行下列 Cmdlet 以編輯會議原則：
    
        Set-CsConferencingPolicy -Identity Pool01ConferencingPolicy -VideoBitRateKb 2000 -TotalReceiveVideoBitRateKb 2000 

## 修改舊版用戶端的媒體組態

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列上執行下列 Cmdlet 以編輯媒體組態：
    
        Set-CsMediaConfiguration -Identity site:Redmond01 -MaxVideoRateAllowed CIF250K


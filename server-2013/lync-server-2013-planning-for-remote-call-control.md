---
title: Lync Server 2013：規劃遠端通話控制
TOCTitle: 規劃遠端通話控制
ms:assetid: 688a0328-1aa7-449f-b5f7-98c876112ed2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558658(v=OCS.15)
ms:contentKeyID: 49291188
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃遠端通話控制

 

_**上次修改主題的時間：** 2012-09-05_

在 Lync Server 2013 中，遠端呼叫控制案例支援可讓使用者在桌上型電腦上使用 Lync 2013，以控制專用交換機 (PBX) 電話。本節說明遠端呼叫控制功能，以及部署遠端呼叫控制的需求。

PBX 與 Lync Server 2013 的整合可讓已啟用遠端呼叫控制的使用者使用 Lync 2013 使用者介面 (UI)，透過下列方式控制 PBX 電話上的通話：

> [!NOTE]  
> 最終，主控使用者之 PBX 電話的 PBX 功能可決定該使用者可使用的遠端呼叫控制功能。



  - 撥出電話

  - 接聽來電

  - 使用立即訊息接聽來電
    
    > [!NOTE]  
    > 亦即，當來電者的電話號碼可以與您組織之全域通訊清單 (GAL)、被呼叫者之 Lync 連絡人清單或同盟協力廠商之組織中的立即訊息位址相關聯時。
    


  - 轉接電話

  - 轉接來電

  - 保留通話

  - 切換多個並行通話

  - 在通話時接聽第二個通話 (即插撥)

  - 撥打複頻式訊號 (DTMF) 數字

  - 在 \[交談\] 視窗中，於 Microsoft Office OneNote 筆記記錄程式中輸入記事

另外，啟用使用者的遠端呼叫控制時， Lync 2013 也會將下列通話資訊提供給使用者：

  - 來電者的電話號碼存在於啟用遠端呼叫控制功能之使用者的 Microsoft Office Outlook 訊息和共同作業用戶端連絡人清單、 Lync 連絡人清單或組織的 GAL 時，以名稱顯示的來電者識別。

  - 過去的來電及撥出電話 (儲存至 Outlook 的 \[交談記錄\] 資料夾中)。

  - 未接來電通知 (傳送給使用者的 Outlook \[收件匣\] 資料夾，但只有在接收到來電時有執行 Lync 時才會產生)。

## 遠端呼叫控制及　Enterprise Voice

雖然遠端呼叫控制功能與 企業語音功能不同，而且無法為使用者同時啟用這兩種功能，但是 企業語音還是會提供也可供啟用遠端呼叫控制的使用者使用的功能子集。如果已部署 企業語音，則啟用遠端呼叫控制的使用者可以使用 Lync 存取下列 企業語音功能：

  - 撥打及接收另一個 Lync 用戶端的音訊通話

  - 加入啟用 企業語音之使用者所建立會議的音訊部分

## 本節內容

  - [Lync Server 2013 中遠端呼叫控制的部署工作](lync-server-2013-deployment-tasks-for-remote-call-control.md)


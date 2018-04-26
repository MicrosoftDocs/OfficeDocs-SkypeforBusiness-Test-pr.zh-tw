---
title: 在移轉後變更簡單 URL
TOCTitle: 在移轉後變更簡單 URL
ms:assetid: addb0dc8-8324-42b1-9a00-f4bd14fdf5c0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721844(v=OCS.15)
ms:contentKeyID: 49890255
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在移轉後變更簡單 URL

 

_**上次修改主題的時間：** 2012-09-22_

Lync Server 支援 3 個簡單 URL：

  - **Meet** 可作為網站或組織中所有會議的基底 URL。 透過 Meet 簡單 URL，加入會議的連結可更容易理解，且更容易溝通與分送。

  - **Dial-in** 可讓使用者存取 \[電話撥入式會議設定\] 網頁。 Dial-in 簡單 URL 會包含在所有的會議邀請中，讓想要撥號參加會議的使用者能夠存取所需的電話號碼與 PIN 資訊。

  - **Admin** 可快速存取 Lync Server 控制台。Admin 簡單 URL 是您組織內部的 URL。

移轉至 Lync Server 2013 後，您必須了解變更會如何影響簡單 URL 的 DNS 記錄與憑證。如果仍在拓撲中使用傳統 Lync Server 2010 Director，則不需變更您的簡單 URL。如果移轉後從拓撲移除 Lync Server 2010 Director，則必須更新簡單 URL DNS 記錄，以指向其中一個 Lync Server 2013 集區。只要您變更了簡單 URL 名稱，您就必須在每個 Director 與前端伺服器上執行 Enable-CsComputer，以登錄變更。

## 在移轉後變更簡單 URL

**更新 Meet 簡單 URL**

1.  在 拓撲產生器中，用滑鼠右鍵按一下 \[Lync Server\] 上層節點，然後按一下 \[編輯內容\] 。

2.  在左窗格中選取 \[簡單 URL\] ，然後在 \[會議 URL\] 下，選取 Meet URL 然後按一下 \[編輯 URL\] 。

3.  將 URL 更新為想要的值，然後按一下 \[確定\] 儲存編輯的 URL。

**更新 Admin 簡單 URL**

1.  在 拓撲產生器中，用滑鼠右鍵按一下 \[Lync Server\] 上層節點，然後按一下 \[編輯內容\] 。

2.  在左窗格中選取 \[簡單 URL\] ，然後在 \[系統管理存取 URL\] 方塊下，輸入您想要以系統管理存取 Lync Server 2013 控制台的簡單 URL，然後一下 \[確定\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>建議您盡可能使用最簡單的 URL 作為管理 URL。最簡單的選項是 <strong>https://admin.</strong><em>&lt;domain&gt;</em>。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 概念

[在 Lync Server 2013 中規劃簡單 URL](lync-server-2013-planning-for-simple-urls.md)


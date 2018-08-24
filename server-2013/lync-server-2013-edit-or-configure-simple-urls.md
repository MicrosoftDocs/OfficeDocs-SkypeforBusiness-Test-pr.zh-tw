---
title: Lync Server 2013：編輯或設定簡單 URL
TOCTitle: 編輯或設定簡單 URL
ms:assetid: 0008aeea-4ae9-4e36-83cd-ef7ff7b6e128
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398063(v=OCS.15)
ms:contentKeyID: 49289884
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中編輯或設定簡單 URL

 

_**上次修改主題的時間：** 2014-02-04_

此程序不需要本機系統管理員或已授權網域群組中的成員資格。您應該以標準使用者身分登入電腦。

Lync Server 2013 會使用簡單 URL 將內部和外部電話引導至 前端伺服器上或 Director 上的服務 (如果已部署)。如需簡單 URL 的詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃簡單 URL](lync-server-2013-planning-for-simple-urls.md)。您有多種簡單 URL 的格式選項可以選擇。如需這些選項的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中簡單 URL 的 DNS 需求](lync-server-2013-dns-requirements-for-simple-urls.md)。

根據預設，簡單 URL 會以下列格式設定 (例如，dial-in 的簡單 URL)：https://dialin.\<SIP 網域\>

## 若要設定簡單 URL

1.  在 拓撲產生器 中，以滑鼠右鍵按一下 **Lync Server** 節點，然後按一下 \[編輯內容\]。

2.  在 \[簡單 URL\] 窗格中，選取 \[電話存取 URL:\] (撥入) 或 \[會議 URL:\] (會議) 來編輯，然後按一下 \[編輯 URL\] 。

3.  將 URL 更新為想要的值，然後按一下 **\[確定\]** 儲存編輯的 URL。此處顯示的範例已將 Dial-in URL 修改為 https://pool01.contoso.net/dialin。

4.  必要時，使用相同步驟編輯 Meet URL。

## 若要定義選用的 Admin 簡單 URL

1.  在 拓撲產生器 中，以滑鼠右鍵按一下 **Lync Server** 節點，然後按一下 \[編輯內容\]。

2.  在 **\[系統管理存取 URL\]** 方塊中，輸入您想用於提供 Lync Server 2013 控制台系統管理存取的簡單 URL，然後按一下 **\[確定\]** 。
    
    > [!TIP]
    > 建議您盡可能使用最簡單的 URL 作為 Admin URL。最簡單的選項是 <strong>https://admin.</strong><em>&lt;domain&gt;</em>。
    
    > [!IMPORTANT]  
    > 如果您在初始部署之後變更簡單 URL，則必須留意有哪些變更會影響簡單 URL 的網域名稱系統 (DNS) 記錄和憑證。如果此變更會影響簡單 URL 的基底，您也必須變更 DNS 記錄和憑證。例如，從 https://lync.contoso.com/Meet 變更為 https://meet.contoso.com，會使基底 URL 從 lync.contoso.com 變更為 meet.contoso.com，所以您需要將 DNS 記錄和憑證變更成指向 meet.contoso.com。如果您將簡單 URL 從 https://lync.contoso.com/Meet 變更為 https://lync.contoso.com/Meetings，則基底 URL lync.contoso.com 維持不變，所以不需要變更 DNS 或憑證。但是，每當您變更簡單 URL 名稱，就必須在每個 Director 和 前端伺服器上執行 <strong>Enable-CsComputer</strong> Cmdlet 來註冊變更。
    


## 請參閱

#### 概念

[在 Lync Server 2013 中規劃簡單 URL](lync-server-2013-planning-for-simple-urls.md)


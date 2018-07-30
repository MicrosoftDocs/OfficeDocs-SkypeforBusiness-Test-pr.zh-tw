---
title: Lync Server 2013：安裝 Edge Server
TOCTitle: 安裝 Edge Server
ms:assetid: 1655ab69-3899-4ee4-a1cc-8243bc1bfa0f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398230(v=OCS.15)
ms:contentKeyID: 49290199
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 的 Edge Server

 

_**上次修改主題的時間：** 2012-09-08_

您會使用 \[ Lync Server 部署精靈\]，在 Edge Server 上安裝 Lync Server 2013。在每部 Edge Server 上執行 \[部署精靈\]，可以完成設定 Edge Server 所需的大部分工作。若要在 Edge Server 上部署 Lync Server 2013，您必須已執行 拓撲產生器來定義及發行 Edge Server 拓撲，並將其匯出至可從 Edge Server 使用的媒體。如需詳細資訊，請參閱＜ [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞及＜ [匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md)＞。

使用部署精靈安裝好每個 Edge Server、安裝並指派必要憑證，以及啟動必要服務後，您可使用[在 Lync Server 2013 中設定外部使用者存取支援](lync-server-2013-configuring-support-for-external-user-access.md)中的資訊來啟用並設定外部使用者存取，以及[在 Lync Server 2013 中驗證 Edge 部署](lync-server-2013-verifying-your-edge-deployment.md)中的資訊來驗證安裝，包括伺服器和用戶端連線，以便完成安裝。

## 安裝 Edge Server

1.  以本機 Administrators 群組成員的身分或具有相同使用者權限的帳戶，登入您想要安裝 Edge Server 的電腦。

2.  確定 Edge Server 上具有您以 拓撲產生器建立並匯出，以及複製至外部媒體的可用拓撲設定檔案 (例如，存取內含複製拓撲設定檔案的 USB 磁碟，或確定可以存取複製檔案所在位置的網路共用)。

3.  啟動部署精靈。
    
    > [!NOTE]  
    > 如果出現訊息告知必須安裝 Microsoft Visual C++ 可轉散發套件，請按一下 <strong>[是]</strong> 。在下一個對話方塊中，您可以接受預設的 <strong>[安裝位置]</strong> ，也可以按一下 <strong>[瀏覽]</strong> 選取其他位置，然後按一下 <strong>[安裝]</strong> 。在下一個對話方塊中，選取 <strong>[我接受授權合約中的條款]</strong> 核取方塊，然後按一下 <strong>[確定]</strong> 。
    


4.  在 \[部署精靈\] 中按一下 \[安裝或更新 Lync Server 系統\] 。

5.  等精靈決定部署狀態後，在 **\[步驟 1：安裝本機設定存放區\]** 中按一下 **\[執行\]** ，然後執行下列步驟：
    
      - 在 **\[設定中央管理存放區的本機複本\]** 對話方塊中，按一下 **\[從檔案匯入 (建議 Edge Server 使用)\]** ，前往匯出拓撲設定檔的位置、選取 .zip 檔案、按一下 **\[開啟\]** ，然後按 **\[下一步\]** 。
    
      - 部署精靈會從設定檔讀取設定資訊，並將 XML 設定檔寫入本機電腦。
    
      - **\[執行命令\]** 程序完成後，按一下 **\[完成\]** 。

6.  在 \[部署精靈\] 中，按一下 \[步驟 2：安裝或移除 Lync Server 元件\] ，安裝儲存於本機電腦中之 XML 設定檔指定的 Lync Server 2013 Edge 元件。

7.  完成安裝後，使用[針對 Lync Server 2013 設定 Edge 憑證](lync-server-2013-set-up-edge-certificates.md)中的資訊，安裝和指派必要憑證，之後就能啟動服務。


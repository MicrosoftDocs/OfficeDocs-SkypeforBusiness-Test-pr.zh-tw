---
title: Lync Server 2013：在伺服器上啟動服務
TOCTitle: 在伺服器上啟動服務
ms:assetid: fa26eaed-0529-4f32-9f3f-f32c4bd4b1c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413059(v=OCS.15)
ms:contentKeyID: 49292869
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 在伺服器上啟動服務

 

_**上次修改主題的時間：** 2014-09-03_

若要成功完成本程序，您需要以 RTCUniversalServerAdmins 群組成員使用者的身分登入或者具有正確的代理權限。如需委派權限的詳細資訊，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)主題。

在您的伺服器上安裝本機設定存放區後，請安裝 Lync Server 2013 元件，並在 前端伺服器 或 前端伺服器 上設定憑證。您必須在伺服器上啟動 Lync Server 2013 服務。使用下列程序，在您部署中的每個 前端伺服器 上啟動服務。

## 在前端伺服器上啟動服務

1.  在 Lync Server 部署精靈中的 **Lync Server 2013** 頁面上，按一下 \[執行\] (位於 \[步驟 4：啟動服務\] 。

2.  在 \[啟動服務\] 頁面上，按 \[下一步\] 即可在伺服器上啟動 Lync Server 服務。

3.  在 \[執行命令\] 頁面上順利啟動所有服務之後，按一下 \[完成\] 。
    
    > [!IMPORTANT]  
    > 在伺服器上啟動服務的命令是報告事實上已啟動服務的最佳方法。它可能不會反映服務的實際狀態。建議您在 [啟動服務] 之後立即使用 [服務狀態 (選擇性)] 步驟，以開啟 Microsoft Management Console (MMC)，並確認已成功啟動服務。如果未啟動任何 Lync Server 服務，您可以在 MMC 中以滑鼠右鍵按一下該服務，然後按一下 [啟動] 。
    


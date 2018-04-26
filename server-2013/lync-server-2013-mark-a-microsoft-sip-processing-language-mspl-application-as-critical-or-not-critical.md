---
title: 將 Microsoft SIP Processing Language (MSPL) 應用程式標示為 或
TOCTitle: 將 Microsoft SIP Processing Language (MSPL) 應用程式標示為 或
ms:assetid: df68fdc6-b7e6-4f07-acdc-0cd4c2c888a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182598(v=OCS.15)
ms:contentKeyID: 49292554
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Microsoft SIP Processing Language (MSPL) 應用程式標示為 或

 

_**上次修改主題的時間：** 2012-11-01_

Microsoft SIP Processing Language (MSPL) 伺服器應用程式是僅指令碼的應用程式，它會使用 MSPL 指令碼語言，而不是 Microsoft Lync 2010 API。某些 MSPL 伺服器應用程式會被指定為關鍵。如果是關鍵指令碼，就必須在系統啟動期間啟動該指令碼，如此 Lync Server 2013 才會啟動。如果指令碼在 Lync Server 執行時失敗，則伺服器不會關閉，但是會停止傳送流量至指令碼，並且將錯誤寫入事件日誌。

您可以使用 Lync Server 控制台，將 Microsoft SIP Processing Language (MSPL) 伺服器應用程式標示為關鍵，或將它們取消標示。

並非所有指令碼都支援此選項。例如，DefaultRouting 指令碼會標示為關鍵，且無法為 DefaultRouting 變更這個選項。

## 若要將 MSPL 伺服器應用程式標示 (或取消標示) 為關鍵

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[拓撲\]**，然後按一下 **\[伺服器應用程式\]**。

4.  在 **\[伺服器應用程式\]** 頁面上，視需要按一下欄標題以排序應用程式，然後按一下您要修改的伺服器應用程式。

5.  按一下 **\[動作\]**。

6.  按一下 **\[標示為關鍵\]** 或 **\[取消選取為關鍵\]** (也就是，如果指令碼支援這個選項)。

## 請參閱

#### 工作

[啟用或停用 Microsoft SIP Processing Language (MSPL) 伺服器應用程式](lync-server-2013-enable-or-disable-a-microsoft-sip-processing-language-mspl-server-application.md)  

#### 概念

[在 Lync Server 2013 中檢視 Microsoft SIP Processing Language (MSPL) 伺服器應用程式](lync-server-2013-view-microsoft-sip-processing-language-mspl-server-applications.md)  

#### 其他資源

[管理 Lync Server 2013 拓撲](lync-server-2013-managing-the-lync-server-topology.md)


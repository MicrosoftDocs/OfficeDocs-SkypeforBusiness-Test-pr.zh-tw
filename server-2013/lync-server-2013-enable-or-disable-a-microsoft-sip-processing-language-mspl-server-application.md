---
title: 啟用或停用 Microsoft SIP Processing Language (MSPL) 伺服器應用程式
TOCTitle: 啟用或停用 Microsoft SIP Processing Language (MSPL) 伺服器應用程式
ms:assetid: b20af38d-224a-4459-991d-0b7eabb3ca7c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182573(v=OCS.15)
ms:contentKeyID: 49292045
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用 Microsoft SIP Processing Language (MSPL) 伺服器應用程式

 

_**上次修改主題的時間：** 2012-09-21_

您可以使用 Lync Server 控制台來啟用或停用在您的 Lync Server 2013 環境中執行的 Microsoft SIP Processing Language (MSPL) 伺服器應用程式。這些應用程式是使用指令碼語言 (而非 Microsoft Lync 2013 Preview API) 的僅指令碼應用程式。

並非所有指令碼都可以啟用或停用。例如，DefaultRouting 指令碼會被啟用，且無法為 DefaultRouting 變更這個選項。

## 若要啟用或停用 MSPL 伺服器應用程式

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[拓撲\]**，然後按一下 **\[伺服器應用程式\]**。

4.  在 **\[伺服器應用程式\]** 頁面上，視需要按一下欄標題以排序應用程式，然後按一下您要修改的伺服器應用程式。

5.  按一下 \[動作\]。

6.  按一下 **\[啟用應用程式\]** 或 **\[停用應用程式\]** (也就是，如果指令碼支援這個選項)。

## 請參閱

#### 工作

[將 Microsoft SIP Processing Language (MSPL) 應用程式標示為 \[關鍵\] 或](lync-server-2013-mark-a-microsoft-sip-processing-language-mspl-application-as-critical-or-not-critical.md)  

#### 概念

[在 Lync Server 2013 中檢視 Microsoft SIP Processing Language (MSPL) 伺服器應用程式](lync-server-2013-view-microsoft-sip-processing-language-mspl-server-applications.md)  

#### 其他資源

[管理 Lync Server 2013 拓撲](lync-server-2013-managing-the-lync-server-topology.md)


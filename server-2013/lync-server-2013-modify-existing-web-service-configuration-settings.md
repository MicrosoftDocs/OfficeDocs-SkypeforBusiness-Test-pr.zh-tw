---
title: 修改現有 Web 服務組態設定
TOCTitle: 修改現有 Web 服務組態設定
ms:assetid: bd9c7aa5-d31c-4fab-b31d-8baae26b1296
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182580(v=OCS.15)
ms:contentKeyID: 49292152
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改現有 Web 服務組態設定

 

_**上次修改主題的時間：** 2012-11-01_

您可以使用 \[Web 服務\] 頁面，設定用於存取 Lync Server 2013 相關 Web 伺服器和 Web 服務的驗證方法。

請依照下列步驟來修改現有的 Web 服務原則。

## 若要修改現有的 Web 服務

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[安全性\]**，然後按一下 **\[Web 服務\]**。

4.  在 **\[Web 服務\]** 頁面上，依序按一下設定、**\[編輯\]** 和 **\[顯示詳細資料\]**。

5.  在 \[編輯 Web 服務設定\] 中的 \[整合式 Windows 驗證\] 內，選取 \[交涉\]、\[整合式 Windows 驗證\] 或 \[無\]。

6.  依據用戶端的功能和您環境中的支援，選取下列其中一個或多個項目：
    
      - **\[啟用 PIN 驗證\]** 可允許使用 PIN 號碼來驗證用戶端。
    
      - **\[啟用憑證驗證\]** 以讓集區中的伺服器核發憑證給用戶端。
    
      - **\[啟用憑證鏈結下載\]** 可讓看到驗證憑證的伺服器下載該憑證的憑證鏈結。

7.  按一下 \[認可\]。

## 請參閱

#### 其他資源

[在 Lync Server 2013 控制台中設定驗證](lync-server-2013-configuring-authentication-in-the-lync-server-control-panel.md)


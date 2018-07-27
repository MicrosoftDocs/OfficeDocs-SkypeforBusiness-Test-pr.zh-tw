---
title: 修改現有登錄器組態設定
TOCTitle: 修改現有登錄器組態設定
ms:assetid: a8931511-3e66-49ed-a3ec-03bcd61ce1f0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182566(v=OCS.15)
ms:contentKeyID: 49291936
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改現有登錄器組態設定

 

_**上次修改主題的時間：** 2012-11-01_

您可以使用登錄器設定 Proxy 伺服器驗證通訊協定。如需可用通訊協定的相關資訊，請參閱＜[建立登錄器組態設定](lync-server-2013-create-registrar-configuration-settings.md)＞。

> [!NOTE]  
> 當伺服器支援遠端與企業用戶端的驗證時，我們建議您同時啟用 Kerberos 和 NTLM。Edge Server 和內部伺服器將進行通訊，以確認只提供 NTLM 驗證給遠端用戶端。如果只在這些伺服器上啟用 Kerberos，則伺服器將無法驗證遠端使用者。如果企業使用者也對伺服器進行驗證，則會使用 Kerberos。



請依照下列步驟來修改現有的登錄器。

## 若要修改現有的登錄器

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[安全性\]**，然後按一下 **\[登錄器\]**。

4.  在 **\[登錄器\]** 頁面上，依序按一下服務、**\[編輯\]** 和 **\[顯示詳細資料\]**。

5.  在 **\[編輯登錄器設定\]** 中，依據用戶端的功能和您環境中的支援，選取下列其中一個或多個項目：
    
      - **\[啟用 Kerberos 驗證\]** 以讓集區中的伺服器使用 Kerberos 驗證來提出質詢。
    
      - **\[啟用 NTLM 驗證\]** 以讓集區中的伺服器使用 NTLM 驗證來提出質詢。
    
      - **\[啟用憑證驗證\]** 以讓集區中的伺服器核發憑證給用戶端。

6.  按一下 \[認可\]。


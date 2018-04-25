---
title: 在 Lync Server 2013 中設定會議邀請
TOCTitle: 在 Lync Server 2013 中設定會議邀請
ms:assetid: 7faa4797-0344-418b-9fa3-59dfb9c2baf7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398638(v=OCS.15)
ms:contentKeyID: 49291458
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定會議邀請

 

_**上次修改主題的時間：** 2013-07-16_

您可以在會議邀請的內文中納入下列選擇性項目，自訂 Lync 2013 的線上會議增益集傳送的會議邀請：

  - **您組織的標誌** 使用 \[標誌 URL\] 選項，將您組織的標誌新增到會議邀請。如果會議邀請將傳送給非組織內部的人員，影像應該位在可公開存取的 URL。支援的影像格式是 GIF 和 JPG。雖然 Lync Server 2013 儲存 URL 時，沒有影像的大小限制，但為了獲取最佳效果，影像最大大小應該是 30 像素高 x 188 像素寬。

  - **自訂說明或支援連結** 新增組織說明或支援團隊網站的 URL。如果會議邀請將傳送給非公司內部的人員，URL 應該可公開存取。URL 長度上限為 1 KB。

  - **法律免責聲明文字** 對於所有會議邀請中將顯示的法律文字或免責聲明新增 URL。如果會議邀請將傳送給非公司內部的人員，URL 應該可公開存取。URL 長度上限為 1 KB。

  - **自訂頁尾文字** 新增將在邀請中呈現為自訂頁尾的文字。可新增的文字長度上限為 2 KB。

您可以使用 Lync Server 控制台或 Lync Server 管理命令介面設定這些選項。


**使用 Lync Server 控制台自訂會議邀請**

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]，然後按一下 \[會議設定\]。

4.  在 \[會議設定\] 頁面上按一下 \[新增\]，然後執行下列其中一項操作：
    
      - 若要建立網站層級原則，請按一下 \[站台組態\]。在 \[選取站台\] 搜尋欄位中，輸入您要定義會議加入設定之網站的完整或部分名稱。在產生的網站清單中按一下所需的網站，然後按一下 \[確定\]。
    
      - 若要建立集區層級原則，請按一下 \[集區組態\]。在 \[選取服務\] 搜尋欄位中，輸入您要定義會議加入設定之集區服務的完整或部分名稱。在產生的服務清單中，按一下您需要的集區，然後按一下 \[確定\]。

5.  執行下列任一項作業：
    
      - 在 \[標誌 URL\] 欄位中，輸入您組織標誌影像的 URL。
    
      - 在 \[說明 URL\] 欄位中，輸入您組織說明或支援網站的 URL。
    
      - 在 \[法律文字\] 欄位中，輸入會議邀請中要包含的法律文字或免責聲明 URL。
    
      - 在 \[自訂頁尾文字\] 欄位中， 輸入頁尾文字，最多 2 KB。

**使用 Lync Server 管理命令介面自訂會議邀請**

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 **New-CsMeetingConfiguration** 或 **Set-CsMeetingConfiguration** Cmdlet 建立或設定會議邀請選項。例如，執行：
    
        New-CsMeetingConfiguration -Identity site:Redmond -EnableInviteCustomization $True -LogoURL "http://www.contoso.com/logo/contosobanner.gif" -HelpURL "http://www.contoso.com/support" -LegalURL "http://www.contoso.com/disclaimer" -CustomFooterText "Communications may be monitored or recorded."


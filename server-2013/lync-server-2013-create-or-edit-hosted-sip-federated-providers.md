---
title: Lync Server 2013：建立或編輯主控的 SIP 同盟提供者
TOCTitle: 建立或編輯主控的 SIP 同盟提供者
ms:assetid: 0dd6dcb6-a88d-46b8-9c96-b35967309bcd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552445(v=OCS.15)
ms:contentKeyID: 49290090
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或編輯主控的 SIP 同盟提供者 Lync Server 2013

 

_**上次修改主題的時間：** 2012-10-19_

裝載提供者立即訊息 (IM) 連線功能可讓組織中的使用者使用 IM 來與裝載提供者 (包括 Microsoft Office 365 和 Lync Online) 提供的 IM 服務使用者通訊。

每個裝載提供者都設有提供者的 Edge Server 完整網域名稱，以及預設驗證層級 \[允許使用者僅與其連絡人清單中使用此提供者的人通訊\] 。

使用下列程序來建立或編輯裝載提供者：

## 建立或編輯裝載提供者

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[同盟和外部存取\]** 和 **\[SIP 同盟提供者\]** 。

4.  如果您需要建立新的裝載提供者，請按一下 \[新增\] ，然後按一下 \[裝載提供者\] 。

5.  如果您需要編輯裝載提供者清單中的項目，請選取裝載提供者，按一下 \[編輯\] ，然後按一下 \[顯示詳細資料\] 。

6.  在 **\[編輯 SIP 同盟提供者\]** 頁面上，您可以鍵入或編輯下列設定：
    
      - **允許與這個提供者的通訊**    選取此設定可與這個提供者的使用者進行通訊。
    
      - **\[提供者名稱：\]**    必要屬性，鍵入的提供者名稱會反映在 SIP 同盟提供者的清單中。
    
      - **Access Edge Service (FQDN)：**    必要內容，請輸入您要設定之裝載提供者的 Access Edge Service 完整網域名稱。此資訊應由裝載提供者提供，而唯有當裝載提供者對裝載提供者的 Access Edge Service FQDN 進行變更時，才能變更。
    
      - **\[預設驗證層級：\]**    預設設定， **\[僅允許使用者與其連絡人清單上使用此提供者的人通訊\]** 會限制與您已接受並且在您的連絡人清單中的連絡人通訊。
        
        選取 \[允許使用者與使用此提供者的所有人通訊\] 會移除您必須收到並接受連絡人邀請的限制。此設定不限制哪些人可以從裝載提供者的網路連絡您。

7.  完成設定之後，請按一下 **\[認可\]** 儲存，或按一下 **\[取消\]** 捨棄您的變更。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定原則以控制公用使用者存取](lync-server-2013-configure-policies-to-control-public-user-access.md)  
[在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)


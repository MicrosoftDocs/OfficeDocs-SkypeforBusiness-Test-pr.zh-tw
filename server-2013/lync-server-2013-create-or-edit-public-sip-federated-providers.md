---
title: Lync Server 2013：建立或編輯公用 SIP 同盟提供者
TOCTitle: 建立或編輯公用 SIP 同盟提供者
ms:assetid: 5321598c-1ab1-40e3-b739-4b2e6d0a3a3b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398349(v=OCS.15)
ms:contentKeyID: 49290924
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者

 

_**上次修改主題的時間：** 2012-10-19_

公用立即訊息 (IM) 連線可以讓您組織中的使用者利用 IM 與公用 IM 服務提供者所提供之 IM 服務的使用者進行通訊，包括 Windows Live Messenger、Yahoo\! 和 AOL。

Lync Server 2013 有 America Online、Windows Live 和 Yahoo\! 立即訊息的公用提供者設定。每個公用提供者都會使用提供者的 Edge Server 完整網域名稱，以及預設驗證層級 **\[僅允許使用者與其連絡人清單上使用此提供者的人通訊\]** 來設定。

預設設定為不啟用任何公用提供者。在啟用公用提供者之前，您應該先完成授權合約及佈建工作。您可以在完成授權和佈建工作之前啟用提供者。在必要工作完成之前，使用者將無法與這些提供者的連絡人通訊。如需公用提供者的授權與佈建相關詳細資訊，請參閱〈 [在 Lync Server 2013 中設定原則以控制公用使用者存取](lync-server-2013-configure-policies-to-control-public-user-access.md)〉。

請使用下列程序來建立或編輯公用提供者：

## 建立或編輯公用提供者

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[同盟和外部存取\]** 和 **\[SIP 同盟提供者\]** 。

4.  如果您需要建立新的公用提供者，請依序按一下 **\[新增\]** 和 **\[公用提供者\]** 。

5.  如果您需要編輯公用提供者清單中的項目，選取公用提供者，然後依序按一下 **\[編輯\]** 和 **\[顯示詳細資料\]** 。

6.  在 **\[編輯 SIP 同盟提供者\]** 頁面上，您可以鍵入或編輯下列設定：
    
      - **\[允許與這個提供者的通訊\]**    選取此設定可讓 IM 與此提供者的使用者通訊。
    
      - **\[提供者名稱：\]**    必要屬性，鍵入的提供者名稱會反映在 SIP 同盟提供者的清單中。
    
      - **\[Access Edge Service (FQDN):\]**    必要屬性，鍵入您設定的提供者的 Access Edge Service 完整網域名稱。此資訊的提供是預設項目，只有在公用提供者變更其 Access Edge Service 的 FQDN 時才能變更。
    
      - **\[預設驗證層級：\]**    預設設定， **\[僅允許使用者與其連絡人清單上使用此提供者的人通訊\]** 會限制與您已接受並且在您的連絡人清單中的連絡人通訊。
        
        選取 **\[允許使用者與使用此提供者的所有人通訊\]** 會移除您必須已收到並接受連絡人邀請的限制。此設定不會限制誰可以從公用提供者網路與您連絡。

7.  完成設定之後，請按一下 **\[認可\]** 儲存，或按一下 **\[取消\]** 捨棄您的變更。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定原則以控制公用使用者存取](lync-server-2013-configure-policies-to-control-public-user-access.md)  
[在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)


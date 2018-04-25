---
title: 確認與 Lync Online 客戶的通訊
TOCTitle: 確認與 Lync Online 客戶的通訊
ms:assetid: c8287b15-e1bb-4b26-8354-0ec90b2fcfe7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202189(v=OCS.15)
ms:contentKeyID: 49292300
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認與 Lync Online 客戶的通訊

 

_**上次修改主題的時間：** 2012-10-08_

若要讓組織中的 Lync 使用者能夠與 Microsoft Lync Online 2010 客戶的使用者通訊，您必須完成下列步驟：

  - 符合所有先決條件；包括部署內部伺服器和 Edge Server、啟用組織的同盟支援，以及設定使用者帳戶。如需詳細資訊，請參閱＜[與 Lync Online 客戶同盟的先決條件](lync-server-2013-prerequisites-for-federating-with-a-lync-online-customer.md)＞。

  - 設定內部部署的網域存取支援；包括建立主機提供者項目，以及設定部署以允許從 Lync Online 客戶的網域存取。如需詳細資訊，請參閱＜[為 Lync Online 網域設定同盟支援](lync-server-2013-configure-federation-support-for-a-lync-online-domain.md)＞。

  - 設定您的使用者帳戶以支援同盟。如需詳細資訊，請參閱＜[設定與 Lync Online 客戶同盟的使用者存取](lync-server-2013-configure-user-access-for-federation-with-a-lync-online-customer.md)＞。

在您完成所有的步驟，而且 Lync Online 2010 客戶的系統管理員完成線上服務的所有設定以支援與您組織的同盟後，請測試您組織中內部使用者與 Lync Online 客戶使用者之間的通訊，以確認通訊情形。如果通訊不成功，請使用 Edge Server 的記錄工具擷取記錄和追蹤檔案，以疑難排解問題。如需使用記錄工具的詳細資訊，請參閱作業文件中的[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。如需記錄工具的詳細資訊，請參閱 TechNet Library 的＜Lync Server 2010 記錄工具＞文件，網址為 [http://go.microsoft.com/fwlink/?linkid=199265\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=199265%26clcid=0x404)。


---
title: Lync Server 2013：準備基礎結構和系統
TOCTitle: 準備基礎結構和系統
ms:assetid: 1254ee38-0679-4714-b293-1050f107c158
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398205(v=OCS.15)
ms:contentKeyID: 49290146
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 準備 Lync Server 2013 的基礎結構和系統

 

_**上次修改主題的時間：** 2013-02-21_

部署 Lync Server 2013 時需要使用 拓撲產生器來定義及發行拓撲設計。為了識別拓撲所需的元件，請使用 拓撲產生器來建立與儲存拓撲設計。在拓撲產生器中發行拓撲之前，請執行下列作業：

  - 針對您以拓撲產生器建立並儲存之拓撲設計中的每個元件，取得並安裝硬體，包括所有必要電腦 (執行 Lync Server 2013 的伺服器、資料庫伺服器、執行 Internet Information Services (IIS) 的伺服器，以及反向 Proxy 伺服器，視情況而定)、網路介面卡、硬體負載平衡器和儲存裝置 (例如檔案伺服器)。如需如何定義拓撲來指定部署所需元件的詳細資訊，請參閱＜ [在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)＞。如需伺服器硬體需求的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)＞。

  - 確定網路基礎結構符合需求。如需詳細資訊，請參閱規劃文件中的＜[網路基礎結構需求](lync-server-2013-network-infrastructure-requirements.md)＞。

  - 設定 Active Directory 網域服務。若要發行及啟用拓撲，您需要 AD DS 中的電腦帳戶來代表內部伺服器。您可以將電腦加入 AD DS 來達到這個目的。如需準備 AD DS 的詳細資訊，請參閱＜ [為 Lync Server 2013 準備 Active Directory 網域服務](lync-server-2013-preparing-active-directory-domain-services.md)＞。

  - 建立檔案共用。Standard Edition Server 可以裝載必要檔案的檔案共用，而在 Enterprise 部署中，檔案共用不能裝載在前端伺服器上。必須正確設定在資料夾和共用上部署及設定存取控制清單 (ACL) 時所需的權限和群組成員資格，才能順利完成拓撲產生器。您應該確認執行拓撲產生器的人員具有以下權限和群組成員資格：
    
      - 本機系統管理員成員
    
      - 網域使用者成員
    
      - 共用和檔案存放區之資料夾的完全控制權限

  - 若為 Enterprise Edition，請安裝及設定 SQL Server。為了讓 SQL Server 安裝成功，SQL Server 型伺服器必須在線上，而發行拓撲的人員必須是 SQL Server 上的本機管理員，也必須是 SQL Server 執行個體上的 SQL Server 系統管理員群組成員。

完成本主題說明的所有準備工作後，您還需要在發行拓撲前執行其他準備工作，包括安裝 Windows 作業系統和其他必要的軟體、設定 IIS 及設定 DNS。如需上述工作的詳細資訊，請參閱＜ [執行 Lync Server 2013 之伺服器的系統需求](lync-server-2013-system-requirements-for-servers-running-lync-server-2013.md)＞、＜ [針對 Lync Server 2013 設定 IIS](lync-server-2013-configure-iis.md)＞及＜ [準備 Lync Server 2013 的基礎結構和系統](lync-server-2013-preparing-the-infrastructure-and-systems.md)＞。此外，您應該要熟悉用戶端和用戶端需求。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中部署用戶端和裝置](lync-server-2013-deploying-clients-and-devices.md)＞。

## 本章節內容

  - [Lync Server 2013 的硬體設定](lync-server-2013-hardware-setup.md)

  - [Lync Server 2013 的軟體設定](lync-server-2013-software-setup.md)

  - [為 Lync Server 2013 準備 Active Directory 網域服務](lync-server-2013-preparing-active-directory-domain-services.md)

  - [為 Lync Server 2013 設定 SQL Server](lync-server-2013-configure-sql-server-for-lync-server.md)

  - [在 Lync Server 2013 中設定前端集區或 Standard Edition Server 的 DNS 記錄](lync-server-2013-configure-dns-records-for-a-front-end-pool-or-standard-edition-server.md)

  - [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)


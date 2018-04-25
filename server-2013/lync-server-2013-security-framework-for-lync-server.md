---
title: Lync Server 2013 的安全性架構
TOCTitle: Lync Server 2013 的安全性架構
ms:assetid: 01131e28-b38e-40d9-8524-06725b9c6608
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn481316(v=OCS.15)
ms:contentKeyID: 59683092
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的安全性架構

 

_**上次修改主題的時間：** 2013-11-08_

本節提供 Microsoft Lync Server 2013 安全性架構基本元素的概觀。瞭解這些元素如何共同運作是非常重要的，如此一來，才能做出明智的決策來保護特定 Lync Server 2013 部署的安全。

這些元素如下：

  - Active Directory 網域服務 (AD DS) 提供單一受信任的後端儲存機制，用於存放使用者帳戶和網路資源。

  - 角色型存取控制 (RBAC) 讓您能委派系統管理工作，同時維護高標準的安全性。

  - 公開金鑰基礎結構 (PKI) 使用受信任憑證授權單位 (CA) 核發的憑證，以驗證伺服器並確保資料的完整性。

  - 傳輸層安全性 (TLS)、HTTPS over SSL (HTTPS) 和雙向 TLS (MTLS) 會進行端點驗證和 IM 加密作業。點對點音訊、視訊及應用程式共用資料流，皆會使用安全即時傳輸通訊協定 (Secure Real-Time Transport Protocol, SRTP) 加密。

  - 使用者驗證所需的業界標準通訊協定 (可執行時)。

  - 預設會啟用 Windows PowerShell 提供的安全性功能，讓使用者無法輕易或在不知情的情況下執行指令碼。

這些基本安全性元素會共同運作，以定義受信任的使用者、伺服器、連線及作業，以確保 Lync Server 2013 的安全基礎。

## 本章節內容

本節中的主題說明每一項基礎元素如何運作來增強 Lync Server 基礎結構的安全性。

  - [Lync Server 2013 的 Active Directory 網域服務](lync-server-2013-active-directory-domain-services-for-lync-server.md)

  - [Lync Server 2013 的角色型存取控制 (RBAC)](lync-server-2013-role-based-access-control-rbac.md)

  - [Lync Server 2013 的公開金鑰基礎結構](lync-server-2013-public-key-infrastructure.md)

  - [Lync Server 2013 的 TLS 和 MTLS](lync-server-2013-tls-and-mtls.md)

  - [Lync Server 2013 的加密](lync-server-2013-encryption.md)

  - [Lync Server 2013 的使用者和用戶端驗證](lync-server-2013-user-and-client-authentication.md)

  - [Windows PowerShell 和 Lync Server 2013 管理工具](lync-server-2013-windows-powershell-and-lync-server-management-tools.md)


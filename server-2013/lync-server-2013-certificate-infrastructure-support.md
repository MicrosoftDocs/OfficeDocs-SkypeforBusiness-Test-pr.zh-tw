---
title: Lync Server 2013 憑證基礎結構支援
TOCTitle: 憑證基礎結構支援
ms:assetid: 47aa5c95-eb60-4d4b-81d5-7fdaef1a1145
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425950(v=OCS.15)
ms:contentKeyID: 49290797
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的憑證基礎結構支援

 

_**上次修改主題的時間：** 2013-11-07_

Lync Server 2013 需要公開金鑰基礎結構 (PKI)，才能支援傳輸層安全性 (TLS) 和相互 TLS (MTLS) 連線。依預設， Lync Server 2013 是設成使用 TLS 進行用戶端對伺服器的連線。MTLS 是用於伺服器之間的連線。

Lync Server 2013 的 MTLS 憑證必須由信任的憑證授權單位 (CA) 發行。 Lync Server 支援下列 CA 所發行的憑證：

  - 內部 CA 發行的憑證：
    
      - Windows Server 2003 作業系統 CA
    
      - Windows Server 2008 作業系統 CA
    
      - Windows Server 2008 R2 作業系統 CA
    
      - Windows Server 2012 作業系統 CA
    
      - Windows Server 2012 R2 作業系統 CA

  - 公用 CA 發行的憑證

與其他應用程式和伺服器 (例如 Exchange 2013) 通訊時，需要其他應用程式和產品支援的憑證。 Lync Server 2013 及其他 2013 版的 Microsoft 伺服器產品 (包括 Exchange 2013 和 SharePoint Server) 支援使用開放授權 (OAuth) 通訊協定來進行伺服器對伺服器驗證和授權。如需詳細資訊，請參閱部署文件或作業文件中的＜ [在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)＞。

對於從執行 Windows 7 作業系統、 Windows Server 2008 R2 作業系統 和 Microsoft Office Communicator 2007 Phone Edition 的用戶端建立的連線， Lync Server 2013 支援 (但不需要) 以 SHA-256 密碼編譯雜湊函數簽署的憑證。為支援使用 SHA-256 的外部存取，外部憑證是由公用 CA 使用 SHA-256 發行。

如需有關憑證需求的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 的憑證基礎結構需求](lync-server-2013-certificate-infrastructure-requirements.md)＞。如需有關使用萬用字元憑證的詳細資訊，請參閱＜支援能力＞文件中的＜ [Lync Server 2013 中的萬用字元憑證支援](lync-server-2013-wildcard-certificate-support.md)＞。


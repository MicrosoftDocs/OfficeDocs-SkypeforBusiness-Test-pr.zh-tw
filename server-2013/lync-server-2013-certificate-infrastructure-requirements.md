---
title: Lync Server 2013 憑證基礎結構需求
TOCTitle: 憑證基礎結構需求
ms:assetid: 0051aa23-0bbe-4e72-9f29-e01c6bcc6190
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398066(v=OCS.15)
ms:contentKeyID: 49289889
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的憑證基礎結構需求

 

_**上次修改主題的時間：** 2013-03-22_

Lync Server 2013 需要公開金鑰基礎結構 (PKI) 來支援 TLS 和相互 TLS (MTLS) 連線。

Lync Server 會基於下列目的使用憑證：

  - 用戶端及伺服器之間的 TLS 連線

  - 伺服器之間的 MTLS 連線

  - 使用自動探索協力廠商 DNS 的同盟連線

  - 遠端使用者存取即時訊息 (IM)

  - 外部使用者存取音訊/視訊 (A/V) 工作階段、應用程式共用及會議

  - 使用 Web 服務自動探索的行動要求

Lync Server 適用下列一般需求：

  - 所有的伺服器憑證必須支援伺服器授權 (伺服器 EKU)。

  - 所有的伺服器憑證必須包含一個 CRL 發佈點 (CDP)。

  - 所有的憑證必須使用作業系統支援的簽署演算法簽署。 Lync Server 2013 支援摘要大小 (224、256、384 和 512 位元) 同時符合或超過作業系統需求的 SHA-1 和 SHA-2 套件。如需作業系統支援，請參閱 [http://go.microsoft.com/fwlink/?LinkId=287002](http://go.microsoft.com/fwlink/?linkid=287002)。

  - 執行 Lync Server 的內部伺服器支援自動註冊。

  - Lync Server Edge Server 不支援自動註冊。

  - 當您將 Web 憑證要求提交至 Windows Server 2003 CA 時，您必須從執行 Windows Server 2003 (SP2) 或 Windows XP 的電腦進行提交。
    
    請注意，雖然 KB922706 可支援解決 Windows Server 2003 憑證服務的網頁註冊功能引發的網頁憑證註冊問題，但仍無法使用 Windows Server 2008、Windows Vista 或 Windows 7 向 Windows Server 2003 CA 要求憑證。

  - 支援的加密金鑰長度為 1024、2048 和 4096。建議的金鑰長度為 2048 和以上。

  - 預設的摘要或雜湊簽署演算法為 RSA。同時也支援 ECDH\_P256、ECDH\_P384 和 ECDH\_P521 演算法。

## 本章節內容

  - [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)

  - [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)

  - [Lync Server 2013 中的常設聊天室伺服器的憑證需求](lync-server-2013-certificate-requirements-for-persistent-chat-server.md)

  - [Lync Server 2013 中的行動憑證需求](lync-server-2013-certificate-requirements-for-mobility.md)


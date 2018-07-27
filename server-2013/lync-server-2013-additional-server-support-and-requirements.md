---
title: Lync Server 2013：其他伺服器支援和需求
TOCTitle: 其他伺服器支援和需求
ms:assetid: 7622986b-abd6-4f45-8b5b-d5e2368521e8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398577(v=OCS.15)
ms:contentKeyID: 49291357
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的其他伺服器支援和需求

 

_**上次修改主題的時間：** 2013-12-09_

除了此支援文件的其他小節所述的軟體支援以外， Lync Server 2013 還具有下列支援限制：

  - Lync Server 2013 支援對特定伺服器角色使用網域名稱系統 (DNS) 和硬體負載平衡。也支援對中繼伺服器使用應用程式負載平衡 (若情況允許)。如需各項目使用時機的詳細資訊，請參閱規劃文件。

  - Lync Server 2013 使用 Distribution List Expansion Protocol (DLX) 來展開通訊群組清單。此通訊協定也會指定為了取得通訊群組清單的成員資格而使用的 Web 服務方法。 Microsoft Exchange Server 支援動態群組，亦即不靜態指派成員的群組。這些群組中儲存在展開群組時才會評估的查詢。DLX 不支援動態通訊群組清單。

  - \[啟用使用者精靈\] 不支援自動將非英文字元轉換成符合 SIP 標準的 URI，因此您必須手動修改 SIP 位址。

  - 對於執行防毒軟體的伺服器，請參閱 [Lync Server 2013 的防毒掃描排除項目](lync-server-2013-antivirus-scanning-exclusions.md)，以取得病毒排除建議與其他安全性相關建議。

  - 如果您有使用 IPsec，我們建議您針對音訊與視訊流量所使用的連接埠範圍停用 IPsec。如需詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的 IPsec 例外](lync-server-2013-ipsec-exceptions.md)＞。

  - 如果您的組織使用的是服務品質 (QoS) 基礎結構，則媒體子系統將會設計成配合此現有基礎結構運作。如需實作 QoS 的詳細資訊，請參閱作業文件中的＜ [在 Lync Server 2013 中管理服務品質 (QoS)](lync-server-2013-managing-quality-of-service-qos.md)＞。

  - 支援使用作業系統防火牆。 Lync Server 2013 會管理作業系統防火牆的防火牆例外，但 Microsoft SQL Server 資料庫軟體除外。如需 SQL Server 防火牆需求的詳細資訊，請參閱 SQL Server 文件。

  - 用來實作外部使用者存取支援的外部介面必須位於個別子網路，而非 與內部介面位於相同網路。

  - Microsoft 已測試過 Lync Server 2013 的 XMPP 功能，確定其可與 Google Talk 建立立即訊息同盟，而 Microsoft 也會負責這項功能的支援工作。對於其他 XMPP 系統，請連絡第三方廠商，確認其系統是否能與 Lync Server 2013 建立同盟，以及其是否有任何部署或疑難排解方面的建議。

  - 發行 Lync Server 2013 累計更新：2013 年 7 月後， Lync Server 2013 現已支援雙因素驗證。如需更多資訊，請參閱＜ [Lync Server 2013 中的雙因素驗證](lync-server-2013-planning-for-and-deploying-two-factor-authentication.md)＞。

  - 大多數的內部伺服器需要定義為 **開放驗證** (OAuth) 的憑證類型。您必須在 Lync Server 部署精靈的 **要求、安裝及指派驗證**階段，要求並指派一個 OAuth 憑證。OAuth 憑證金鑰大小的下限為 1024 位元。如果您請求的憑證金鑰長度小於 2048 位元，可能會顯示警告。在 2048 長度位元的金鑰強制執行而非出現警告時，為了避免潛在的問題發生，我們強烈建議您針對 OAuth 憑證使用 2048 位元金鑰長度。

  - 如果 Windows Server 2008 R2 作業系統設定為使用 FIPS 140-2 演算法進行系統密碼編譯， Lync Server 2013 和 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 在運作時即支援美國聯邦資訊處理標準 (FIPS) 140-2 演算法。若要實作 FIPS 支援，您必須設定每部執行 Lync Server 2013 的伺服器以支援。如需 FIPS 相容演算法以及如何實作 FIPS 支援的詳細資訊，請參閱 Microsoft 知識庫文章 811833，＜Windows XP 和 Windows 更新版本中的「系統密碼編譯：使用 FIPS 相容演算法進行加密、雜湊與簽署」安全性設定的影響＞，網址為 <http://support.microsoft.com/kb/811833>。如需 Exchange 2010 中 FIPS 140-2 支援與限制的詳細資訊，請參閱＜Exchange 2010 SP1 與 FIPS 相容演算法的支援＞，網址為 <http://go.microsoft.com/fwlink/?linkid=205335>。

在部署 Lync Server 2013 之前或部署期間，必須對特定元件安裝其他軟體。這些軟體包括作業系統隨附的軟體、可下載的軟體，以及會在 Lync Server 2013 安裝期間自動安裝的軟體。以下列出其他可能需要的軟體：

  - Windows Update

  - Windows Identity Foundation

  - Microsoft .NET 4.5 Framework

  - Microsoft Visual C++ 2012 可轉散發套件
    
    > [!NOTE]  
    > 當您安裝 Lync Server 2013 時，已自動安裝 Microsoft Visual C++ 2012 可轉散發套件。請勿安裝及使用任何其他版本。
    


  - URL Rewrite Module Version 2.0 可轉散發套件

  - Windows Media Format Runtime

  - Windows PowerShell 3.0 版

  - Microsoft Silverlight 4 瀏覽器外掛程式 (Lync Server 控制台需要 Silverlight 4.0.50524.0 或最新的版本)

  - Active Directory 網域服務 工具

其中有些軟體需求僅適用於特定伺服器角色或元件。如需這些軟體需求的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)＞。


---
title: 建立登錄器組態設定
TOCTitle: 建立登錄器組態設定
ms:assetid: eddfbdd2-cfd0-4c03-986e-443d6728db7d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182601(v=OCS.15)
ms:contentKeyID: 49292734
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立登錄器組態設定

 

_**上次修改主題的時間：** 2013-03-17_

您可以使用登錄器設定 Proxy 伺服器驗證方法。您指定的驗證通訊協定會決定集區中的伺服器對用戶端發出的挑戰類型。可用的通訊協定包括：

  - **Kerberos**   這是用戶端可以使用的最強密碼式驗證配置，但通常僅供企業用戶端使用，因為它需要用戶端連線到金鑰發佈中心 (Kerberos 網域控制站)。如果伺服器只驗證企業用戶端，這種設定就比較適合。

  - **NTLM**   這是密碼式驗證，可供在密碼上使用挑戰/回應雜湊配置的用戶端使用。此驗證是唯一可供沒有金鑰發佈中心 (Kerberos 網域控制站) 連線能力的用戶端 (例如遠端使用者) 使用的驗證類型。如果伺服器僅驗證遠端使用者，則您應該選擇 NTLM。

  - **憑證驗證**   這是新的驗證方法，會在伺服器需要從 Lync Phone Edition 用戶端、公共區域電話和 Lync 2013 取得憑證時使用。在 Lync Phone Edition 用戶端上，使用者登入並透過提供個人識別碼 (PIN) 成功驗證之後，Lync Server 2013 接著會將 SIP URI 提供給電話，並且佈建 Lync Server 簽署的憑證或使用者憑證，以便讓電話識別 Joe (例如：SN=joe@contoso.com )。此憑證用於對登錄器和 Web 服務進行驗證。

> [!NOTE]  
> 當伺服器支援遠端與企業用戶端的驗證時，我們建議您同時啟用 Kerberos 和 NTLM。Edge Server 和內部伺服器將進行通訊，以確認只提供 NTLM 驗證給遠端用戶端。如果只在這些伺服器上啟用 Kerberos，則伺服器將無法驗證遠端使用者。如果企業使用者也對伺服器進行驗證，則會使用 Kerberos。



請依照下列步驟建立新的登錄器。

## 若要建立登錄器

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[安全性\]**，然後按一下 **\[登錄器\]**。

4.  在 **\[登錄器\]** 頁面上，按一下 **\[新增\]**

5.  在 \[選取服務\] 中，按一下要套用登錄器的服務，然後按一下 \[確定\]。

6.  在 **\[新增登錄器設定\]** 中，依據用戶端的功能和您環境中的支援，選取下列其中一個或多個項目：
    
      - **\[啟用 Kerberos 驗證\]** 以讓集區中的伺服器使用 Kerberos 驗證來提出質詢。
    
      - **\[啟用 NTLM 驗證\]** 以讓集區中的伺服器使用 NTLM 驗證來提出質詢。
    
      - **\[啟用憑證驗證\]** 以讓集區中的伺服器核發憑證給用戶端。

7.  按一下 **\[認可\]**。


---
title: 在 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 中設定夥伴應用程式
TOCTitle: 在 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 中設定夥伴應用程式
ms:assetid: 9c3a3054-6201-433f-b128-4c49d3341370
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688151(v=OCS.15)
ms:contentKeyID: 49890225
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 中設定夥伴應用程式

 

_**上次修改主題的時間：** 2014-11-05_

伺服器對伺服器驗證通常牽涉到三個實體：兩部需要彼此通訊的伺服器，以及第三方安全性權杖伺服器。如果兩部伺服器 (例如伺服器 A 和伺服器 B) 需要通訊，這兩部伺服器一開始的動作都是連絡權杖伺服器並取得彼此信任的安全性權杖。接著伺服器 A 向伺服器 B 出示安全性權杖 (反之亦然)，以保證自己身分的真實性和可信度。

但是，那只是一般規則。Lync Server 2013、Microsoft Exchange Server 2013 及 Microsoft SharePoint Server 2013 彼此通訊時並不需要使用第三方權杖伺服器，這是因為這些伺服器產品可以建立彼此都接受的安全性權杖，而不需要另外借助權杖伺服器。(此功能只適用於 Lync Server 2013、Exchange 2013 及 SharePoint Server 2013。如果您需要設定與其他伺服器的伺服器對伺服器驗證，包括其他 Microsoft 伺服器產品，則您需要使用第三方權杖伺服器。)

若要設定 Lync Server 和 Exchange 之間的伺服器對伺服器驗證，您必須執行兩個動作：1) 指派適當的憑證給每部伺服器；以及 2) 將每部伺服器設定為另一部伺服器的夥伴應用程式：這表示您必須將 Lync Server 2013 設定為 Exchange 2013 的夥伴應用程式，並且必須將 Exchange 2013 設定為 Lync Server 2013 的夥伴應用程式。

## 將 Lync Server 2013 設定為 Exchange 2013 的夥伴應用程式

將 Lync Server 2013 設定為 Exchange 2013 的夥伴應用程式最簡單的方式是執行 Configure-EnterprisePartnerApplication.ps1 指令碼，這是 Exchange 2013 隨附的 Windows PowerShell 指令碼。若要執行此指令碼，您必須提供 Lync Server 驗證中繼資料文件的 URL，通常是 SharePoint 集區的完整網域名稱，後面加上尾碼 /metadata/json/1。例如：

    https://atl-cs-001.litwareinc.com/metadata/json/1

若要設定 Lync Server 作為夥伴應用程式，請開啟 Exchange 管理命令介面，然後執行如下的命令 (假設 Exchange 已安裝在 C: 磁碟機且使用預設資料夾路徑)：

    "C:\Program Files\Microsoft\Exchange Server\V15\Scripts\Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl 'https://atl-cs-001.litwareinc.com/metadata/json/1' -ApplicationType Lync"

設定夥伴應用程式之後，建議您在 Exchange 信箱與用戶端存取伺服器上停止再重新啟動 Internet Information Services (IIS)。您可以使用如下的命令來重新啟動 IIS，該命令會在電腦 atl-exchange-001 上重新啟動服務：

    iisreset atl-exchange-001

您可以從 Exchange 管理命令介面執行此命令，或從任何其他以系統管理員權限執行的命令視窗執行此命令。

## 將 Exchange 2013 設定為 Lync Server 2013 的夥伴應用程式

將 Lync Server 2013 設定為 Exchange 2013 的夥伴應用程式之後，您必須將 Exchange 設定為 Lync Server 的夥伴應用程式。這可以藉由使用 Lync Server 管理命令介面以及指定 Exchange 的驗證中繼資料文件來完成，後者通常是 Exchange 自動探索服務的 URI，後面加上尾碼 /metadata/json/1。例如：

    https://autodiscover.litwareinc.com/autodiscover/metadata/json/1

Lync Server 中是使用 [New-CsPartnerApplication](new-cspartnerapplication.md) Cmdlet 來設定夥伴應用程式。除了指定中繼資料 URI 之外，您也應該將應用程式信任層級設定為「完全信任」；這樣可以讓 Exchange 同時代表自己和領域中的任何授權使用者。例如：

    New-CsPartnerApplication -Identity Exchange -ApplicationTrustLevel Full -MetadataUrl "https://autodiscover.litwareinc.com/autodiscover/metadata/json/1"

或者，您也可以複製及修改在 Lync Server 2013 伺服器對伺服器驗證文件中找到的指令碼，來建立夥伴應用程式。如需詳細資訊，請參閱＜[在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)＞一文。

如果您已成功為 Lync Server 和 Exchange 設定夥伴應用程式，表示您也已成功設定這兩項產品之間的伺服器對伺服器驗證。Lync Server 2013 包含名為 [Test-CsExStorageConnectivity](test-csexstorageconnectivity.md) 的 Windows PowerShell Cmdlet，可以讓您確認伺服器對伺服器驗證是否已正確設定，以及 Lync Server 存放服務是否可以連線至 Exchange 2013。此 Cmdlet 完成此動作的方式是連線至 Exchange 2013 使用者的信箱，在該使用者的 \[交談記錄\] 資料夾中寫入一個項目，然後 (選擇性地) 刪除該項目。

若要測試 Lync Server 2013 和 Exchange 2013 的整合，請從 Lync Server 管理命令介面執行如下的命令：

    Test-CsExStorageConnectivity -SipUri "sip:kenmyer@litwareinc.com"

在上述命令中，SipUri 代表在 Exchange 2013 具有帳戶之使用者的 SIP 位址；您的命令會失敗，因為這不是有效的使用者帳戶。

如果測試成功且建立連線，您就可以繼續設定選用功能，例如封存整合和整合連絡人存放區。


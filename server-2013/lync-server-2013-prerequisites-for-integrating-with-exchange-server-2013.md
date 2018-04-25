---
title: 整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 的先決條件
TOCTitle: 整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 的先決條件
ms:assetid: ea22beb9-c02e-47cb-836d-97a556969052
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721919(v=OCS.15)
ms:contentKeyID: 49890369
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 的先決條件

 

_**上次修改主題的時間：** 2014-04-22_

整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 前，您必須確實完成所有先決條件步驟。您可能已猜到，除非 Exchange 2013 與 Lync Server 2013 皆已完全安裝，且啟動並執行，否則將無法執行整合。有關安裝 Exchange 的詳細資訊，請參閱 Exchange 2013 規劃與部署文件 (英文)，網址為：[http://go.microsoft.com/fwlink/?linkid=268539\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268539%26clcid=0x404)。有關安裝 Lync Server 2013 的詳細資訊，請參閱規劃與部署文件 (英文)，網址為：[http://go.microsoft.com/fwlink/?linkid=254806\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=254806%26clcid=0x404)。

伺服器啟動並執行後，您必須指派伺服器對伺服器驗證憑證到 Lync Server 2013 與 Exchange 2013；這些憑證允許 Lync Server 與 Exchange 交換資訊，並與他人通訊。安裝 Exchange 2013 時，系統會建立一個名為 Microsoft Exchange Server Auth Certificate 的自我簽署憑證。此憑證 (位於本機電腦憑證存放區) 應用於 Exchange 2013 的伺服器對伺服器驗證。有關在 Exchange 2013 指派憑證的詳細資訊，請參閱「設定郵件流程與用戶端存取」(英文)，網址為：[http://go.microsoft.com/fwlink/?linkid=268540\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268540%26clcid=0x404)。

若使用 Lync Server 2013，您可使用現有的 Lync Server 憑證，當作伺服器對伺服器驗證憑證；例如您的預設憑證也可當作 OAuthTokenIssuer 憑證。Lync Server 2013 可讓您將網頁伺服器憑證當作伺服器對伺服器驗證的憑證，但前提是：

  - 憑證要包含主體欄位中 SIP 網域名稱。

  - 在所有前端伺服器中，將同一個憑證設為 OAuthTokenIssuer 憑證。

  - 憑證的長度至少要有 2048 個位元。

如需詳細了解 Microsoft Lync Server 2013 的伺服器對伺服器驗證憑證，請參閱＜[將伺服器對伺服器驗證憑證指派給 Microsoft Lync Server 2013](lync-server-2013-assigning-a-server-to-server-authentication-certificate-to-lync-server-2013.md)＞。

指派憑證後，您必須設定 Exchange 2013 的自動探索服務。在 Exchange 2013 中，自動探索服務會在使用者登入系統時設定使用者設定檔，並提供 Exchange 服務之存取。使用者向自動探索服務出具電子郵件位址與密碼，服務將會向使用者提供下列資訊：

  - 內部與外部連線到 Exchange 2013 的連線資訊。

  - 使用者郵件信箱伺服器的位置。

  - Outlook 功能的 URL，例如有空/忙碌資訊、整合通訊與離線通訊錄。

  - Outlook Anywhere 伺服器設定。

自動探索服務必須在整合 Lync Server 2013 與 Exchange 2013 前設定。要確認是否已設定自動探索服務，請從 Exchange Management Shell 執行下列命令，並檢查 AutoDiscoverServiceInternalUri 屬性值：

    Get-ClientAccessServer | Select-Object Name, AutoDiscoverServiceInternalUri | Format-List

若此值為空白，您必須指派 URI 到自動探索服務。通常此 URI 看起來像這樣：

    https://autodiscover.litwareinc.com/autodiscover/autodiscover.xml

要指派自動探索 URI，您可執行類似這樣的命令：

    Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri "https://autodiscover.litwareinc.com/autodiscover/autodiscover.xml"

有關自動探索服務的詳細資訊，請參閱「了解自動探索服務」(英文)，網址為：[http://go.microsoft.com/fwlink/?linkid=268542\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268542%26clcid=0x404)。

設定自動探索服務後，您必須修改 Lync Server OAuth 組態設定值；這樣可確認 Lync Server 知道該去何處尋找自動探索服務。要修改 Lync Server 2013 的 OAuth 組態設定值，請在 Lync Server 管理命令介面內執行下列命令。執行此命令時，請務必指定 URI 到 Exchange 伺服器正在執行的自動探索服務，以及指向服務位置的是 **autodiscover.svc**，而不是 **autodiscover.xml** (這個指向服務所使用的 XML 檔案)：

    Set-CsOAuthConfiguration -Identity global -ExchangeAutodiscoverUrl "https://autodiscover.litwareinc.com/autodiscover/autodiscover.svc

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>前置命令中的身分識別參數可省略；因為 Lync Server 只能讓您擁有一個 OAuth 組態設定值的單一全域集合。除此之外，這代表您可使用較簡單的命令設定自動探索 URL：<br />
Set-CsOAuthConfiguration–ExchangeAutodiscoverUrl &quot;https://autodiscover.litwareinc.com/autodiscover/autodiscover.svc&quot;<br />
若不熟悉此技術，OAuth 是各大網站使用的標準授權通訊協定。有了 OAuth，使用者認證與密碼就不會在電腦之間傳送，而是根據安全性權杖的交換進行驗證與授權；這些權杖會授與存取權，讓您在特定時間長度內存取特定資源集合。</td>
</tr>
</tbody>
</table>


除了設定自動探索服務，您還必須為指向 Exchange 伺服器的服務建立 DNS 記錄。例如，若自動探索服務的位置在 autodiscover.litwareinc.com，您必須為 autodiscover.litwareinc.com (解析到 Exchange 伺服器的完整網域名稱) 建立 DNS 記錄 (例如 atl-exchange-001.litwareinc.com)。


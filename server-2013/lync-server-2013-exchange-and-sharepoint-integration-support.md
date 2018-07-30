---
title: Lync Server 2013：Exchange Server 與 SharePoint 整合支援
TOCTitle: Exchange Server 與 SharePoint 整合支援
ms:assetid: 72bf8aa5-55b1-4851-8a59-c96bf85d215a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205005(v=OCS.15)
ms:contentKeyID: 49291298
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Exchange Server 與 SharePoint 整合支援

 

_**上次修改主題的時間：** 2014-09-29_

如果您整合 Lync Server 2013 和 Lync 2013，這些產品可以安全又順暢地與其他應用程式及伺服器產品通訊，包括 Office 2013、Exchange 2013 及 SharePoint。將 Lync Server 2013 與 Office 整合在一起後，使用者就能直接在環境中存取 Lync 的立即訊息 (IM)、改良過的目前狀態、電話語音和會議功能。Office 使用者可從 Outlook 2013 訊息和共同作業用戶端及其他 Office 程式，或是從 Microsoft SharePoint Server 2010 頁面使用 Lync 功能。使用者亦可在 Outlook \[歷程記錄\] 資料夾中檢視 Lync 交談記錄。Lync Server 2013 與 Exchange 2013 和 Exchange Online 整合後，可支援下列作業：

  - 整合的連絡人存放區：可讓使用者將所有連絡人資訊儲存於 Exchange 2013 或 Exchange Online 中，以便在 Lync 2013、Exchange、Outlook 和 Outlook Web App 中全域提供該資訊。

  - 儲存於 Exchange 使用者資料夾的交談記錄和 Web 會議歷程記錄。

  - 從 Lync 封存的內容 (例如 IM 和會議內容) 可儲存於 Exchange 儲存體。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 支援與舊版的 Microsoft Exchange Server 和 SharePoint 進行整合，但這些先前版本並不支援所有功能，例如封存存放區與 Microsoft Exchange 的整合。<br />
如果將使用者移轉至 Exchange 2013，在您完成移轉的時候，便可暫時使用 Exchange 存放區及 Lync Server 存放區。 Exchange 及 Lync Server 存放區不支援永久使用。</td>
</tr>
</tbody>
</table>


Lync Server 2013、 Exchange 2013 以及 SharePoint Server 的整合需要執行 Lync Server 2013、 Microsoft Exchange Server 和 SharePoint Server 之伺服器之間的伺服器對伺服器驗證。 Lync Server 2013 可支援伺服器對伺服器驗證及授權的 OAuth (Open Authorization) 通訊協定。針對 Microsoft 伺服器之間的內部部署伺服器對伺服器驗證，並不需要使用協力廠商 Token 伺服器。 Lync Server 2013、 Exchange 2013 和 SharePoint 具有可用於彼此相互驗證的內建 Token 伺服器。例如， Lync Server 2013 可自行發行和簽署安全性 Token，以及可在與 Exchange 2013 通訊之時使用該 Token。在此情況下，則不需要使用協力廠商 Token 伺服器。

Lync Server 2013 支援兩種伺服器對伺服器驗證案例，包括下列項目之間的伺服器對伺服器驗證設定：

  - Lync Server 2013 內部部署安裝及 Exchange 2013 內部部署安裝及/或 SharePoint Server。

  - 一對 Office 元件 (例如，Microsoft Exchange 365 和 Microsoft Lync Server 365 之間或 Microsoft Lync Server 365 和 Microsoft SharePoint 365 之間)。

> [!NOTE]  
> 此 Lync Server 2013 版本不支援內部部署伺服器和 Office 365 元件之間的伺服器對伺服器驗證。除此之外，這表示您無法在 Lync Server 2013 和 Microsoft Exchange 365 之間的內部部署安裝設定伺服器對伺服器驗證。



如需有關伺服器對伺服器驗證的詳細資訊，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)。


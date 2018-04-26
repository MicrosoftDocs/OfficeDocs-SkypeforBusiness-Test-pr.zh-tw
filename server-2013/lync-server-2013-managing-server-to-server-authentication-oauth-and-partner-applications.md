---
title: 在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式
TOCTitle: 在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式
ms:assetid: 38848373-c8c6-4097-bf7f-699fe471348d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204817(v=OCS.15)
ms:contentKeyID: 49290604
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式

 

_**上次修改主題的時間：** 2015-05-14_

Microsoft Lync Server 2013 必須能夠安全且順暢地與其他應用程式及伺服器產品通訊。例如，您可以設定 Lync Server 2013，將連絡人資料及 (或) 封存資料儲存在 Microsoft Exchange Server 2013；但是，這只有在 Lync Server 及 Exchange 能夠安全互相通訊的情況下，才有可能達成。同樣地，您可以在 Microsoft SharePoint Server 中排程 Lync Server 會議；但是，也只有在這兩部伺服器 ((SharePoint 及 Lync Server) 互相信任的情況下，這才有辦法達成。雖然可以針對 Lync 對 Exchange 通訊使用一種驗證機制，而針對 Lync 對 SharePoint 通訊使用另外一種機制，更好又更有效的方式為針對所有伺服器對伺服器的驗證及授權使用標準化方法。

Lync Server 2013 採取的方式就是使用單一、標準化的伺服器對伺服器驗證方法。2013 版本的 Lync Server 2013 (以及其他 Microsoft 伺服器產品，包括 Exchange 2013 及 Microsoft SharePoint Server) 針對伺服器對伺服器驗證及授權，支援 OAuth (開放授權) 通訊協定。藉由 OAuth (一些主要網站皆使用的標準授權通訊協定)，使用者認證及密碼並不會在電腦間傳遞。驗證及授權是基於安全性權杖的交換，這些權杖會授與一段特定時間內一組特定資源的存取權。

OAuth 驗證通常涉及三方：單一授權伺服器及兩個需要互相通訊的領域。(伺服器對伺服器驗證也可不使用驗證伺服器，本文件稍後會討論此一程序。) 授權伺服器 (亦稱為安全性權杖伺服器) 會發行安全性權杖給兩個需要通訊的領域；這些證明通訊來自其中一方領域的權杖應受另一方領域的信任。例如，授權伺服器可發行權杖以證明從特定 Lync Server 2013 領域的使用者可存取指定的 Exchange 2013 領域，反之亦然。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>領域只是安全性容器。依據預設，Lync Server 2013 使用預設的 SIP 網域作為 OAuth 領域。</td>
</tr>
</tbody>
</table>


Lync Server 2013 支援三種伺服器對伺服器驗證狀況。透過 Lync Server 2013 您可以處理下列情況：

  - 設定 Lync Server 2013 的內部安裝以及 Exchange 2013 和 (或) Microsoft SharePoint Server 的內部安裝兩者之間的伺服器對伺服器驗證。

  - 設定一對 Office 365 元件 (例如，Microsoft Exchange 及 Microsoft Lync Server，或者 Microsoft Lync Server 及 Microsoft SharePoint) 之間的伺服器對伺服器驗證。

  - 設定跨單位環境下伺服器對伺服器驗證 (亦即內部安裝伺服器及 Office 365 元件之間的伺服器對伺服器驗證)。

請注意：目前只有 Exchange 2013、SharePoint Server 及 Lync Server 2013 支援伺服器對伺服器驗證；如果並非執行這些伺服器，則無法完全實作 OAuth 驗證。

此外，使用伺服器對伺服器驗證並非必要，部署 Lync Server 2013 並不需要伺服器對伺服器驗證。如果 Lync Server 2013 不需要與其他伺服器通訊 (例如 Exchange 2013)，則不需要伺服器對伺服器驗證。

然而，如果要使用 Lync Server 某些新功能 (例如，整合連絡人存放區)，則需要伺服器對伺服器驗證。透過整合連絡人存放區，Lync Server 2013 連絡人資訊會儲存在 Exchange 2013，而不是在 Lync Server；這讓使用者有單一組的連絡人，且從 Lync、Microsoft Outlook 或 Microsoft Outlook Web Access 皆可存取。因為整合連絡人存放區需要 Lync Server 2013 與 Exchange 2013 共用資訊，所以必須使用伺服器對伺服器驗證，才能部署該功能。如果選擇使用 Exchange 封存，則也需要伺服器對伺服器驗證，因為立即訊息工作階段的文字記錄會儲存為 Exchange 2013 電子郵件，而非個別資料庫記錄。

如果 Lync Server 的 Office 365 版本要與 Exchange 的 Office 365 版本通訊，Lync Server 2013 必須先從授權伺服器取得安全性權杖。然後，Lync Server 會使用該安全性權杖向 Exchange 識別自己的身分。Exchange 的 Office 365 版本必須以同樣的方式才能與 Lync Server 2013 通訊。

不過，對於兩部 Microsoft 伺服器之間的內部部署伺服器對伺服器驗證，則不需要使用協力廠商權杖伺服器。像 Lync Server 2013 及 Exchange 2013 伺服器產品有內建的權杖伺服器，可用於與其他支援伺服器對伺服器驗證的 Microsoft 伺服器 (例如 SharePoint Server) 作為驗證之用。例如，Lync Server 2013 可自己發行並簽署安全性權杖，然後使用該權杖與 Exchange 2013 通訊。在此情況下，不需要協力廠商權杖伺服器。

如要針對內部部署實作的 Lync Server 2013 設定伺服器對伺服器驗證，必須完成下列兩項動作：

  - 指派憑證給 Lync Server 內建的權杖發行者。

  - 將 Lync Server 2013 要通訊的伺服器設定為「協力廠商應用程式」。例如，如果 Lync Server 2013 需要與 Exchange 2013 通訊，則需要將 Exchange 設定為協力廠商應用程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>「協力廠商應用程式」是不需透過協力廠商安全性權杖伺服器，就能與 Lync Server 2013 直接交換安全性權杖的任何應用程式。</td>
</tr>
</tbody>
</table>


請注意，OAuth 是產品的核心部分，無法停用或移除。

## 請參閱

#### 概念

[將伺服器對伺服器驗證憑證指派給 Microsoft Lync Server 2013](lync-server-2013-assigning-a-server-to-server-authentication-certificate-to-lync-server-2013.md)  
[在跨單位環境中設定 Microsoft Lync Server 2013](lync-server-2013-configuring-lync-server-in-a-cross-premises-environment.md)


---
title: Lync Server 2013：整合 Microsoft Exchange Server 2013
TOCTitle: 整合 Lync Server 2013 與 Exchange Server 2013
ms:assetid: 795dc1c6-524f-4012-8b66-103b55198044
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688098(v=OCS.15)
ms:contentKeyID: 49890127
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013

 

_**上次修改主題的時間：** 2014-07-09_

Exchange 和 Lync Server 在相容性和整合方面已有很長的歷史。此項整合在其各自的用戶端應用程式內是最受矚目的。例如，Microsoft Outlook 中可以報告 Lync 目前狀態資訊；同理， Lync 可以使用 Outlook 行事曆，自動更新該Microsoft Outlook 中 (例如，Lync 隨時可將您的狀態變更為 \[忙碌\]，讓您的行事曆顯示您已排程會議)。儘管您不需要為了執行 Lync Server 而執行 Exchange (反之亦然)， 還是會有點懷疑將這兩個產品一起使用是否象徵「充分整合，功能升級」一詞的完美定義。

此情況特別適用於 Microsoft Lync Server 2013 的版本和 Microsoft Exchange Server 2013。除了像是整合訊息和 IM 與目前狀態等可在 Microsoft Exchange Server 2010 與 Microsoft Lync Server 2010 中找到的功能之外，伺服器產品的 2013 年版本還會包含一些新功能。這些功能包含下列項目：

  - **Lync 封存整合** 。在 Lync Server 2013 中，系統管理員仍然可以選擇將立即訊息和 Web 會議文字記錄封存至 SQL Server (與在 Lync Server 2010 中封存這些文字記錄相同的方式)。或者，儘管如此，系統管理員還是可以選擇將文字記錄封存至 Exchange 2013，使用與 Exchange 用來封存通訊的相同方式，在個別使用者信箱中儲存這些文字記錄。這表示適用於您所有電子通訊 (來自 Exchange 與 Lync Server) 的單一儲存機制，讓您能夠在需求產生時，更容易搜尋與擷取這些封存的通訊。

  - **整合的連絡人存放區** 。在 Lync Server 2010 中，使用者必須維護 Outlook 和 Lync 中的個別連絡人清單；事實上，若要確定您在這兩個產品中擁有相同的連絡人，您必須維護重複的連絡人清單，一個用於 Outlook，另一個用於 Lync。但是，利用 Lync Server 2013，使用者連絡人可以儲存於 Exchange 2013 和整合的連絡人存放區中。使用單一連絡人存放區，讓使用者能夠只維護一組連絡人，與可以在 Lync 2013、Outlook 2013 及 Outlook Web Access 2013 中取得連絡人組相同。

  - **從 OWA 排程的 Lync 會議** 。整合 Lync Server 2013 與 Exchange 2013 之後，使用者可以排程來自 Outlook Web Access 2013 的 Lync 會議。

  - **高解析度相片** 。 Lync 2010 僅能顯示您連絡人的小型相片；這是因為這些相片都是儲存於 Active Directory 中，而 Active Directory 在儲存的相片上加入了 48 像素 x 48 像素的大小限制。但是，使用 Lync Server 2013，相片可以儲存於 Microsoft Exchange；其允許和 648 像素 x 648 像素一樣大的高解析度相片。如您所預期， Lync 2013 已升級，可允許顯示這些高解析度相片。

請記住，這些新功能需要同時使用 Lync Server 2013 和 Exchange 2013。除了這一點之外，希望利用這些新功能的使用者必須在 Lync Server 2013 和 Exchange 2013 上有帳戶，而且必須使用最新版的用戶端軟體 (例如 Lync 2013)。例如，整合的連絡人存放區不適用已位於 Lync Server 2010 的使用者；同理，高解析度的相片無法在 Lync 2010 中顯示。

本文件提供整合 Lync Server 2013 和 Exchange 2013 的相關資訊，包含啟用像是封存整合與整合連絡人存放區等新功能的逐步資訊。本文件不會討論這兩個產品的初始安裝與設定。如需有關部署 Lync Server 2013 的詳細資訊，請參閱 Lync Server 2013 Tech Center，網址為 [http://go.microsoft.com/fwlink/?linkid=246127\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=246127%26clcid=0x404)。如需有關部署 Exchange 2013 的詳細資訊，請參閱 Exchange 2013 Tech Center，網址為 [http://go.microsoft.com/fwlink/?linkid=268528\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268528%26clcid=0x404)。

## 本章節內容

[整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 的先決條件](lync-server-2013-prerequisites-for-integrating-with-exchange-server-2013.md)

[在 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013 中設定夥伴應用程式](lync-server-2013-configuring-partner-applications-in-lync-server-2013-and-exchange-server-2013.md)

[設定 Microsoft Lync Server 2013 使用 Microsoft Exchange Server 2013 Archiving](configuring-lync-server-2013-to-use-microsoft-exchange-server-2013-archiving.md)

[設定 Microsoft SharePoint Server 2013 搜尋已封存的 Microsoft Lync Server 2013 資料](lync-server-2013-configuring-microsoft-sharepoint-server-2013-to-search-for-archived-lync-server-2013-data.md)

[設定 Microsoft Lync Server 2013 使用整合連絡人存放區](lync-server-2013-configuring-lync-server-to-use-the-unified-contact-store.md)

[設定在 Microsoft Lync Server 2013 中使用高解析度相片](lync-server-2013-configuring-the-use-of-high-resolution-photos.md)

[針對 Microsoft Lync Server 2013 Voicemail 設定 Microsoft Exchange Server 2013 Unified Messaging](lync-server-2013-configuring-microsoft-exchange-server-2013-unified-messaging-for-lync-server-2013-voice-mail.md)

[整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013](lync-server-2013-integrating-lync-server-and-outlook-web-app-2013.md)


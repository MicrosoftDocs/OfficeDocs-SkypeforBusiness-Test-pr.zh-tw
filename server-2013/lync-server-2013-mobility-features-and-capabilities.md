---
title: Lync Server 2013：行動功能與性能
TOCTitle: 行動功能與性能
ms:assetid: 12517a88-2531-44a5-bea5-d8884aff53eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh689983(v=OCS.15)
ms:contentKeyID: 49290144
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的行動功能與性能

 

_**上次修改主題的時間：** 2013-02-19_

    The information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Lync Server 2013 累計更新 (2013 年 2 月) 所推出的行動功能支援 Lync 2010 Mobile 和 Lync 2013 Mobile 用戶端功能。當您部署 Lync Server 2013 Mobility Service 時，使用者可以使用支援的 Apple iOS、Android、Windows Phone 或 Nokia Symbian 行動裝置來執行傳送和接收立即訊息、檢視連絡人，以及檢視目前狀態之類的活動。此外，行動裝置還可支援部分企業語音功能，例如按一下加入會議、從公司撥號、單一號碼搜尋、語音信箱及未接來電。Lync Server 2013 累計更新 (2013 年 2 月) 所推出的新功能包括 Voice over IP (VoIP) 功能和會議出席者的視訊 (H.264)。

Lync Server 2013 累計更新 (2013 年 2 月) 所推出的行動功能支援 Lync 2013 Mobile 用戶端功能。Lync Server 2013 累計更新 (2013 年 2 月) 安裝 Unified Communications Web API (UCWA)。UCWA 是 Lync 2013 Mobile 用戶端所使用的元件。在 Lync Server 2013 中， Lync 2010 Mobile 用戶端則使用 Mcx。Lync Server 2013 累計更新 (2013 年 2 月) 推出 UCWA 做為行動服務新的進入點。 Lync Server 2013 會同時實作 Mobility Service (Mcx) (推出於 Lync Server 2010 累計更新 (2011 年 11 月))，並支援 Lync 2010 Mobile。部署 Lync Server 2013 累計更新 (2013 年 2 月) 之後，使用者即可使用支援的 Apple iOS、Android 及 Windows Phone 行動裝置執行下列活動︰

> [!IMPORTANT]  
> Lync Server 2010 累計更新 (2011 年 11 月) 的 Mobility Service 所支援之功能會標註 (Mcx)。推出於 Lync Server 2013 累計更新 (2013 年 2 月) 的 UCWA 支援所有列出的功能。



  - 傳送和接收立即訊息 (Mcx)

  - 檢視目前狀態 (Mcx)

  - 檢視連絡人 (Mcx)

  - 按一下加入會議 (Mcx)

  - 從公司撥號 (Mcx)

  - 單一號碼搜尋 (Mcx)

  - 語音信箱 (Mcx)

  - 未接來電通知 (Mcx)

  - Voice over IP (VoIP)

  - 出席者視訊 (H.264)

> [!NOTE]  
> Lync 2010 Mobile 提供 Nokia Symbian 裝置適用的用戶端。 Lync 2013 Mobile 則不會有 Nokia Symbian 裝置適用的用戶端。



Apple iPad 使用者將可存取增強型功能。使用音訊回撥加入會議之後，iPad 使用者將能夠檢視在會議中上傳的 Microsoft PowerPoint 簡報、共用應用程式和桌面、檢視會議參與者清單，以及接收會議中其他共用內容類型的通知。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用單一號碼搜尋時，使用者可以用行動電話接收撥打至公司號碼的電話。使用「從公司撥號」時，使用者可以使用公司電話號碼，而非行動電話號碼，從 Lync Mobile 用戶端撥打電話。若要撥出，用戶端會傳送要求給 Mcx 或 UCWA (視 Lync Mobile 版本而定) 以撥打電話。伺服器會起始通話，然後回撥給使用者的行動電話。當使用者接聽時，伺服器就會撥打給另一方，以完成通話。藉由使用「從公司撥號」，使用者可以在通話期間維持其公司身分識別，這表示受話者不會看到來電者的行動電話號碼，而且來電者可避免產生撥出電話的費用。</td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 並非所有功能在所有行動裝置上都會以完全相同的方式運作。如需行動裝置支援功能的詳細資訊，請參閱＜行動用戶端比較表＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=234777" class="uri">http://go.microsoft.com/fwlink/?linkid=234777</a>。如需支援裝置和作業系統的詳細資訊，請參閱＜ <a href="lync-server-2013-planning-for-mobile-clients.md">規劃 Lync Server 2013 中的行動用戶端</a>＞下的需求主題。



當您使用 Lync Server 2013 「自動探索」功能時，行動應用程式可以自動尋找 Lync Server 2013 Web 服務，而不需要使用者在其裝置設定中手動輸入 URL。也支援在行動裝置設定中手動輸入 URL，但主要是用於疑難排解。

> [!IMPORTANT]  
> Mcx 和 UCWA 為互補服務，兩者都部署為支援 Lync 2010 Mobile 和 Lync 2013 Mobile 用戶端。 Lync 2013 Mobile 無法登入 Lync Server 2010 部署。 Lync 2010 Mobile 和 Lync 2013 Mobile 可使用套用 Lync Server 2013 累計更新 (2013 年 2 月) 的 Lync Server 2013 部署。



對於不支援在背景執行應用程式的行動裝置，行動功能也可以支援「推播通知」 。推播通知是針對在行動應用程式為非使用中狀態時所發生的事件，傳送通知給行動裝置。例如，錯失的立即訊息 (IM) 邀請會產生推播通知。

Lync Server 2013 提供 Mcx、UCWA、自動探索服務及推播通知的支援。更新的用戶端功能和使用 UCWA 做為行動進入點都推出於 Lync Server 2013 累計更新 (2013 年 2 月)。


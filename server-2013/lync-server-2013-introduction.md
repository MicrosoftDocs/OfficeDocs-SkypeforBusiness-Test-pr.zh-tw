---
title: Lync Server 2013 簡介
TOCTitle: Lync Server 簡介
ms:assetid: 99dd6b65-e591-421f-852b-ee9fe9588998
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398795(v=OCS.15)
ms:contentKeyID: 49291763
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 簡介

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 和其用戶端軟體 (如 Lync 2013) 可讓使用者不論身在何處，都能夠以新的方式隨時保持聯繫。 Lync 和 Lync Server 將人們使用的各種不同通訊方式融入單一用戶端介面中。它們是採用整合式平台的部署形式，讓您能夠透過單一管理基礎結構管理它們。

下表和以下小節說明 Lync Server 提供給使用者的主要功能集或「工作負載」 。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>工作量</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IM 和目前狀態</p></td>
<td><p>立即訊息 (IM) 和目前狀態能協助使用者有效率地搜尋人員及進行通訊。</p>
<p>IM 提供具有交談記錄的立即訊息平台，並支援與公用 IM 網路 (如 MSN/Windows Live、Yahoo!、AOL 及 Google Talk) 上的使用者進行公用 IM 連線。</p>
<div class="alert">

> [!IMPORTANT]  
> <p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
> <p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
> ows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p>

</div>
<p>透過 [線上] 或 [忙碌] 等常見狀態以及 [馬上回來] 和 [請勿打擾] 等更詳細狀態的使用，目前狀態可建立並顯示使用者的個人空閒狀態和通訊意願。這項多樣化的目前狀態資訊能讓其他使用者立即做出有效率的通訊選擇。</p></td>
</tr>
<tr class="even">
<td><p>會議</p></td>
<td><p>Lync Server 含有適用於排程會議和即席會議的 IM 會議、音訊會議、Web 會議、視訊會議及應用程式共用等支援。這些類型的會議都能透過單一用戶端來支援。 Lync Server 亦支援電話撥入式會議，因此使用公用交換電話網路 (PSTN) 電話的使用者能透過聲音來參與會議。</p>
<p>您可以順暢地在第一時間內變更會議及提升會議的規模。例如，您可以即時將幾位使用者之間的立即訊息會議提升為啟用桌面共用並涉及多位與會者的音訊會議，操作簡單且毋須中斷交談流程。</p></td>
</tr>
<tr class="odd">
<td><p>企業語音</p></td>
<td><p>「 Enterprise Voice 」 是 Lync Server 的 Voice over Internet Protocol (VoIP) 功能。它提供的語音選項能強化或取代傳統的專用交換機 (PBX) 系統。Enterprise Voice 除了具備 IP PBX 的完整電話功能之外，還能與功能豐富的目前狀態、IM、共同作業及會議整合。諸如自動答錄、通話保留、繼續通話、通話轉接、來電轉接及通話轉移等功能均可直接支援。至於個人化的快速撥號鍵則取代為連絡人清單，而自動對講機則取代為 IM。</p>
<p>Enterprise Voice 能透過通話許可控制 (CAC)、分公司生存能力及資料恢復擴充選項來支援高可用性。</p></td>
</tr>
<tr class="even">
<td><p>遠端使用者支援</p></td>
<td><p>您可以將 Lync Server 的完整功能提供給目前位在組織防火牆之外的使用者，只要部署稱為 <em>Edge Server</em> 的伺服器以提供連線給這些遠端使用者即可。這些遠端使用者能利用已安裝 Lync 2013 的個人電腦、電話或 Web 介面來連接會議。</p>
<p>部署 Edge Server 亦能讓您與協力廠商或廠商組織 <em>結成同盟</em> 。同盟關係能讓使用者將同盟使用者加入連絡人清單、與這些使用者交換目前狀態資訊和立即訊息，以及邀請他們參與音訊通話、視訊通話及會議。</p></td>
</tr>
<tr class="odd">
<td><p>行動用戶端支援</p></td>
<td><p>另外，透過 Lync Server 行動服務，您的使用者可以在使用受支援的 Apple iOS、Android、Windows Phone 或 Nokia 行動裝置時存取 Lync 功能，並且執行如傳送和接收立即訊息、檢視連絡人以及檢視目前狀態等活動。此外，行動裝置可支援某些 Enterprise Voice 功能，例如按一下加入會議、從公司撥號、單一號碼搜尋、語音信箱及未接來電。對於不支援在背景執行應用程式的行動裝置，也可支援「推入通知」。</p></td>
</tr>
<tr class="even">
<td><p>與其他產品整合</p></td>
<td><p>Lync Server 能與其他數種產品整合，以提供額外的效益給使用者和系統管理員。</p>
<p>會議工具能整合到 Outlook 中，讓召集人只要按一下滑鼠就可以排程會議或啟動即席會議，而與會者也能輕鬆參加會議。</p>
<p>目前狀態資訊能整合到 Outlook 和 SharePoint 中。</p>
<p>Exchange 整合通訊 (UM) 提供數種整合功能。使用者能在 Lync Server 中查看是否有新的語音信箱訊息。他們能在 Outlook 訊息中按一下播放按鈕聆聽語音信箱音訊，或在通知訊息中檢視語音信箱訊息的文字記錄。</p>
<p>此外，搭配 Exchange 2013 執行 Lync Server 2013 可以啟用數項新功能，例如整合的連絡人存放區 (可同時供這兩項產品的用戶端存取)，以及儲存於 Exchange 2013 資料庫中的連絡人所享有的高解析度相片。</p></td>
</tr>
<tr class="odd">
<td><p>簡易部署</p></td>
<td><p>為了協助您進行伺服器和用戶端的規劃與部署， Lync Server 提供了 拓撲產生器。</p>
<p></p>
<p>拓撲產生器是 Lync Server 的安裝元件。您可以使用 拓撲產生器來建立、調整及發行所規劃的拓撲。它也能在開始安裝伺服器之前驗證您的拓撲。在將 Lync Server 安裝在個別的伺服器時，安裝程式會依照拓撲指示的方式部署伺服器。</p></td>
</tr>
<tr class="even">
<td><p>簡易管理</p></td>
<td><p>Lync Server 部署完成後，它便能提供下列功能強大且操作簡便的管理工具：</p>
<ul>
<li><p>中央組態管理，可以讓您集中管理變更，並且快速地將變更複寫到整個部署。</p></li>
<li><p>Lync Server 控制台，它是一款供系統管理員使用的 Web 型圖形使用者介面。透過這個 Web 型 UI， Lync Server 系統管理員可以從公司網路上的任何位置管理系統，不需要在電腦上安裝特別的管理軟體。</p></li>
<li><p>Lync Server 管理命令介面 命令列管理工具，它是一款以 Windows PowerShell 命令列介面為基礎的工具。此工具提供多樣化的命令集以便管理產品各層面的事務，同時也能讓 Lync Server 系統管理員利用熟悉的工具使重複的工作自動化。</p></li>
</ul></td>
</tr>
</tbody>
</table>


每個 Lync Server 部署作業均會自動安裝 IM 和目前狀態功能，不過您可以選擇是否要部署會議、Enterprise Voice 及遠端使用者存取等功能，以根據組織的需求量身設定部署。

## 本章節內容

  - [Lync Server 2013 中的 IM 和目前狀態](lync-server-2013-im-and-presence.md)

  - [Lync Server 2013 中的會議](lync-server-2013-conferencing.md)

  - [Lync Server 2013 中的企業語音](lync-server-2013-enterprise-voice.md)

  - [使用 Lync Server 2013 的延展性](lync-server-2013-scalability.md)


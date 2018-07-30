---
title: Lync Server 2013：定義前端伺服器、立即訊息及顯示狀態的需求
TOCTitle: 定義前端伺服器、立即訊息及顯示狀態的需求
ms:assetid: c21198bc-520c-4d17-8b84-7ff1475b9b0a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412956(v=OCS.15)
ms:contentKeyID: 49292210
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義前端伺服器、立即訊息及顯示狀態的需求

 

_**上次修改主題的時間：** 2013-10-07_

規劃立即訊息 (IM) 和目前狀態的主要工作在於確保您擁有足夠的前端伺服器可提供給使用者。

## 與外部使用者進行通訊

您可以藉由讓使用者與外部使用者進行通訊的方式，大幅提高 Lync Server 的投資價值。外部使用者包括：

  - **遠端使用者**   組織自己的使用者，這些使用者位於組織防火牆外，並使用自己的筆記型電腦或其他 Lync Server 裝置工作。

  - **同盟使用者**   來自您合作的公司，並且同樣執行 Lync Server 的使用者。為了方便您的使用者輕鬆連絡這些使用者，您可以和這些公司建立同盟關係。

  - **公用使用者**   公用 IM 服務 (例如 Windows Live 網路的網際網路服務、Yahoo\! 和 AOL 提供的 IM 服務) 的使用者，以及使用可延伸傳訊和顯示狀態通訊協定 (XMPP) (例如 Google Talk) 之提供者和伺服器的使用者。
    
    > [!NOTE]  
    > 請注意，與 Windows Live、AOL 和 Yahoo! 等公用 IM 進行連線可能需要個別授權
    
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
    <li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
    <li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


若要啟用其中任何或所有案例，您需要部署 Edge Server 協助在您的 Lync Server 部署與外部使用者之間啟用安全的通訊。您組織的遠端使用者和同盟組織的使用者將能夠看見彼此的目前狀態，並且使用 IM 進行通訊。如需啟用與外部使用者通訊的詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)。

## 封存 IM 內容

如果您的組織必須遵循規範要求， Lync Server 也提供相關功能。您可以使用封存功能來封存組織內所有使用者的 IM 訊息內容，或是僅針對您指定的特定使用者進行封存。如需詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)。

如果您也部署了 Microsoft Exchange Server 2013，則可將 Exchange 資料封存整合與 Lync Server 資料封存整合，並使用單一工具同時搜尋這兩種封存資料。如需詳細資訊，請參閱 [設定 Microsoft Lync Server 2013 使用 Microsoft Exchange Server 2013 Archiving](configuring-lync-server-2013-to-use-microsoft-exchange-server-2013-archiving.md)。


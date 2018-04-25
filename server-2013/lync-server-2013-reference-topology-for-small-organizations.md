---
title: 小型組織的 Lync Server 2013 參考拓撲
TOCTitle: 小型組織的參考拓撲
ms:assetid: 0453aeee-c41f-44e6-a6e0-aaace526ca08
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398095(v=OCS.15)
ms:contentKeyID: 49289942
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 小型組織中 Lync Server 2013 的參考拓撲

 

_**上次修改主題的時間：** 2013-10-07_

小型組織的參考拓撲顯示如何透過僅部署三部執行 Lync Server 的伺服器，來部署強大且高度可用的解決方案。

**小型組織的參考拓撲**

![部署三個伺服器圖表的參考拓撲](images/Gg398095.25196d0d-dd07-451b-83ba-94c0ddf59030(OCS.15).jpg "部署三個伺服器圖表的參考拓撲")

  - **部署一組 Standard Edition Server**    此組織的中央網站有 4,000 位使用者。組織部署了兩部 Standard Edition 伺服器並配對在一起，以啟用高可用性和災害復原。每部伺服器裝載 2000 位使用者，但是所有使用者的相關資訊會在這兩部伺服器之間同步處理。如果其中一部伺服器故障，系統管理員可以容錯移轉這些使用者，讓另一部伺服器來提供服務，以降低對使用者所造成的困擾。如需有關 Lync Server 2013 之高可用性和災害復原功能的詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)＞。

  - **建議使用 Edge Server 部署。** 雖然內部 IM、出席和會議不需要部署 Edge Server，但我們仍建議小型部署使用 Edge Server。您可以部署 Edge Server 以對目前在組織防火牆外的使用者提供服務，進而發揮最大的 Lync Server 投資效益。包含下列優勢：
    
      - 貴組織本身的使用者在家工作或在出差時仍可使用 Lync Server 功能。
    
      - 您的使用者可以邀請外部使用者參與會議。
    
      - 如果您的合作夥伴、廠商或客戶組織也使用 Lync Server，則可以與該組織構成「同盟關係」 。然後您的 Lync Server 部署會辨識來自該同盟組織的使用者，進而產生更好的合作成果。
    
      - 您的使用者可以和下列公用 IM 服務的使用者交換立即訊息：Windows Live、AOL、Yahoo\! 及 Google Talk。與這些服務的公用 IM 連線可能需要個別的授權。
        
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


  - **分支網站生存能力。** 此組織執行 Lync Server Enterprise Voice 功能的接駁計畫。某些使用者使用 Lync Server 作為唯一的語音解決方案。其中一些語音接駁使用者位於分支網站。分支網站沒有中央網站的可靠廣域網路 (WAN) 連結，所以便部署了 Survivable Branch Appliance。部署此設備之後，如果 WAN 連結中斷，分支網站的使用者仍可撥打和接聽電話 (包含組織內的電話和 PSTN 電話)、擁有語音信箱功能，以及利用雙方立即訊息 (IM) 通訊。無法使用 WAN 連結時，也可以驗證使用者。

  - **Exchange UM 部署。** 此參考拓撲包含的 Exchange 整合通訊 (UM) Server 是執行 Microsoft Exchange Server，而非 Lync Server。
    
    如需 Exchange UM 的詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃 Exchange Unified Messaging 整合](lync-server-2013-planning-for-exchange-unified-messaging-integration.md)＞及＜ [Lync Server 2013 中的主控 Exchange 整合通訊整合](lync-server-2013-hosted-exchange-unified-messaging-integration.md)＞。

  - **Office Web Apps Server。** 建議在使用 Web 會議的每個組織中部署 Office Web Apps Server 或 Office Web Apps Server 伺服器陣列。透過 Office Web Apps Server，您可以在 Web 會議中呈現 PowerPoint 投影片。如需詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。


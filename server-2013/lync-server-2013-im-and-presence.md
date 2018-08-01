---
title: Lync Server 2013 IM 和目前狀態
TOCTitle: IM 和目前狀態
ms:assetid: 6a93ae95-3b64-410b-ab72-74dea232f065
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg417162(v=OCS.15)
ms:contentKeyID: 49291213
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 IM 和目前狀態

 

_**上次修改主題的時間：** 2013-10-07_

立即訊息 (IM) 及目前狀態會自動安裝至任何 Lync Server 部署中。

*「目前狀態」* 資訊可讓使用者在正確的時間使用正確的通訊方式連絡同事，進而產生更具生產力的工作環境。使用者的目前狀態是資訊的集合，包括顯示狀態、通訊意願、其他記事 (如位置及狀態)，以及使用者的連絡方式。在 Lync Server 中，已使用圖片、位置資訊及一組豐富的目前狀態 (除了基本狀態 (如 \[線上\]、\[忙碌\] 及 \[會議中\]) 之外，還包括 \[下班\]、\[請勿打擾\] 及 \[馬上回來\]) 來加強「目前狀態」功能。系統管理員也可以定義自訂的組織特有目前狀態。

連絡人管理及使用者存取選項可讓使用者控制其他人可以看到的資訊。使用者可以設定不同的連絡人層級，而各層級都可以檢視不同的目前狀態資訊層級。

只要查看連絡人清單，使用者就可以快速找到他們需要知道的所有資訊。簡易彩色圖示可指出其他使用者的目前狀態，也會顯示圖片及位置。

在 Lync Server 與 Outlook、SharePoint 等其他產品之間進行整合時，任何時候只要顯示連絡人名稱 (例如在電子郵件訊息中或團隊網站上的連絡人名稱)，則狀態和連絡人資訊也會顯示。另外，如果您部署 Exchange 2013、 Lync Server 和 Exchange 2013 可共用整合連絡人存放區，任一產品的用戶端皆可加以存取。

使用 Lync Server 中的立即訊息，使用者可以使用即時資訊快速互相進行傳訊。使用者也可以依其偏好與公用 IM 網路 (如 MSN/Windows Live、Yahoo\! 及 AOL) 的使用者進行通訊。請注意，與 Windows Live、AOL 和 Yahoo\! 等公用 IM 進行連線可能需要個別授權。 Lync Server 也具備 Extensible Messaging and Presence Protocol (XMPP) 相容性，所以您的使用者可與 Google Talk 等 XMPP 服務的使用者交換 IM 訊息和目前狀態資訊。

> [!Important]  
> <li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
> <li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
> <li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
> </ul>


交談記錄可讓使用者追蹤舊的 IM 交談，以及擷取數月前透過 IM 進行通訊的資訊。

無間 常設聊天室功能可讓您參與長期持續的多方主題式交談。張貼至聊天室 (討論論壇) 的訊息可以持續存在 (也就是長期可用)，因此來自不同位置和部門的人員都可以參與，即使並非同時在線上。

如果您的組織必須遵循規範要求，則可以部署訊息封存功能來封存組織中所有使用者的 IM 訊息內容，或只封存所指定特定使用者的立即訊息內容。如果您也部署 Exchange 2013，則您的 IM 封存可與 Exchange 的就地保留功能整合，來為您的規範提供單一管理體驗。


---
title: Lync Server 2013 伺服器角色
TOCTitle: 伺服器角色
ms:assetid: 7137fc06-fca2-4e5f-9db5-10c7c29a788c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398536(v=OCS.15)
ms:contentKeyID: 49291277
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的伺服器角色

 

_**上次修改主題的時間：** 2013-10-07_

每部執行 Lync Server 的伺服器都會執行一或多個 *「伺服器角色」* 。伺服器角色是該伺服器提供的一組已定義 Lync Server 功能。您不需要在網路中部署所有可用的伺服器角色。請只安裝含有所需功能的伺服器角色。

即使不熟悉 Lync Server 中的伺服器角色， 規劃工具還是可以引導您找到所需要部署之伺服器的最佳解決方案 (根據所需的功能)。本節概述伺服器角色及其提供的一般功能：

  - Standard Edition Server

  - 前端伺服器及後端伺服器

  - Edge Server

  - 中繼伺服器

  - Director

  - 常設聊天室前端伺服器

  - 常設聊天室存放區 (常設聊天室後端伺服器)

  - 常設聊天室存放區 (常設聊天室規範後端伺服器)

針對大部分的伺服器角色，若要獲得延展性及高可用性，您可以部署多部全都執行相同伺服器角色之伺服器的 *「集區」* 。集區中的每部伺服器都必須執行一或多個相同的伺服器角色。針對 Lync Server 中的大部分集區類型，您必須部署負載平衡器，在集區的各個伺服器之間分散流量。 Lync Server 支援網域名稱系統 (DNS) 負載平衡及硬體負載平衡器。

## Standard Edition Server

Standard Edition Server 是針對小型組織以及針對大型組織的試驗專案所設計。它可讓多個 Lync Server 功能 (包括必要資料庫) 在單一伺服器上執行。這可讓您以更低的成本擁有 Lync Server 功能，但所提供的解決方案未真正具有高可用性。

Standard Edition Server 可讓您使用立即訊息 (IM)、顯示狀態、會議及 企業語音，而這些項目全都在一部伺服器上執行。

如需高可用性解決方案，請使用 Lync Server Enterprise Edition。

## 前端伺服器及後端伺服器

在 Lync Server Enterprise Edition 中，前端伺服器是核心伺服器角色，並且執行多個基本 Lync Server 功能。前端伺服器以及後端伺服器都是任何 Lync Server Enterprise Edition 部署中需要有的唯一伺服器角色。

*「前端集區」* 是一組以相同方式設定的前端伺服器，共同運作以提供服務給一般使用者群組。多部執行相同角色之伺服器的集區可提供延展性及容錯移轉功能。

前端伺服器包括下列功能：

  - 使用者驗證及註冊

  - 顯示狀態資訊及連絡人卡片交換

  - 通訊錄服務及通訊群組清單延伸

  - IM 功能 (包括多方 IM 會議)

  - Web 會議、PSTN 電話撥入式會議及 A/V 會議 (若已部署)

  - 應用程式裝載 (適用於 Lync Server 所含的兩個應用程式，例如會議服務員和 回應群組應用程式) 及協力廠商應用程式

  - (選用) 監控，可收集詳細通話記錄 (CDR) 及通話錯誤記錄 (CER) 格式的使用資訊。這項資訊可提供有關周遊 企業語音通話及 A/V 會議網路的媒體 (音訊和視訊) 品質計量。

  - 支援 Web Scheduler 與 Join LauncherWeb 這類 Web 工作的 Web 元件。

  - (選用) 封存，可基於規範考量封存 IM 通訊及會議內容。如需詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)＞。
    
    在 Lync Server 2010 與先前版本中，監控和封存為個別的伺服器角色，並未組合於前端伺服器。

  - (選用) 如果啟用常設聊天室，常設聊天室 Web 服務可執行聊天室管理作業及並提供檔案上傳/下載。

前端集區亦為使用者與會議資料的主要存放區。每個使用者的相關資訊會複寫到集區的三部伺服器中，並備份於後端伺服器上。

此外，部署中的一個前端集區也會執行 *「中央管理伺服器」* ，此伺服器管理基本設定資料，並將其部署至所有執行 Lync Server 的伺服器。 中央管理伺服器也提供 Lync Server 管理命令介面及檔案傳輸功能。

後端伺服器是執行 Microsoft SQL Server 的資料庫伺服器，提供前端集區的資料庫服務。後端伺服器可當作集區使用者與會議資料的備份存放區，亦為回應群組等其他資料庫的主要存放區。您可有單一後端伺服器，但建議使用 SQL Server 鏡像的解決方案來進行容錯移轉。後端伺服器無法執行任何 Lync Server 軟體。

> [!IMPORTANT]  
> 建議您不要將 Lync Server 資料庫與其他資料庫組合，如果這麼做，可能會影響可用性與效能。



後端伺服器資料庫中所儲存的資訊包括目前狀態資訊、使用者的連絡人清單、會議資料 (包括所有目前會議狀態的持續性資料) 以及會議排程資料。

## Edge Server

Edge Server 可讓使用者與組織防火牆外部的使用者通訊及共同作業。這些外部使用者可以包括目前在辦公室外工作的組織使用者、同盟協力廠商組織的使用者，以及受邀加入 Lync Server 部署中所主控之會議的外部使用者。Edge Server 也可以連線至公用 IM 連線服務 (包括 Windows Live、AOL、Yahoo\! 及 Google Talk)。

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


部署 Edge Server 亦會啟用支援行動裝置上 Lync 功能的行動服務。使用者可使用支援的 Apple iOS、Android、Windows Phone 或 Nokia 行動裝置執行活動，例如，傳送和接收立即訊息、檢視聯絡人、檢視目前狀態。此外，行動裝置還支援部分 企業語音功能，例如，按一下即可加入會議、透過公司電話通話、單一號碼連絡、語音信箱及未接來電。行動功能亦可針對不支援應用程式在背景執行的行動裝置支援 *「推入通知」* 。推入通知是可將行動應用程式處於非作用狀態時發生的事件傳送至行動裝置的通知。

Edge Server 亦包括完全整合的 Extensible Messaging and Presence Protocol (XMPP) Proxy，以及包含在前端伺服器的 XMPP 閘道。您可設定這些 XMPP 元件以啟用 Lync Server 2013 使用者，從採用 XMPP 的合作夥伴 (如 Google Talk) 新增聯絡人以使用立即訊息與目前狀態。

如需詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)＞。

## 中繼伺服器

中繼伺服器是實作 企業語音及電話撥入式會議的必要元件。中繼伺服器會轉譯訊號，而在部分設定中，也會轉譯內部 Lync Server 基礎結構與公用交換電話網路 (PSTN) 閘道、IP-PBX 或工作階段初始通訊協定 (SIP) 主幹之間的媒體。您可執行與前端伺服器組合在相同伺服器的中繼伺服器，或已個別分開的獨立中繼伺服器集區。

如需詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的中繼伺服器元件](lync-server-2013-mediation-server-component.md)＞。

## Director

Director 可以驗證 Lync Server 使用者要求，但不會裝載使用者帳戶，或是提供顯示狀態或會議服務。Director 最適合用於加強啟用外部使用者存取之部署的安全性。Director 可以先驗證要求，再將它們傳送至內部伺服器。在拒絕服務攻擊的情況中，攻擊會與 Director 同時結束，而且不會影響前端伺服器。如需詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的 Director 案例](lync-server-2013-scenarios-for-the-director.md)。

## 常設聊天室伺服器 角色

常設聊天室可讓使用者參與長期持續無間的多方主題式交談。常設聊天室前端伺服器可執行常設聊天室服務，常設聊天室後端伺服器可儲存聊天室記錄資料以及有關類別和聊天室的資訊。選用的常設聊天室規範後端伺服器可針對法規遵循目的儲存聊天室內容與規範事件。

執行 Lync ServerStandard Edition 的伺服器亦可執行組合在相同伺服器的常設聊天室。您無法將常設聊天室前端伺服器與 Enterprise Edition前端伺服器組合。

如需詳細資訊，請參閱＜[在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)＞。

## 請參閱

#### 概念

[Lync Server 2013 中的中繼伺服器元件](lync-server-2013-mediation-server-component.md)  

#### 其他資源

[在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)  
[在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)  
[Lync Server 2013 中的 Director 案例](lync-server-2013-scenarios-for-the-director.md)  
[在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)


---
title: Lync Server 2013：外部使用者存取的部署檢查表
TOCTitle: 外部使用者存取的部署檢查表
ms:assetid: 3f55f502-88a0-4315-8783-45a32a0b78ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425910(v=OCS.15)
ms:contentKeyID: 49290701
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中外部使用者存取的部署檢查表

 

_**上次修改主題的時間：** 2015-03-09_

在部署周邊網路並實作支援外部使用者之前，您必須先部署 Microsoft Lync Server 2013 內部伺服器，包括 前端集區或 Standard Edition 伺服器。此外，如果您打算在內部網路部署選用的 Director，則應在部署 Edge Server 之前先行部署。如需 Director 部署程序的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的 Director 案例](lync-server-2013-scenarios-for-the-director.md)＞。

Microsoft Lync Server 2013 包含的工具有助於規劃及部署內部伺服器與 Edge Server。拓撲完成之後，將產生的拓撲定義發行至生產環境。若要進行這項作業，您必須是 **Domain Admins** 群組及 **RTCUniversalServerAdmins** 群組的成員。

  - **規劃工具**    Office Communications Server 2007 R2 包含規劃工具及 Edge 規劃工具，可用來協助引導拓撲設計。在 Lync Server 2010 中，這兩個工具合併為單一的 規劃工具，並且加入其他作用與功能，例如收集已規劃的使用者計數、語音要求、外部使用者存取類型，以及同盟選項。此外，還可以規劃基礎結構的網路參數，例如 IP 位址、負載平衡器類型，以及其他周邊網路考量。

  - **拓撲產生器**    Lync Server 2013拓撲產生器可協助您定義拓撲及元件。對於部署執行 Lync Server 2013 的伺服器而言， 拓撲產生器是必要的。 拓撲產生器會將結果發行至 中央管理存放區 (這是用於設定組織中所有執行 Lync Server 2013 的伺服器)。您必須使用 拓撲產生器，才能在伺服器上安裝 Lync Server 2013。

如果您已在規劃程序期間設計 Edge 拓撲 (包括執行 拓撲產生器以定義 Edge 拓撲)，則可以使用那些結果來開始 Edge Server 部署。如果您先前未完成 Edge 拓撲的建置或想要變更先前指定的資訊，則必須先完成 拓撲產生器的執行，再繼續其他部署步驟。如需如何建置拓撲的詳細資訊，請參閱＜ [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞。

如需規劃工具及拓撲產生器的詳細資訊，請參閱規劃文件中的＜ [開始 Lync Server 2013 的規劃程序](lync-server-2013-beginning-the-planning-process.md)＞。

下表提供 Edge Server 部署程序的概觀。如要檢閱部署外部使用者存取之前必須完成的規劃決定，請參閱＜ [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞。

> [!WARNING]
> 下表的資訊以全新部署為主。如果您已在 Lync Server 2010、 Office Communications Server 2007 R2 或 Office Communications Server 2007 環境中部署 Edge Server，請參閱 <a href="migration.md">移轉</a>中有關移轉至 Lync Server 2013 的詳細資訊。不支援從任何比 Office Communications Server 2007 R2 舊的版本 (包括 Office Communications Server 2007、 Live Communications Server 2005 以及 Live Communications Server 2003) 移轉。


為了提升 Edge Server 效能與安全性，以及協助部署順利進行，請在部署周邊網路和 Edge Server 時套用下列最佳作法：

  - 在組織內已測試及驗證 Lync Server 2013 作業之後，才部署 Edge Server。

  - 建議您在工作群組 (而不是網域) 中部署 Edge Server。這麼做可簡化安裝程序，同時將 Active Directory 網域服務 (AD DS) 置於周邊網路之外。將 AD DS 設置在周邊網路中，可能帶來重大的安全風險。

  - 可支援將 Edge Server 加入完全位於周邊網路中的網域，但不建議使用。 Edge Server 作為內部網域的一部分違反了信任網路界限 (其中網際網路最不受信任，周邊網路比網際網路更受信任，而內部網路最受信任)。Edge Server 作為網域的成員會自動成為最受信任網路的一部分，卻位於較不受信任的網路中 (周邊網路)。

## Edge Server 部署程序


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>權限</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>建立適當的 Edge 拓撲，並決定適當的元件。</p></td>
<td><ul>
<li><p>執行 拓撲產生器以進行 Edge Server 設定、建立並發行拓撲，然後使用 Lync Server 管理命令介面匯出拓撲組態檔。</p></li>
</ul>
<p></p></td>
<td><p><strong>Domain Admins</strong> 群組和 <strong>RTCUniversalServerAdmins</strong> 或 <strong>CsAdmins</strong> 群組</p>
<div>

> [!NOTE]  
> 您可以使用本機使用者群組的成員帳戶來定義拓撲，但發行拓撲需要以 <strong>Domain Admins</strong> 群組和 <strong>RTCUniversalServerAdmins</strong> 群組的成員帳戶進行。


</div></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-building-an-edge-and-director-topology.md">在 Lync Server 2013 中建置 Edge 和 Director 拓撲</a>＞</p></td>
</tr>
<tr class="even">
<td><p>準備進行安裝。</p></td>
<td><ol>
<li><p>確定已符合系統先決條件。</p></li>
<li><p>在每部 Edge Server 上，設定內部與公開網路介面的 IP 位址 (IPv4 和 IPv6，如果使用的話)。</p></li>
<li><p>設定內部與外部 DNS 記錄 (IPv4 和 IPv6 的主機 A 和 AAAA)，包括在要部署為 Edge Server 的電腦上設定 DNS 尾碼。</p></li>
<li><p>(選用) 建立並安裝公用憑證。取得憑證所需的時間，視發出憑證的憑證授權單位 (CA) 而定。如果您此時不執行這個步驟，也必須在 Edge Server 安裝期間執行。未取得並安裝憑證前，Edge Server Service 無法啟動。</p></li>
<li><p>佈建公用 IM 連線的支援 (如果您的部署是要支援與 Windows Live、AOL 或 Yahoo! 使用者的通訊)。</p>
<div>


> [!IMPORTANT]  
> <p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p>  
> <p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p>
> <p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p>

</div></li>
<li><p>佈建針對 Office Communications Server 2007、 Office Communications Server 2007 R2 以及 Lync Server 2010 協力廠商之 XMPP 與同盟的支援 (如果部署將使用的話)</p></li>
<li><p>設定防火牆。</p></li>
</ol></td>
<td><p>視組織而定</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-preparing-for-installation-of-servers-in-the-perimeter-network.md">在周邊網路中準備安裝 Lync Server 2013 的伺服器</a>＞</p></td>
</tr>
<tr class="odd">
<td><p>設定反向 Proxy。</p></td>
<td><ul>
<li><p>在周邊網路設定反向 Proxy (例如，針對 Microsoft Forefront Threat Management Gateway 2010 或 Microsoft Internet Security and Acceleration (ISA) Server Service Pack 1)、取得必要公用憑證，並在反向 Proxy 伺服器上設定發行規則。</p>
<p>如果已為行動性做規劃，並且要在前端集區或 Standard Edition Server 上部署行動性服務，請準備好行動性服務的反向 Proxy。</p></li>
</ul></td>
<td><p><strong>Administrators</strong> 群組或反向 Proxy 管理員</p></td>
<td><p></p>
<p>部署文件中的＜ <a href="lync-server-2013-setting-up-reverse-proxy-servers.md">設定 Lync Server 2013 的反向 Proxy 伺服器</a>＞</p></td>
</tr>
<tr class="even">
<td><p>安裝 Director (選用)。</p></td>
<td><ul>
<li><p>(選用) 在內部網路安裝並設定一個或多個 Director。</p></li>
</ul></td>
<td><p><strong>Administrators</strong> 群組</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-setting-up-the-director.md">在 Lync Server 2013 中設定 Director</a>＞</p></td>
</tr>
<tr class="odd">
<td><p>設定 Edge Server。</p></td>
<td><ol>
<li><p>安裝必要軟體。</p></li>
<li><p>將匯出的拓撲組態檔傳輸給每部 Edge Server。</p></li>
<li><p>在每部 Edge Server 上安裝 Lync Server 2013 軟體。</p></li>
<li><p>設定 Edge Server。</p></li>
<li><p>為每一部 Edge Server 要求並安裝憑證。</p></li>
<li><p>啟動 Edge Server 服務。</p></li>
</ol></td>
<td><p><strong>Administrators</strong> 群組</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-setting-up-edge-servers.md">在 Lync Server 2013 中設定 Edge Server</a>＞</p></td>
</tr>
<tr class="even">
<td><p>設定部署以進行外部使用者存取。</p></td>
<td><ol>
<li><p>使用 Lync Server 控制台來設定下列每一項的支援 (若適用) ：</p>
<ul>
<li><p>媒體中繼</p></li>
<li><p>同盟路由</p></li>
<li><p>遠端使用者存取</p></li>
<li><p>與 Lync Server、 Office Communications Server 及 Live Communications Server 進行同盟</p></li>
<li><p>公用 IM 連線</p></li>
<li><p>XMPP 同盟</p></li>
<li><p>匿名使用者</p></li>
</ul></li>
<li><p>設定使用者帳戶以進行遠端使用者存取、同盟、公用 IM 連線、XMPP 和匿名使用者支援 (若適用)</p></li>
</ol></td>
<td><p>指派給 <strong>CSAdministrator</strong> 角色的 <strong>RTCUniversalServerAdmins</strong> 群組或使用者帳戶</p>
<p></p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-configuring-support-for-external-user-access.md">在 Lync Server 2013 中設定外部使用者存取支援</a>＞</p></td>
</tr>
<tr class="odd">
<td><p>驗證您的 Edge Server 設定。</p></td>
<td><ol>
<li><p>驗證伺服器連線以及內部伺服器組態資料的複寫是否正確。</p></li>
<li><p>驗證外部使用者 (包括遠端使用者、同盟網域的使用者、公用 IM 使用者和匿名使用者，視您的部署而定) 是否能連線。</p></li>
<li><p>使用 Lync Server 遠端連線分析程式 ( <a href="https://www.testocsconnectivity.com" class="uri">https://www.testocsconnectivity.com</a>) 驗證設定及通訊</p></li>
<li><p>疑難排解設定及通訊問題</p></li>
</ol></td>
<td><p>若為驗證複寫，為指派給 <strong>CSAdministrator</strong> 角色的 <strong>RTCUniversalServerAdmins</strong> 群組或使用者帳戶</p>
<p>若為驗證使用者連線，則為您支援之每種外部使用者存取類型的使用者</p>
<p>遠端使用者</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-verifying-your-edge-deployment.md">在 Lync Server 2013 中驗證 Edge 部署</a>＞</p></td>
</tr>
</tbody>
</table>


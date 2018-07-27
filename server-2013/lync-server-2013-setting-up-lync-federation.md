---
title: Lync Server 2013：設定 Lync 同盟
TOCTitle: 設定 Lync 同盟
ms:assetid: 374ddc43-26f9-499d-be68-a5158adfa49c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204800(v=OCS.15)
ms:contentKeyID: 49290582
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Lync 同盟

 

_**上次修改主題的時間：** 2015-03-09_

如果您已經部署一或多部 Edge Server，就可以直接新增同盟案例功能。如果您尚未設定 Edge Server，則必須先進行設定。如需詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)＞和部署文件中的＜ [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)＞。

> [!NOTE]  
> 如果您想要設定任何 XMPP 同盟、Lync 同盟或 Public Instant Messaging Connectivity 的組合，您可以同時部署它們，或者一次部署一個。如果您透過拓撲產生器和 Lync Server 管理命令介面設定選項，接著在設定一個、兩個或三個同盟類型的選項之後，於 Edge Server 上執行部署精靈，則您可以減少必要的步驟數。



## 在拓撲產生器和部署精靈中設定 Lync 同盟

1.  在前端伺服器上，開啟 \[拓撲產生器\]。展開 Edge 集區，然後按一下您的 Edge Server 或 Edge Server 集區。選取 \[編輯內容\]。

2.  在 \[一般\] 下的 \[編輯內容\] 中，選取 \[啟用此 Edge 集區的同盟 (連接埠 5061)\]。按一下 \[確定\]。

3.  按一下 \[動作\]，然後依序選取 \[拓撲\] 和 \[發行\]。出現發行拓撲的提示時，按 \[下一步\]。完成發行時，按一下 \[完成\]。

4.  在 Edge Server 上，開啟 \[Lync Server 部署精靈\]。按一下 \[安裝或更新 Lync Server 系統\]，然後按一下 \[安裝或移除 Lync Server 元件\]。按一下 \[再執行一次\]。

5.  在 \[安裝 Lync Server 元件\] 上，按 \[下一步\]。摘要畫面將顯示它們執行的動作。部署完成之後，按一下 \[檢視記錄\] 以檢視可用的記錄檔。按一下 \[完成\] 以完成部署。
    
    > [!IMPORTANT]  
    > 您可以選取此選項，但是只能將組織中的一個 Edge 集區或 Edge Server 發行到外部，以進行同盟。所有由同盟使用者 (包括公用立即訊息 (IM) 使用者) 進行的存取都會通過相同的 Edge 集區或單一 Edge Server。例如，如果您的部署範圍包括分別部署在紐約與倫敦的一個 Edge 集區或單一 Edge Server，而您針對紐約的 Edge 集區或單一 Edge Server 啟用了同盟支援，則同盟使用者的訊號流量會通過紐約的 Edge 集區或單一 Edge Server。儘管位於倫敦的內部使用者在致電倫敦的同盟使用者時，使用了倫敦集區或 Edge Server 以傳送音訊/視訊流量，與倫敦的使用者進行通訊時也適用這種情況。
    


## 設定與協力廠商的同盟

1.  若要成功設定與其他 Microsoft Lync Server 2013、 Lync Server 2010、 Office Communications Server 2007 R2 或 Office Communicator 2007 同盟，請從下表中選取同盟類型並定義 DNS SRV 記錄、DNS 主機 (適用於 IPv6 的 A 或 AAAA)，以及設定適用於同盟類型的原則：
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>同盟類型</th>
    <th>DNS 記錄</th>
    <th>原則定義</th>
    <th>附註</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>探索到的協力廠商網域</p></td>
    <td><p>設定 SRV 記錄的格式 _sipfederationtls._tcp.&lt;外部網域名稱&gt;。其中 SRV 記錄的連接埠值為 TCP 5061，並且將 <strong>[提供這項服務的主機]</strong> 定義為 sip。&lt;外部網域名稱&gt; - Access Edge Service 的 FQDN。如需關於建立 SRV 記錄的詳細資訊，請參閱＜ <a href="lync-server-2013-configure-dns-for-edge-support.md">在 Lync Server 2013 中設定 Edge 支援的 DNS</a>＞。</p></td>
    <td><ul>
    <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></li>
    <li><p><a href="lync-server-2013-enable-or-disable-discovery-of-federation-partners.md">在 Lync Server 2013 中啟用或停用探索同盟協力廠商</a></p></li>
    </ul></td>
    <td><p>舊版將此類型的同盟稱為 <strong>「開放式增強型同盟」</strong>。您必須針對此類型的同盟建立 SRV 記錄，以允許其他協力廠商探索您的同盟。</p></td>
    </tr>
    <tr class="even">
    <td><p>允許的協力廠商網域</p></td>
    <td><p>設定 SRV 記錄的格式 _sipfederationtls._tcp.&lt;外部網域名稱&gt;。其中 SRV 記錄的連接埠值為 TCP 5061，並且將 <strong>[提供這項服務的主機]</strong> 定義為 sip。&lt;外部網域名稱&gt; - Access Edge Service 的 FQDN。如需關於建立 SRV 記錄的詳細資訊，請參閱＜ <a href="lync-server-2013-configure-dns-for-edge-support.md">在 Lync Server 2013 中設定 Edge 支援的 DNS</a>＞。</p></td>
    <td><ul>
    <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></li>
    </ul></td>
    <td><p>舊版將此類型的同盟稱為 <strong>「增強型同盟」</strong>。您可以選擇性地針對此類型的同盟建立 SRV 記錄，以允許其他協力廠商探索您的同盟。當然，這就是 <strong>「開放式增強型同盟」</strong>或 <strong>「探索到的協力廠商網域」</strong>.</p></td>
    </tr>
    <tr class="odd">
    <td><p>允許的協力廠商伺服器</p></td>
    <td><p>設定 SIP 網域名稱和協力廠商 Edge Server FQDN，作為原則中的同盟協力廠商</p></td>
    <td><ul>
    <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></li>
    <li><p><a href="lync-server-2013-configure-support-for-allowed-external-domains.md">在 Lync Server 2013 中針對允許的外部網域設定支援</a></p></li>
    <li><p><a href="lync-server-2013-configure-support-for-blocked-external-domains.md">在 Lync Server 2013 中為封鎖的外部網域設定支援</a></p></li>
    </ul></td>
    <td><p>此同盟類型為一對一關聯性的定義，不允許其他同盟協力廠商進行探索。每個同盟協力廠商都已明確設定。在舊版中，這稱為 <strong>「直接同盟」</strong></p></td>
    </tr>
    <tr class="even">
    <td><p>裝載提供者和公用 IM 提供者</p></td>
    <td><p>未針對此類型的同盟定義任何特定的 DNS 需求</p></td>
    <td><ul>
    <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></li>
    <li><p><a href="lync-server-2013-create-or-edit-public-sip-federated-providers.md">在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者</a></p></li>
    <li><p><a href="lync-server-2013-create-or-edit-hosted-sip-federated-providers.md">建立或編輯主控的 SIP 同盟提供者 Lync Server 2013</a></p></li>
    </ul></td>
    <td><p>此同盟類型定義您要為使用者設定的服務和裝載提供者。一般用法包含針對像是 Windows Live Messenger、Yahoo! 及 AOL 等公用 IM 提供者，以及像是 Lync Online 和 Office 365 的主機服務提供者進行設定。</p>
    <div class="alert">
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

    </div></td>
    </tr>
    </tbody>
    </table>


2.  定義和設定任何必要的 DNS 主機 (適用於 IPv6 的 A 或 AAAA) 和 DNS SRV 記錄

3.  使用 Lync Server 控制台或使用 Lync Server 管理命令介面和適當的 Cmdlet 來定義和設定任何原則。如需關於 Lync Server 管理命令介面 Cmdlet 的詳細資訊，請參閱＜ [Lync Server 2013 中的同盟和外部存取 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/skype/)＞。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Room System (LRS) 不會針對同盟 Lync 合作夥伴中的組織者所傳送的會議顯示加入按鈕。若要在 LRS 上顯示會議加入連結，傳送組織必須使用下列 Cmdlet 啟用 TNEF：<br />
    <br />
    <code>New-RemoteDomain -DomainName Contoso.com -Name Contoso</code><br />
    <code>Set-RemoteDomain -Identity Contoso -TNEFEnabled $true</code><br />
    請注意，這定不是 LRS 特有的。Outlook 與 Lync 在此情況下也不會顯示 [加入] 連結，因為並未傳輸 MAPI 內容，但在 Outlook 中，使用者可以開啟會議邀請並按一下會議 URL。當 TNEFEnabled 設定為 true 時，Exchange 2013 不會除去包括 OnlineMeetingExternalLink 的 MAPI 內容，且 [加入] 按鈕將會顯示在提醒中。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 其他資源

[規劃 Lync Server 2013 中的 SIP、XMPP 同盟和公用立即訊息](lync-server-2013-planning-for-sip-xmpp-federation-and-public-instant-messaging.md)  
[管理 Lync Server 2013 的同盟與外部存取](lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md)


---
title: Lync Server 2013：常見問題集：佈建 Lync Server 以供 Skype 連線
TOCTitle: 常見問題集：佈建 Lync Server 以供 Skype 連線
ms:assetid: 4d1b2bfc-780b-4b8c-afd5-11c2e59203b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn440172(v=OCS.15)
ms:contentKeyID: 59602846
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 常見問題集：佈建 Lync Server 以供 Skype 連線

 

_**上次修改主題的時間：** 2015-07-22_

**問：Microsoft Lync 與 Skype 之間支援哪些功能？**

**答：**由於 Skype 目前已成為 Microsoft 系列的一員，數以百萬計的 Skype 使用者將可因為整合通訊選項的拓展而享有更多可能性。這項結合將可讓 Lync 用戶藉由 Lync 的豐富功能與 Skype 的普及率而與供應商、客戶及合作夥伴連線並共同作業。

  - 立即訊息與音訊和視訊通話：Lync 與 Skype 使用者之間的同盟音訊和視訊通話與立即訊息

  - 目前狀態分享：同盟連絡人之間的目前狀態資訊交換

  - 簡易管理：提供設定與控制項，可配合組織的原則與標準設定同盟通訊

**問：如何將 Lync 部署與 Skype 連線？**

**答：**如果您有下列任一項即有授權可進行 Skype 連線：

  - Lync Server (2010 或 2013)，外加組織中將連線至 Skype 之使用者及/或裝置均有 Lync Server 標準用戶端存取使用權 ("CAL"；2010 或 2013)

  - Lync Online (獨立授權或 Office 365 套件的一部分)。然而，此服務 (pic.lync.com) 僅適合佈建 Lync Server 與混合式 Lync Server 與 Lync Online 的部署。Lync Online PIC 佈建是透過 Lync Online 控制台 (LOCP) 完成。

**問：Lync 使用者要如何與 Skype 連絡人連線？**

**答：**在組織的 Lync 系統管理員啟動網域並啟用功能後，Lync 使用者即可在 Lync 用戶端中將 Skype 連絡人新增至連絡人清單。

**問：Skype 使用者要如何與 Lync 連絡人連線？**

**答：**所有要與 Lync 使用者連線的 Skype 使用者必須有與其 Skype 識別碼相關聯的 Microsoft 帳戶，並使用該 Microsoft 帳戶登入。這可在 Skype 用戶端中啟用。

**答：與 Windows Live 的同盟服務是否仍然可用？**

**答：**自 2012 年 10 月起，Microsoft 即著手協助 Windows Live Messenger (WLM) 使用者移至 Skype，以達到最後淘汰 WLM 的目的。只要 WLM 仍提供於市面，Lync 將持續支援與 WLM 的同盟，但已不再允許啟用新的 Windows Live 網域。WLM 使用者的移轉作業是由適用於 Mac 與 Windows 的 Skype 6.0 (於 2012 年 10 月 25 日發行) 提供，該軟體允許使用 Microsoft 帳戶 (亦即與 WLM 相同的認證) 登入。只要登入 Skype，WLM 好友清單即會自動填入 Skype，而使用者即可利用 Skype 的擴充通訊功能，例如撥打市話與手機、螢幕共用、群組視訊通話，以及各式裝置的支援。不僅如此，WLM 使用者的同盟 Lync 連絡人將可與其他好友清單一併移轉至 Skype，且這些連絡人將可立即使用 Skype 與 Lync 之間的 IM 功能。Lync 用戶無需執行任何操作來延續啟用這項服務。

**問：與 Yahoo\! 或 AOL 的同盟服務是否仍然可用？**

**答：**針對 Lync 與 Office Communications Server 的用戶，與 Yahoo\! 及 AOL 之間的同盟均已邁向尾聲。Microsoft 能夠提供這些服務，一直是因為 Yahoo\! 與 AOL 提供支援，而這些服務的基本合約亦即將結束。針對 Yahoo\! 與 AOL，服務將持續至 2014 年 6 月。

  - Yahoo\!：服務將持續至 2014 年 6 月，用戶仍需取得 Microsoft Lync 公用 IM 連線使用者訂閱授權 ("PIC USL") 的授權。自 2012 年 9 月 1 日起，PIC USL 不再以新合約或續約的方式供使用者購買。於該日期之前購買授權的用戶將能夠與 Yahoo\! 維持同盟關係，直至服務終止日或授權到期為止。用戶合約中的 PIC 授權若超過 2014 年 6 月 30 日，將會收到等同於下列款項金額的信用額度 (依比例計算：2014 年 6 月 30 日之後的時間長度佔合約總長度的比例)。

  - AOL：Lync 的 IM 連線 ("PIC") 服務將於 2014 年 6 月 30 日停止。為限制服務終止對用戶所造成的影響，我們已停止佈建新的用戶網域。在 2014 年 6 月 30 日前，用戶無須進行任何動作即可繼續以 AIM 支援同盟通訊。在此日期後 (或是想在此期間佈建新網域的用戶)，可直接從 AOL 取得替代的服務。如需 AOL 新服務的詳細資訊，請參閱 <http://aimenterprise.aol.com/pic.php> (在 AOL.com 上開啟新網頁)。 

**問：我是否能夠在購買 Lync 前試用 Skype 連線？**

**答：**Skype 連線不提供試用。Microsoft 歡迎具有合格授權的 Lync 用戶直接註冊服務進行測試。

**問：佈建需要哪些資訊？**

**答：**若要以合格授權提交佈建要求，您需要下列項目：

  - Microsoft 合約編號：
    
      - Microsoft 大量授權支援：Microsoft 大量授權合約編號
    
      - Microsoft Partner Network：總公司合作夥伴識別碼
    
      - 服務提供者授權合約：初始註冊號碼
    
      - 大量服務：產品註冊號碼

  - Access Edge Service 的完整網域名稱 (FQDN)。
    
      - 需要至少一個 Access Edge Service 的 FQDN。
    
      - 若是您的組織有超過一個伺服器執行 Access Edge Service，請指定各個額外 Access Edge Service 的 FQDN。重要事項：若是先前已有指定 Access Edge Service 的 FQDN，然後想要加以變更，變更的佈建作業可能需要數天才可完成，且可能導致服務中斷。若要避免服務中斷，建議您保留先前指定的 Access Edge Service 的 FQDN。

  - 工作階段初始通訊協定 (SIP) 網域。此為使用者目前用於立即訊息之 SIP URI 的網域尾碼。若是您的組織有超過一個 SIP 網域，請指定用於立即訊息之各個網域的網域尾碼。舉例來說，若是 user1@contoso.com，請將 contoso.com 指定為 SIP 網域；若是 user1@example.fabrikam.com，請將 example.fabrikam.com 指定為 SIP 網域。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請僅指定 SIP 網域的網域尾碼。請勿指定任何 FQDN，包括 SIP 網域之 Access Edge Service 的 FQDN。</td>
    </tr>
    </tbody>
    </table>


  - 連絡人資訊。針對您指定之各個 SIP 網域的系統管理員，指定其電子郵件地址。

**問：我要如何在分割網域的情況下啟用 Lync-Skype 連線？**

**答：**如果您擁有 Lync Online 2013 與 Lync Server 內部部署分割網域 (線上與內部部署的使用者使用相同的 SIP 網域)，請依照順序執行下列兩項步驟以啟用 Lync-Skype 連線：

1.  依照 PIC 佈建指南中的說明，設定內部部署的 Lync-Skype 連線。

2.  等待畫面出現 Microsoft 已佈建網域的確認訊息。

3.  看到確認訊息後，使用 Lync 系統管理中心開啟「外部通訊」。如需詳細資訊，請參閱 [http://office.microsoft.com/zh-tw/support/configure-external-communications-HA102817865.aspx?CTT=5\&origin=HA102817356](http://office.microsoft.com/zh-tw/support/configure-external-communications-ha102817865.aspx?ctt=5%26origin=ha102817356)

這個順序相當重要。您必須先設定內部部署連線，然後才可在 Lync Online 中啟用通訊。若順序顛倒，則在 <https://pic.lync.com> 中針對內部部署所輸入的資訊將無法傳遞。若是您已設定 Lync Online 以便與此網域進行外部通訊，則必須先關閉該功能、等候 24 小時，然後重新開始 (先在 <https://pic.lync.com> 中輸入您的內部部署資訊，然後針對 Lync Online 開啟外部通訊)。

**問：我是否能佈建多個 Access Edge Service FQDN 以供 Skype 連線？**

**答：**各個佈建要求可佈建最多十個 Access Edge Service。

**問：我是否能夠取得在要求佈建的組織中所找到的 Microsoft 帳戶電子郵件地址？**

**答：**否。這些地址為個人識別資訊，無法共用。

**問：如果 Windows Live Messenger 連絡人的識別碼包含 Windows Live 不支援的網域，我要如何新增該連絡人？**

**答：**若要要新增的Windows Live Messenger 使用者的帳戶或識別碼包含非 Windows Live 網域，請以下列格式輸入地址：\<user name\>(\<domain name\>)@msn.com，其中 \<domain name\> 為使用者電子郵件地址的網域名稱。例如，若要新增 ted@contoso.com，您需要採取下列格式：ted(contoso.com)@msn.com。如需 Windows Live 管理之網域的清單，請參閱＜公用立即訊息在 Live Communications Server Service Pack 1 安裝後所會發生的已知問題＞中的＜支援網域＞一節：http://support.microsoft.com/?kbid=897567。

**問：佈建程序需要多久時間？**

**答：**佈建最多需要 30 天。

**問：我要如何知道佈建已經完成？**

**答：**Microsoft 會在佈建完成時傳送電子郵件通知。

**問：我要如何更新所提交的設定或連絡人詳細資訊？**

**答：**佈建完成後，您可以在用於提出佈建要求的相同網站上更新您的資訊。請輸入您的合約編號，然後按下 \[更新服務\]。


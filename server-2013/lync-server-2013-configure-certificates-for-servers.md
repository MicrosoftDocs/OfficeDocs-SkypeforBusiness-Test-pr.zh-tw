---
title: Lync Server 2013：設定伺服器憑證
TOCTitle: 設定伺服器憑證
ms:assetid: e12e59b5-a146-4859-86ec-cabfc198c7b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398995(v=OCS.15)
ms:contentKeyID: 49292573
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定伺服器憑證

 

_**上次修改主題的時間：** 2013-03-17_

若要成功完成此程序，您應該以身為 RTCUniversalServerAdmins 群組成員或擁有正確委派之權限的使用者身分登入。如需委派權限的詳細資訊，請參閱＜ [在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)＞。根據您的組織以及對要求憑證的需求，您可能需要其他群組成員資格。請向負責管理公開金鑰基礎結構 (PKI) 憑證授權單位 (CA) 的部門洽詢相關資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除了 Lync Phone Edition 之外， Lync Server 2013 也支援在從執行 Windows 7、Windows Server 2008 R2、Windows Server 2008、Windows Vista 或 Windows XP 作業系統的用戶端進行連線時使用採雜湊摘要演算法與簽署演算法的 SHA-256 套件 (SHA-2 會使用 224、256、384 或 512 位元摘要長度)。為了支援使用 SHA-256 套件的外部存取，外部憑證會由亦可核發位元長度摘要相同之憑證的公用 CA 核發。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雜湊摘要演算法與簽署演算法的選擇，會視將使用憑證的用戶端和伺服器而定，而用戶端和伺服器將會進行通訊的其他電腦與裝置，也必須知悉如何使用憑證中所採的演算法。如需有關作業系統與部分用戶端應用程式所支援之雜湊長度的資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=287002">http://go.microsoft.com/fwlink/?LinkId=287002</a>。</td>
</tr>
</tbody>
</table>


每部 Standard Edition 伺服器或 前端伺服器最多需要四個憑證：oAuthTokenIssuer 憑證、一個預設憑證、一個內部 Web 憑證和一個外部 Web 憑證。但是，可以要求並指派一個具有合適主體別名項目的預設憑證，以及 oAuthTokenIssuer 憑證。如需憑證需求的詳細資訊，請參閱＜ [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)＞。如需要求、指派及安裝 oAuthTokenIssuer 憑證的詳細資訊，請參閱＜ [在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)＞。

使用下列程序要求、指派及安裝 Standard Edition 伺服器或 前端伺服器憑證。為每個 前端伺服器重複這個程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列程序描述了如何從組織部署的內部企業 PKI 以及如何透過離線要求處理設定憑證。若需從公用 CA 取得憑證的資訊，請參閱規劃文件的＜ <a href="lync-server-2013-certificate-requirements-for-internal-servers.md">Lync Server 2013 中內部伺服器的憑證需求</a>＞。此外，本程序還描述了如何在 前端伺服器設定期間要求、指派和安裝憑證。如果您預先要求憑證 (如本部署文件中的＜ <a href="lync-server-2013-request-certificates-in-advance-optional.md">針對 Lync Server 2013 預先要求憑證 (選用)</a>＞一節所述)，或者您不使用組織中部署的內部企業 PKI 取得憑證，則您必須根據需要修改本程序。</td>
</tr>
</tbody>
</table>


## 若要為前端伺服器設定憑證

1.  在 \[ Lync Server 部署精靈\] 中，按一下 **\[執行\]** ，旁邊即是 **\[步驟 3：要求、安裝或指派憑證\]** 。

2.  在 **\[憑證精靈\]** 頁面中，按一下 **\[要求\]** 。

3.  在「憑證要求」 頁面上，按 \[下一步\] 。

4.  在 \[延遲或立即要求\] 頁面上，按 \[下一步\] ，可以接受預設的 \[立即將此要求傳送到線上憑證授權單位\] 。選取此選項之後，可以使用具有自動線上註冊功能的內部 CA。如果您選擇此選項延遲要求，則系統會提示您輸入名稱和位置，以儲存憑證要求檔案。憑證要求必須由組織內的 CA 或公用 CA 提供和處理。您需要匯入憑證回應並將其指派給合適的憑證角色。

5.  在 \[選擇憑證授權單位 (CA)\] 頁面上，選擇 \[從您環境中偵測到的清單選取 CA\] 選項，然後從清單中選擇一個已知 (在 Active Directory 網域服務 上註冊) CA。或者，選擇 \[請指定其他憑證授權單位\] 選項，在方塊中輸入其他 CA 的名稱，然後按 \[下一步\] 。

6.  在 **\[憑證授權單位帳戶\]** 頁面上，系統將會提示您輸入要求和處理 CA 中憑證要求的認證。您需要確定預先要求憑證是否需要使用者名稱和密碼。您的 CA 管理員瞭解必需資訊，並且可以在本步驟中為您提供協助。如果您需要提供其他憑證，請選取該核取方塊，在文字方塊中輸入使用者名稱和密碼，然後按 **\[下一步\]** 。

7.  在 **\[指定其他憑證範本\]** 頁面上，若要使用預設 Web 伺服器範本，請按 **\[下一步\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的組織已建立了一個範本，用作預設 Web 伺服器 CA 範本的替代範本，請選取該核取方塊，然後輸入該替代範本的名稱。您需要 CA 管理員定義的範本名稱。</td>
    </tr>
    </tbody>
    </table>


8.  在 **\[名稱和安全性設定\]** 頁面上，指定一個 **\[易記名稱\]** ，以允許您辨識憑證和瞭解用途。如果您將其留空，則會自動產生一個名稱。設定金鑰的 **\[位元長度\]** ，或接受預設的 2048 個位元。如果確定需要將該憑證和私密金鑰移動或複製到其他系統，請選擇 **\[將憑證的私密金鑰標示為可匯?\]** ，然後再按 **\[下一步\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 對可匯出的私密金鑰的需求最低。例如集區中的 Edge Server，它上面的媒體轉送驗證服務會使用憑證的複本，而不使用集區中各執行個體的個別憑證。</td>
    </tr>
    </tbody>
    </table>


9.  在 **\[組織資訊\]** 頁面上，可以提供組織資訊，然後按 **\[下一步\]** 。

10. 在 **\[地理資訊\]** 頁面上，可以提供地理資訊，然後按 **\[下一步\]** 。

11. 在 **\[主體名稱 / 主體別名\]** 頁面上，檢閱將要新增的主體別名，然後按 **\[下一步\]** 。

12. 在 **\[SIP 網域設定\]** 頁面上，選取 **\[SIP 網域\]** ，然後按 **\[下一步\]** 。

13. 在 **\[設定其他主體別名\]** 頁面上，新增任何其他必要的主體別名，包括其他 SIP 網域將來可能需要的主體別名，然後按 **\[下一步\]** 。

14. 在 **\[憑證要求摘要\]** 頁面上，檢閱摘要中的資訊。如果資訊是正確的，請按 **\[下一步\]** 。如果需要更正或修改某項設定，請按 **\[上一步\]** ，回到相應的頁面進行更正或修改。

15. 在 **\[執行命令\]** 頁面上，按 **\[下一步\]** 。

16. 在 **\[線上憑證要求狀態\]** 頁面上，檢閱傳回的資訊。請注意，憑證已核發並且已安裝到本機憑證存放區。如果報告憑證已核發並安裝，但是無效，則請確認已在伺服器之受信任的根 CA 存放區中安裝了 CA 根憑證。若要瞭解如何擷取受信任的根 CA 憑證，請參閱您的 CA 文件。若需檢視擷取的憑證，請按一下 **\[檢視憑證的詳細資料\]** 。根據預設， **\[將此憑證指派到 Lync Server 憑證使用方式\]** 的核取方塊已核取。如果您希望手動指派憑證，請清除該核取方塊，然後按一下 **\[完成\]** 。

17. 在上一頁中清除 **\[將此憑證指派到 Lync Server 憑證使用方式\]** 的核取方塊之後，您將會看到 **\[憑證指派\]** 頁面。按 **\[下一步\]** 。

18. 在 **\[憑證存放區\]** 頁面上，選取要求的憑證。若要檢視憑證，請按一下 **\[檢視憑證的詳細資料\]** ，然後再按 **\[下一步\]** 繼續。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 <strong>[線上憑證要求狀態]</strong> 頁面報告一個憑證問題，如憑證無效，則可透過檢視真實憑證來協助解決該問題。上述可導致憑證無效的兩個特定問題為：受信任的根 CA 憑證遺失，與該憑證關聯的私密金鑰遺失。若要解決這兩個問題，請參閱您的 CA 文件。</td>
    </tr>
    </tbody>
    </table>


19. 在 **\[憑證指派摘要\]** 頁面上，檢閱提供的資訊，確認該憑證即是要指派的憑證，然後按 **\[下一步\]** 。

20. 在 **\[執行命令\]** 頁面上，檢閱命令的輸出。若要檢閱指派程序或如果發?了錯誤或警告，請按一下 **\[檢視記錄檔\]** 。檢閱記錄檔完成後，按一下 **\[完成\]** 。

21. 在 **\[憑證精靈\]** 頁面上，驗證憑證的 **\[狀態\]** 是否為「已指派」，然後按一下 **\[關閉\]** 。

## 請參閱

#### 其他資源

[Lync Server 2013 的憑證基礎結構需求](lync-server-2013-certificate-infrastructure-requirements.md)


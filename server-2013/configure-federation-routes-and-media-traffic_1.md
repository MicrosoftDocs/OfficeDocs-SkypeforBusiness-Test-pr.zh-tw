---
title: 設定同盟路由與媒體流量
TOCTitle: 設定同盟路由與媒體流量
ms:assetid: ed6cb922-7863-453a-adce-2ce0ba761d74
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721925(v=OCS.15)
ms:contentKeyID: 49890371
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定同盟路由與媒體流量

 

_**上次修改主題的時間：** 2012-10-16_

同盟是兩個或兩個以上 SIP 網域間的信任關係，其可允許不同組織中的使用者跨越網路界限進行通訊。在您移轉至 Lync Server 2013 試驗集區後，您必須將 Microsoft Office Communications Server 2007 R2 Edge Server 的同盟路由轉換為 Lync Server 2013 Edge Server 的同盟路由。

請使用下列程序，將 Office Communications Server 2007 R2 Edge Server 與 Director 的同盟路由與媒體流量路由轉換至 Lync Server 2013 Edge Server，以利進行單一網站部署。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要變更同盟路由與媒體流量路由，您需要排程 Lync Server 2013 及 Office Communications Server 2007 R2 Edge Server 的維護停機時間。因此，整個轉換程序也意味著在中斷期間，無法使用同盟存取。您應將停機時間排程在預計會有最少使用者活動的時間，也應對您的使用者提供充分的通知。請仔細規劃這項中斷，並在組織內設定合理的期望。</td>
</tr>
</tbody>
</table>


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
<td>若您的舊版 Office Communications Server 2007 R2 Edge Server 是設定為使用與 Access Edge Service、Web Conferencing Edge Service 以及 A/V Edge Service 相同的 FQDN，就不支援本節中轉換同盟設定至 Lync Server 2013 Edge Server 的程序。如果舊版 Edge Service 是設定為使用相同的 FQDN，您必須先將所有使用者從 Office Communications Server 2007 R2 移轉至 Lync Server 2013，然後解除委任 Office Communications Server 2007 R2 Edge Server 後才能啟用 Lync Server 2013 Edge Server 上的同盟功能。如需詳細資訊，請參閱下列主題：
<ul>
<li><p><a href="move-remaining-users-to-lync-server-2013_1.md">將剩餘使用者移到 Lync Server 2013</a></p></li>
<li><p>＜移除伺服器與伺服器角色＞(英文)，網址為： <a href="http://go.microsoft.com/fwlink/?linkid=268790%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268790&amp;clcid=0x404</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若 XMPP 同盟是透過 Lync Server 2013 Edge Server 路由，除非所有使用者皆已移至 Lync Server 2013、已設定 XMPP 原則與憑證、已在 Lync Server 2013 設定 XMPP 同盟協力廠商，且已更新 DNS 項目，否則舊版 Office Communications Server 2007 R2 使用者將無法與 XMPP 同盟協力廠商通訊。</td>
</tr>
</tbody>
</table>


若要在新增或移除伺服器角色時順利發行、啟用或停用拓撲，您應該以 RTCUniversalServerAdmins 和 Domain Admins 群組成員的使用者身分登入。此外也可委派正確的使用者權限來新增伺服器角色。如需詳細資訊，請參閱 Standard Edition Server 或 Enterprise Edition Server 部署文件中的＜ [在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)＞。若要進行其他設定變更，則僅需要 RTCUniversalServerAdmins 群組的成員資格。

## 移除 Lync Server 2013 站台上的舊版同盟關聯

1.  使用拓撲產生器開啟試驗集區。

2.  在左窗格中，瀏覽至該網站節點。

3.  以滑鼠右鍵按一下網站，然後按一下 \[編輯屬性\] 。

4.  選取左窗格中的 \[同盟路由\] 。

5.  在網站同盟路由指派下，清除 \[啟用 SIP 同盟\] 旁的核取方塊，透過 \[BackCompatSite\] 停用同盟路由。
    
    ![\[編輯內容\] 對話方塊，同盟路由](images/JJ721925.2a80c103-c0cc-43ed-ba00-420f9add006a(OCS.15).jpg "[編輯內容] 對話方塊，同盟路由")

6.  按一下 \[確定\] ，以關閉 \[編輯屬性\] 頁面。

7.  在 \[拓撲產生器\] 中，選取頂端節點 \[Lync Server\] 。

8.  在 \[動作\] 功能表中，按一下 \[發行拓撲\] ，然後完成精靈。

## 將舊版 Edge Server 設定成非同盟 Edge Server

1.  從 \[拓撲建置器\] 的 \[動作\] 功能表中，按一下 \[合併 Office Communications Server 2007 R2 拓撲\] 。

2.  按 \[下一步\] 繼續。

3.  在 \[指定 Edge 設定\] 中，選取您目前設定以進行同盟的 \[Edge Server 內部 FQDN\] ，然後按一下 \[變更\] 。
    
    ![合併 OCS 2007 R2 拓撲，指定 Edge 設定](images/JJ721925.42c15aaf-c1ac-4fb1-a086-665835c57b23(OCS.15).jpg "合併 OCS 2007 R2 拓撲，指定 Edge 設定")

4.  按 \[下一步\] 並接受預設值，直到抵達 \[指定外部 Edge\] 頁面為止：
    
    ![拓撲產生器的 \[指定外部 Edge\] 頁面](images/JJ205243.32e97ce5-92f0-477e-8125-5d2ece237b13(OCS.15).jpg "拓撲產生器的 [指定外部 Edge] 頁面")

5.  在 \[指定外部 Edge\] 中，清除 \[此 Edge 集區是用於同盟和公用 IM 連線\] 核取方塊。這樣就會移除與 BackCompatSite 的同盟關聯。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此步驟非常重要。您必須清除這個選項，以移除舊版的同盟關聯。</td>
    </tr>
    </tbody>
    </table>


6.  按 \[下一步\] 並接受精靈剩餘頁面的預設值。

7.  在 \[摘要\] 中按 \[下一步\] ，以開始合併拓撲。

8.  在 \[狀態\] 欄位中，檢查其值是否為 \[成功\] ，然後按一下 \[完成\] 關閉精靈。

9.  在 \[動作\] 功能表中，選取 \[發行拓撲\] ，然後按 \[下一步\] 。

10. 當 \[發行精靈\] 完成之後，按一下 \[完成\] ，以關閉精靈。
    
    ![具有合併之後顯示之網站的拓撲產生器](images/JJ721925.92b679ad-332f-49aa-b4e2-19f939b711ca(OCS.15).jpg "具有合併之後顯示之網站的拓撲產生器")
    
    如上圖所示，\[站台同盟路由指派\] 下的 \[SIP 同盟\] 會設為 \[停用\] 。

## 在 Lync Server 2013 Edge Server 上設定憑證

1.  匯出舊版 Office Communications Server 2007 R2 Edge Server 的 Access Proxy 外部憑證與私密金鑰。

2.  在 Lync Server 2013 Edge Server 中，匯入上一個步驟所述的 Access Proxy 外部憑證。

3.  將 Access Proxy 外部憑證指派給 Lync Server 2013 Edge Server 的外部介面。

4.  請不要變更 Lync Server 2013 Edge Server 的內部介面憑證。

## 若要變更 Office Communications Server 2007 同盟路由以使用 Lync Server 2013 Edge Server

1.  在 Office Communications Server 2007 R2Standard Edition 伺服器 或 前端伺服器 上，開啟 Office Communications Server 2007 R2 系統管理工具。

2.  在左窗格中，展開頂端節點，以滑鼠右鍵按一下 \[樹系\] 節點。選取 \[內容\] ，然後按一下 \[通用內容\] 。

3.  按一下 \[同盟\] 索引標籤。

4.  選取核取方塊以啟用同盟與公用 IM 連線。

5.  輸入 Lync Server 2013  Edge Server 的 FQDN，然後按一下 \[確定\] 。
    
    ![OCS 通用內容，\[同盟\] 索引標籤](images/JJ721925.da633f72-43c6-4dac-8d37-ccd0dcde79c9(OCS.15).jpg "OCS 通用內容，[同盟] 索引標籤")

## 開啟 Lync Server 2013 Edge Server 同盟

1.  在拓撲產生器的左側窗格中，瀏覽至 \[Edge 集區\] Lync Server 2013 節點。

2.  展開節點，再以滑鼠右鍵按一下所列出的 \[ Edge Server\]，然後按一下 \[編輯屬性\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您僅可為單一 Edge 集區啟用同盟。如果您有多個 Edge 集區，請選取一個來做為同盟 Edge 集區。</td>
    </tr>
    </tbody>
    </table>


3.  選取 \[一般\] 頁面的 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 核取方塊。
    
    ![編輯內容，一般，啟用 Edge 同盟](images/JJ688121.cc79a88c-cce4-4cab-80ad-4f70325dc7c4(OCS.15).jpg "編輯內容，一般，啟用 Edge 同盟")

4.  按一下 \[確定\] ，以關閉 \[編輯屬性\] 頁面。

5.  然後，瀏覽至網站節點。

6.  以滑鼠右鍵按一下網站，然後按一下 \[編輯屬性\] 。

7.  在左窗格中，按一下 \[同盟路由\] 。

8.  在 \[網站同盟路由指派\] 下，選取 **啟用 SIP 同盟**，然後從清單中選取其中所列的 Lync Server 2013  Edge Server。

9.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。
    
    ![編輯內容，一般，關聯 Edge 集區](images/JJ721925.33d43297-10cd-412e-bf4a-a1d9a84b9009(OCS.15).jpg "編輯內容，一般，關聯 Edge 集區")
    
    如有部署多個網站，請逐一在各個網站上完成此程序。

## 若要設定 Lync Server 2013 Edge Server 輸出媒體路徑

1.  從 \[拓撲建置器\] 瀏覽至 \[Standard Edition 前端伺服器\] 或 \[Enterprise Edition 前端集區\] 下方的 Lync Server 2013 集區。

2.  以滑鼠右鍵按一下集區，然後按一下 \[編輯屬性\] 。

3.  選取 \[關聯\] 區段底下的 \[關聯 Edge 集區 (適用於媒體元件)\] 核取方塊。

4.  從下拉式清單中，選取 Lync Server 2013 Edge Server。
    
    ![\[編輯內容\] 對話方塊，關聯 Edge 集區](images/JJ721925.0cb76b08-5923-4972-8d7a-a829cb77136b(OCS.15).jpg "[編輯內容] 對話方塊，關聯 Edge 集區")

5.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。

## 發行 Edge Server 的設定變更

1.  在 \[拓撲產生器\] 中，選取頂端節點 \[Lync Server\] 。

2.  在 **\[動作\]** 功能表中，按一下 \[發行拓撲\] ，然後完成精靈。

3.  等候部署中所有集區的 Active Directory 複寫作業開始。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您將會見到下列訊息：<br />
    <strong>警告：拓撲包含多個同盟 Edge Server。移轉至最新版本的產品時可能會發生此問題。在這個情況下，僅會啟動一個 Edge Server 以主動用於同盟。請確認外部 DNS SRV 記錄有指向正確的 Edge Server。若您想同時部署多部主動的同盟 Edge Server (亦即，不是在移轉案例中)，請確認所有同盟協力廠商都是使用 Office Communications Server 2007 R2 或 Lync Server，並確認外部 DNS SRV 記錄有提列所有啟用同盟的 Edge Servers。</strong><br />
    此為預期中的警告，可以不予理會。</td>
    </tr>
    </tbody>
    </table>


## 驗證同盟及外部使用者的遠端存取

1.  從 Lync Server 2013 前端伺服器開啟 Lync Server 管理命令介面。

2.  要驗證同盟與遠端存取的狀態，請在命令列中輸入下列命令：
    
        Get-CsAccessEdgeConfiguration

3.  要啟用同盟與遠端存取的狀態，請在命令列中輸入下列命令：
    
        Set-CsAccessEdgeConfiguration
    
    如需這些 Cmdlet 的詳細資訊，請參閱下列主題： [Get-CsAccessEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAccessEdgeConfiguration) 與 [Set-CsAccessEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsAccessEdgeConfiguration)。

4.  讓 Lync Server 2013 Edge Server 上線並測試同盟與外部存取前，請先等待複寫完成。

## 設定 Lync Server 2013 Edge Server

1.  將所有 Lync Server 2013 Edge Server 上線。

2.  將外部防火牆的路由規則或硬體負載平衡設定，更新成將外部存取 (通常是連接埠 443) 及同盟 (通常是連接埠 5061) 的 SIP 流量傳送至 Lync Server 2013  Edge Server，不是傳送至舊版 Edge Server。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您沒有硬體負載平衡器，您必須更新同盟的 DNS A 記錄，才能解析新的 Lync Server Access Edge Server。要在盡量不中斷服務的情況下完成此工作，請降低外部 Lync Server Access Edge FQDN 的 TTL 值，這樣 DNS 更新並指向新的 Lync Server Access Edge Server 時，同盟與遠端存取才能快速更新。</td>
    </tr>
    </tbody>
    </table>


3.  接下來，停止每部 Edge Server 電腦的 \[Lync Server Server Access Edge\] 。

4.  從每部舊版 Edge Server 電腦上的 \[系統管理工具\] ，開啟 \[服務\] 小程式。

5.  在服務清單中，尋找 **Office Communications Server Access Edge** 。

6.  以滑鼠右鍵按一下服務名稱，然後選取 \[停止\] 來停止服務。

7.  將 \[啟動類型\] 設為 \[停用\] 。

8.  按一下 \[確定\] ，以關閉 \[屬性\] 視窗。

## 測試外部使用者與外部存取連線能力

  - 使用者至少要一個來自同盟網域、, an internal user on Lync Server 2013 的內部使用者及 Office Communications Server 2007 R2 的使用者。測試立即訊息 (IM)、目前狀態、音訊/視訊 (A/V) 及桌面共用。

  - 讓各個組織支援 (且已佈建完成) 的公用 IM 服務提供者的使用者與 Lync Server 2013 上的使用者及 Office Communications Server 2007 R2 上的使用者進行通訊。

  - 確認匿名使用者可以加入會議。

  - 位於 Office Communications Server 2007 R2 上並使用遠端使用者存取的使用者 (非使用 VPN 而從內部網路外部登入 Office Communications Server 2007 R2) 與位於 Lync Server 2013 上的使用者，以及位於 Office Communications Server 2007 R2 上的使用者。測試 IM、目前狀態、A/V 及桌面共用。

  - 位於 Lync Server 2013 上並使用遠端使用者存取的使用者 (非使用 VPN 而從內部網路外部登入 Lync Server 2013) 與位於 Lync Server 2013 上的使用者，以及位於 Office Communications Server 2007 R2 上的使用者。測試 IM、目前狀態、A/V 及桌面共用。


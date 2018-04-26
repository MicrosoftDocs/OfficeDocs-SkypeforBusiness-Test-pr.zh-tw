---
title: 設定同盟路由與媒體流量
TOCTitle: 設定同盟路由與媒體流量
ms:assetid: 8b2f5f81-a955-4ad1-ad74-397322ff9521
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688121(v=OCS.15)
ms:contentKeyID: 49890193
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定同盟路由與媒體流量

 

_**上次修改主題的時間：** 2012-10-15_

同盟是兩個或兩個以上 SIP 網域間的信任關係，其可允許不同組織中的使用者跨越網路界限進行通訊。在您移轉至 Lync Server 2013 試驗集區後，您必須將 Lync Server 2010 Edge Server 的同盟路由轉換為 Lync Server 2013 Edge Server 的同盟路由。

請使用下列程序，將 Lync Server 2010 Edge Server 與 Director 的同盟路由與媒體流量路由轉換至 Lync Server 2013 Edge Server，以利進行單一網站部署。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要變更同盟路由與媒體流量路由，您需要排程 Lync Server 2013 及 Lync Server 2010 Edge Server 的維護停機時間。因此，整個轉換程序也意味著在中斷期間，無法使用同盟存取。您應將停機時間排程在預計會有最少使用者活動的時間，也應對您的使用者提供充分的通知。請仔細規劃這項中斷，並在組織內設定合理的期望。</td>
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
<td>若您的舊版 Lync Server 2010 Edge Server 是設定為使用與 Access Edge Service、Web Conferencing Edge Service 及 A/V Edge Service 相同的 FQDN，就不支援本節中的程序。如果舊版 Edge Service 是設定為使用相同的 FQDN，您必須先將所有使用者從 Lync Server 2010 移轉至 Lync Server 2013，然後解除委任 Lync Server 2010 Edge Server 後才能啟用 Lync Server 2013 Edge Server 上的同盟功能。</td>
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
<td>若 XMPP 同盟是透過 Lync Server 2013 Edge Server 路由，則除非所有使用者皆已移至 Lync Server 2010、已設定 XMPP 原則與憑證、已在 Lync Server 2013 設定 XMPP 同盟合作夥伴，且已更新 DNS 項目，否則舊版 Lync Server 2013 使用者將無法與 XMPP 同盟合作夥伴通訊。</td>
</tr>
</tbody>
</table>


## 從 Lync Server 2013 網站移除舊版同盟關聯

1.  在 Lync Server 2013 前端伺服器上，於拓撲產生器中開啟現有的拓撲。

2.  在左窗格中，瀏覽至該網站節點，此節點位於 **Lync Server** 的正下方。

3.  以滑鼠右鍵按一下網站，然後按一下 \[編輯內容\] 。

4.  在左側窗格中，選取 \[同盟路由\]。

5.  在 \[網站同盟路由指派\] 下方，清除 \[啟用 SIP 同盟\] 核取方塊，以停用透過舊版 Lync Server 2010 環境進行的同盟路由。
    
    ![\[編輯內容\] 對話方塊，\[同盟路由\] 頁面](images/JJ688121.8d755ae0-fc7d-4253-b0db-0cf31b863c55(OCS.15).jpg "[編輯內容] 對話方塊，[同盟路由] 頁面")

6.  按一下 \[確定\] ，以關閉 \[編輯屬性\] 頁面。

7.  在 \[拓撲產生器\] 中，選取頂端節點 \[Lync Server\] 。

8.  從 \[動作\] 功能表中，按一下 \[發行拓撲\] 。

9.  按 \[下一步\] 以完成發行程序，然後在發行程序完成時按一下 \[完成\] 。

## 將舊版 Edge Server 設定成非同盟 Edge Server

1.  在左窗格中，瀏覽至 \[Lync Server 2010\] 節點，然後瀏覽至 \[Edge 集區\] 節點。

2.  以滑鼠右鍵按一下 Edge Server，然後按一下 \[編輯內容\] 。

3.  選取左窗格中的 \[一般\] 。

4.  清除 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 核取方塊，然後選取 \[確定\] 以關閉頁面。
    
    ![編輯內容，一般，清除啟用同盟](images/JJ688121.3be2c8c0-9ed9-4544-bafd-b7694271fafc(OCS.15).jpg "編輯內容，一般，清除啟用同盟")

5.  在 \[動作\] 功能表中，選取 \[發行拓撲\] ，然後按 \[下一步\] 。

6.  當 \[發行精靈\] 完成之後，按一下 \[完成\] ，以關閉精靈。

7.  確認舊版 Edge Server 的同盟已停用。
    
    ![拓撲產生器，Edge 集區，已停用同盟](images/JJ688121.a2948438-d51a-4aeb-9eaa-d899ca950758(OCS.15).jpg "拓撲產生器，Edge 集區，已停用同盟")

## 在 Lync Server 2010 Edge Server 上設定憑證

1.  匯出舊版 Lync Server 2010 Edge Server 的 Access Proxy 外部憑證與私密金鑰。

2.  在 Lync Server 2013 Edge Server 中，匯入上一個步驟所述的 Access Proxy 外部憑證。

3.  將 Access Proxy 外部憑證指派給 Lync Server 2013 Edge Server 的外部介面。

4.  Lync Server 2013 Edge Server 的內部介面憑證應該從信任的 CA 進行要求並加以指派。

## 變更 Lync Server 2010 同盟路由以使用 Lync Server 2013 Edge Server

1.  在 \[拓撲產生器\] 的左窗格中，瀏覽至 \[Lync Server 2013\] 節點，然後瀏覽至 \[Edge 集區\] 節點。

2.  以滑鼠右鍵按一下 Edge Server，然後按一下 \[編輯內容\] 。

3.  選取左窗格中的 \[一般\] 。

4.  選取 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 的核取方塊，然後按一下 \[確定\] 以關閉頁面。
    
    ![\[編輯內容\] 對話方塊，\[一般\] 頁面](images/JJ688121.cc79a88c-cce4-4cab-80ad-4f70325dc7c4(OCS.15).jpg "[編輯內容] 對話方塊，[一般] 頁面")

5.  在 \[動作\] 功能表中，選取 \[發行拓撲\] ，然後按 \[下一步\] 。

6.  當 \[發行精靈\] 完成之後，按一下 \[完成\] ，以關閉精靈。

7.  確認已將 \[同盟 (連接埠 5061)\] 設定為 \[啟用\] 。
    
    ![拓撲產生器，Edge 集區，已啟用同盟](images/JJ688121.e8ccdada-23f4-47e5-a99d-5bf795fefc48(OCS.15).jpg "拓撲產生器，Edge 集區，已啟用同盟")

## 更新 Lync Server 2013 Edge Server 同盟的下一個躍點

1.  在 \[拓撲產生器\] 的左窗格中，瀏覽至 \[Lync Server 2013\] 節點，然後瀏覽至 \[Edge 集區\] 節點。

2.  展開節點，再以滑鼠右鍵按一下所列出的 Edge Server，然後按一下 \[編輯內容\] 。

3.  在 \[一般\] 頁面的 \[下一個躍點選取範圍\] 下方，從下拉式清單中選取 Lync Server 2013  集區。
    
    ![\[編輯內容\] 對話方塊，\[下一個躍點\] 頁面](images/JJ688121.5741b9a8-e729-4457-9f62-38f08a2c5b02(OCS.15).jpg "[編輯內容] 對話方塊，[下一個躍點] 頁面")

4.  按一下 \[確定\] ，以關閉 \[編輯屬性\] 頁面。

5.  在 \[拓撲產生器\] 中，選取頂端節點 \[Lync Server\] 。

6.  在 \[動作\] 功能表中，按一下 \[發行拓撲\] ，然後完成精靈。

## 若要設定 Lync Server 2013 Edge Server 輸出媒體路徑

1.  在 \[拓撲產生器\] 的左窗格中，瀏覽至 \[Lync Server 2013\] 節點，然後瀏覽至 \[Standard Edition 前端伺服器\] 下方的集區或 \[Enterprise Edition 前端集區\] 。

2.  以滑鼠右鍵按一下集區，然後按一下 \[編輯屬性\] 。

3.  選取 \[關聯\] 區段底下的 \[關聯 Edge 集區 (適用於媒體元件)\] 核取方塊。
    
    ![編輯內容，一般，關聯 Edge 集區](images/JJ688121.fd9b18ca-fda2-4764-9bf0-726bf39f6a12(OCS.15).jpg "編輯內容，一般，關聯 Edge 集區")

4.  從下拉式清單中，選取 Lync Server 2013 Edge Server。

5.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。

## 開啟 Lync Server 2013 Edge Server 同盟

1.  在 \[拓撲產生器\] 的左窗格中，瀏覽至 \[Lync Server 2013\] 節點，然後瀏覽至 \[Edge 集區\] 節點。

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


3.  在 \[一般\] 頁面中，確認已勾選 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 設定。
    
    ![\[編輯內容\] 對話方塊，\[一般\] 頁面](images/JJ688121.cc79a88c-cce4-4cab-80ad-4f70325dc7c4(OCS.15).jpg "[編輯內容] 對話方塊，[一般] 頁面")

4.  按一下 \[確定\] ，以關閉 \[編輯屬性\] 頁面。

5.  然後，瀏覽至網站節點。

6.  以滑鼠右鍵按一下網站，然後按一下 \[編輯屬性\] 。

7.  在左窗格中，按一下 \[同盟路由\] 。

8.  在 \[網站同盟路由指派\] 下，選取 **啟用 SIP 同盟**，然後從清單中選取其中所列的 Lync Server 2013  Edge Server。
    
    ![編輯內容，\[同盟路由\] 頁面](images/JJ688121.c50c13b8-0859-4e3e-8793-45c431a5b4b5(OCS.15).jpg "編輯內容，[同盟路由] 頁面")

9.  按一下 \[確定\] 以關閉 \[編輯屬性\] 頁面。
    
    如有部署多個網站，請逐一在各個網站上完成此程序。

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
    <strong>警告：拓撲包含多部同盟 Edge Server。移轉至最新版本的產品時可能會發生此問題。在這個情況下，只能有一部作用中 Edge Server 用於同盟。如果您要部署多部同盟 Edge Server 以同時作用 (也就是非移轉案例)，請確認所有同盟協力廠商都是使用 Lync Server，並確認外部 DNS SRV 記錄會列出所有啟用同盟的 Edge Server。</strong><br />
    此為預期中的警告，可以不予理會。</td>
    </tr>
    </tbody>
    </table>


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
    <td>如果您沒有硬體負載平衡器，就需要更新同盟的 DNS A 記錄，以解析至新的 Lync Server Access Edge Server。若要完成此工作並將干擾降至最低，請減少外部 Lync Server Access Edge FQDN 的 TLL 值，如此一來，在更新 DNS 以指向新的 Lync Server Access Edge 時，將會快速更新同盟與遠端存取。</td>
    </tr>
    </tbody>
    </table>


3.  接著，在每部 Edge Server 電腦上停止 \[Lync Server Access Edge\] 。

4.  從每部舊版 Edge Server 電腦上的 \[系統管理工具\] ，開啟 \[服務\] 小程式。

5.  在服務清單中，尋找 \[Lync Server Access Edge\] 。

6.  以滑鼠右鍵按一下服務名稱，然後選取 \[停止\] 來停止服務。

7.  將 \[啟動類型\] 設為 \[停用\] 。

8.  按一下 \[確定\] ，以關閉 \[屬性\] 視窗。


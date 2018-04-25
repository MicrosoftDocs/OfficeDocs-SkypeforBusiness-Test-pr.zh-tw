---
title: Lync Server 2013：設定 Edge Server 的網路介面
TOCTitle: 設定 Edge Server 的網路介面
ms:assetid: b0aecdf6-4ae2-46f6-b9b6-948bfc3df11e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412847(v=OCS.15)
ms:contentKeyID: 49292033
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Edge Server 的網路介面

 

_**上次修改主題的時間：** 2012-09-08_

每個 Edge Server 都是具有對外和對內介面的多重目錄電腦。介面卡網域名稱系統 (DNS) 設定取決於周邊網路中是否有 DNS 伺服器。如果 DNS 伺服器存在於周邊中，它們必須有一個包含一或多個 DNS A 記錄的區域，以用於下一個躍點伺服器或集區 (也就是，Director 集區或指定的前端集區)，以及將名稱查閱參照到其他公用 DNS 伺服器的外部查詢。如果沒有任何 DNS 伺服器存在於周邊中，則 Edge Server 會使用外部 DNS 伺服器來解析網際網路名稱查閱，且每個 Edge Server 會使用 HOST 將下一個躍點伺服器名稱解析為 IP 位址。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />安全性 附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>基於安全性理由，建議您不要讓 Edge Server 存取內部網路中的 DNS 伺服器。</td>
</tr>
</tbody>
</table>


## 若要設定周邊網路中具有 DNS 伺服器的介面

1.  為每個 Edge Server 安裝兩個網路介面卡，一個用於向內介面，另一個用於向外介面。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>內部和外部子網路必須不能互相路由傳送。</td>
    </tr>
    </tbody>
    </table>


2.  在外部介面的外部周邊網路 (也稱為 DMZ、非軍事區或遮蔽式子網路) 子網路上設定三個靜態 IP 位址，並將預設閘道指向外部防火牆的內部介面。設定介面卡 DNS 設定，以指向一對周邊 DNS 伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用於此介面的 IP 位址可以少到只有一個，但是若要這麼做，需要將連接埠指派變更為非標準值。當您在 拓撲產生器中建立拓撲時會決定此項。</td>
    </tr>
    </tbody>
    </table>


3.  在內部介面的內部周邊網路子網路上設定一個靜態 IP 位址，且不要設定預設閘道。設定介面卡 DNS 設定，以指向至少一個 DNS 伺服器，最好是一對周邊 DNS 伺服器。

4.  在內部介面上建立持續性靜態路由，以傳送到用戶端、 Lync Server 2013 和 Exchange Unified Messaging (UM) 伺服器所在的所有內部網路。

## 設定周邊網路中沒有 DNS 伺服器的介面

1.  為每個 Edge Server 安裝兩個網路介面卡，一個用於向內介面，另一個用於向外介面。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>內部和外部子網路必須不能互相路由傳送。</td>
    </tr>
    </tbody>
    </table>


2.  在外部介面的外部周邊網路子網路上設定三個靜態 IP 位址。同時在外部介面上設定預設閘道。例如，將面向網際網路的路由器或外部防火牆定義為預設閘道。設定 DNS 設定，以指向 DNS 伺服器，最好是一對外部 DNS 伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可以只在外部介面使用一個 IP 位址，但不建議此作法。若要這麼做，就需要將連接埠指派變更為非標準值，並且變更為非預設的連接埠 433，433 通常是用戶端通訊所用來繞過防火牆的連接埠。當您在 拓撲產生器中建立拓撲時可決定 IP 位址設定與連接埠設定。</td>
    </tr>
    </tbody>
    </table>


3.  在內部介面的內部周邊網路子網路上設定一個靜態 IP 位址，且不要設定預設閘道。將介面卡 DNS 設定保留空白。

4.  在內部介面上建立持續性靜態路由，以傳送到 Lync 用戶端或執行 Lync Server 2013 所在之伺服器的所有內部網路。

5.  在每個 Edge Server 上編輯 HOST 檔案，以包含下一個躍點伺服器或虛擬 IP (VIP) 的記錄 (記錄將是在 拓撲產生器中設定為 Edge Server 下一個躍點位址的 Director、Standard Edition Server 或前端集區)。如果您要使用 DNS 負載平衡，請為下一個躍點集區的每個成員加入一行。


---
title: Lync Server 2013：使用拓撲產生器定義其他主幹
TOCTitle: 使用拓撲產生器定義其他主幹
ms:assetid: e68b8377-50a2-452a-bf5c-910929e34236
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721915(v=OCS.15)
ms:contentKeyID: 49890357
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用拓撲產生器定義其他主幹

 

_**上次修改主題的時間：** 2012-10-04_

請依照下列步驟使用 拓撲產生器，以定義您可讓 *「對等」* 與 中繼伺服器建立關聯的其他主幹。對等可讓 企業語音允許的使用者連線到公用交換電話網路 (PSTN)。對等可以是 PSTN 閘道、IP-PBX 或網際網路電話語音服務提供者 (ITSP) 上的工作階段界限控制器 (SBC)。主幹定義 中繼伺服器與對等之間的連線。一個 中繼伺服器可定義多個主幹。一個 中繼伺服器可與多個對等建立關聯。

主幹是 中繼伺服器與閘道 (專門由 Tuple 識別) 之間的邏輯連接：

{ 中繼伺服器 FQDN, 中繼伺服器聆聽連接埠 (TLS 或 TCP)：閘道 IP 與 FQDN、閘道聆聽連接埠}

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題假設您已設定 PSTN 閘道與根主幹，且至少有一個組合的或獨立式的 中繼伺服器，或如同部署文件的＜ <a href="lync-server-2013-define-a-gateway-in-topology-builder.md">在 Lync Server 2013 中於拓撲產生器內定義閘道</a>＞所述的集區。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題假設您已在至少一個中央網站中安裝至少一個 前端集區或 Standard Edition 伺服器，如同部署文件所述的＜ <a href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server</a>＞與＜ <a href="lync-server-2013-publish-the-topology.md">在 Lync Server 2013 中發行拓撲</a>＞。</td>
</tr>
</tbody>
</table>


## 定義 中繼伺服器與閘道對等之間的其他主幹

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 Lync Server 2013 下，您的網站名稱，\[共用元件\] ，在 \[主幹\] 節點上按一下滑鼠右鍵，然後按一下 \[新主幹\] 。
    
    ![Lync Server 拓撲產生器檔案結構畫面](images/JJ721915.90d5b349-aa1e-407a-87ed-fa112f478560(OCS.15).png "Lync Server 拓撲產生器檔案結構畫面")

3.  在 \[定義新主幹\] 中，指定一個好記的名稱，專門識別主幹。兩個主幹不能共用同一個名稱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您指定傳輸層安全性 (TLS) 作為傳輸類型，則必須指定 中繼伺服器對等的 FQDN，而非 IP 位址。</td>
    </tr>
    </tbody>
    </table>


4.  在 \[相關的 PSTN 閘道\] 下，選擇 PSTN 閘道對等，與此主幹建立關聯。
    
    ![主幹之 PSTN 閘道對等的內容設定](images/JJ721915.7c3fe8ee-8f4c-4413-8462-8347228e61bb(OCS.15).png "主幹之 PSTN 閘道對等的內容設定")

5.  在 \[PSTN 閘道的聆聽連接埠\] 下，輸入對等 (PSTN 閘道、IP-PBX 或 SBC) 要從 中繼伺服器 (要與本主幹建立關聯的) 接收 SIP 訊息的聆聽連接埠。傳輸控制通訊協定 (TCP) 的預設對等連接埠為 5066，傳輸層安全性 (TLS) 的預設對等連接埠則為 5067。TCP 的預設 Survivable Branch Appliance 連接埠為 5081，TLS 的預設對等連接埠則為 5082。

6.  在 \[SIP 傳輸通訊協定\] 下，按一下對等使用的傳輸類型。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>基於安全性理由，強烈建議您將對等部署至可使用 TLS 的 中繼伺服器。</td>
    </tr>
    </tbody>
    </table>


7.  在 \[相關中繼伺服器\] 下選擇 中繼伺服器集區，與此對等的根主幹建立關聯

8.  在 \[相關的中繼伺服器連接埠\] 下，輸入 中繼伺服器要從對等接收 SIP 訊息的聆聽連接埠。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>由於 Lync Server 2013 支援多個主幹，因此兩個不同主幹名稱的主幹不能以同一個 [相關 中繼伺服器連接埠] 與 [IP/PSTN 閘道的聆聽連接埠] 設定</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>由於 Lync Server 2013 支援多個支幹，因此 中繼伺服器可定義多個 SIP 訊號連接埠，以便與多個對等通訊。定義主幹時，[相關 中繼伺服器連接埠] 號碼不得超過 中繼伺服器允許各個通訊協定所有的聆聽連接埠範圍。此連接埠範圍是在 Lync Server 2013 與 中繼伺服器集區下設定。在相關的 中繼伺服器集區上按滑鼠右鍵，然後選擇 [編輯內容] 。在 [聆聽連接埠] 欄位中指定連接埠範圍。</td>
    </tr>
    </tbody>
    </table>


9.  按一下 \[確定\] 。

## 請參閱

#### 工作

[在 Lync Server 2013 的拓撲產生器中修改主幹](lync-server-2013-modify-a-trunk-in-topology-builder.md)


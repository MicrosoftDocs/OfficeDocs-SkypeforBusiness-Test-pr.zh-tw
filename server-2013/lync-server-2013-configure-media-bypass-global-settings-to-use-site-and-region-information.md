---
title: 在 Lync Server 2013 中設定媒體旁路全域設定以使用網站和區域資訊
TOCTitle: 在 Lync Server 2013 中設定媒體旁路全域設定以使用網站和區域資訊
ms:assetid: 0a21cdf1-f350-49da-b346-70806f256bea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398150(v=OCS.15)
ms:contentKeyID: 49290032
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定媒體旁路全域設定以使用網站和區域資訊

 

_**上次修改主題的時間：** 2012-09-21_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題假設您已經針對您希望媒體略過中繼伺服器的特定網站或服務，對於從中繼伺服器至對等 (網際網路電話語音服務提供者 (ITSP) 的公用交換電話網路 (PSTN) 閘道、IP-PBX 或工作階段界限控制器 (SBC)) 的任何主幹連線設定媒體旁路。<br />
本主題還假設您已用符合您根據<a href="lync-server-2013-create-or-modify-a-network-region.md">在 Lync Server 2013 中建立或修改網路地區</a>、<a href="lync-server-2013-create-or-modify-a-network-site.md">在 Lync Server 2013 中建立或修改網站</a>及<a href="lync-server-2013-associate-a-subnet-with-a-network-site.md">在 Lync Server 2013 中建立子網路與網路站台的關聯</a>中的步驟執行之網路地區、網路網站和子網路設定的方式，在拓撲產生器中定義所有的中央網站和分支網站。如果不符合，則媒體旁路會失敗。</td>
</tr>
</tbody>
</table>


除了針對與對等關聯的個別主幹連線啟用媒體旁路以外，您也必須設定全域設定。如果您使用本主題中的步驟來設定媒體旁路的全域設定，則假設下列其中一種或兩種情況會影響您的設定：

  - 在 Lync Server 端點和您在主幹連線上設定媒體旁路的任何對等之間*沒有*適當連線。

  - 已啟用頻寬管理的通話許可控制 (CAC)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需有關通話許可控制和媒體旁路的考量詳細資訊，請參閱規劃文件中＜<a href="lync-server-2013-media-bypass-and-mediation-server.md">Lync Server 2013 中的媒體旁路和中繼伺服器</a>＞的＜PSTN 連線的通話許可控制＞一節。</td>
    </tr>
    </tbody>
    </table>


若已啟用通話許可控制與媒體旁路進階 Enterprise Voice 功能，則網路地區和網路網站資訊會由這兩項功能共用。因此，如果您已經設定通話許可控制，則不需要使用下列程序特別針對媒體旁路來編輯網站與地區資訊。如果您尚未設定通話許可控制的網路地區和網站，而想要變更媒體旁路設定，請遵循此程序中的步驟。

或者，如果您想要使用網站與地區資訊進行旁路決策，但無意啟用通話許可控制，請遵循下列步驟。在這種情況下，仍需透過＜[在 Lync Server 2013 中建立網路站間原則](lync-server-2013-create-network-intersite-policies.md)＞中所述的網路網站間原則來呈現頻寬受限連結。因為尚未啟用通話許可控制，所以在此情況下實際頻寬限制沒那麼重要。這些連結會用來分割子網路，以指定沒有頻寬限制，因而可運用媒體旁路的子網路。請注意，若已同時啟用通話許可控制和媒體旁路，情形也是如此。

此外，為了使旁路正常運作，在拓撲產生器中定義的網站與您設定網路地區和網路網站時所定義的網站必須一致。例如，若您在拓撲產生器中定義的分支網站只部署了一個 PSTN 閘道，則必須設定該分支網站的 Enterprise Voice 原則，讓分支網站使用者能夠透過分支網站的 PSTN 閘道傳送其 PSTN 通話。

## 設定媒體旁路的網站與地區資訊

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]**。

3.  連按兩下表格中的 **\[全域\]** 組態。

4.  在 **\[編輯通用設定\]** 頁面上，選取 **\[啟用媒體旁路\]** 核取方塊。

5.  按一下 **\[使用網站和地區設定\]**。

6.  如有必要，請選取 **\[啟用非對應網站的旁路\]** 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有一或多個與相同區域關聯的大型網站沒有頻寬限制 (例如，大型中央網站)，但也有一些與相同區域關聯的分支網站具有頻寬限制，請選取此核取方塊。當您啟用非對應網站的旁路時，設定作業比較精簡，因為您只需指定與分支網站關聯的子網路，而不需指定與所有網站關聯的所有子網路。如果已啟用通話許可控制，則建議您不要選取此核取方塊。</td>
    </tr>
    </tbody>
    </table>


7.  按一下 **\[認可\]**。

接著，如＜[將子網路與媒體旁路的網站關聯](lync-server-2013-associate-subnets-with-network-sites-for-media-bypass.md)＞中所述，將子網路新增至網路網站 (＜[在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)＞說明讓子網路與網路網站產生關聯的實際程序)。在您讓所有子網路與網路網站產生關聯之後，媒體旁路部署便已完成。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您尚未建立網路地區和網路網站，您必須先予以建立，才能繼續進行媒體旁路部署。如需詳細資訊，請參閱＜<a href="lync-server-2013-create-or-modify-a-network-region.md">在 Lync Server 2013 中建立或修改網路地區</a>＞及＜<a href="lync-server-2013-create-or-modify-a-network-site.md">在 Lync Server 2013 中建立或修改網站</a>＞。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[將子網路與媒體旁路的網站關聯](lync-server-2013-associate-subnets-with-network-sites-for-media-bypass.md)


---
title: Lync Server 2013：規劃混合式 Lync Server 部署
TOCTitle: 規劃混合式 Lync Server 部署
ms:assetid: f8b3d240-bc2e-42c9-acf8-d532d641a14c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205403(v=OCS.15)
ms:contentKeyID: 49292866
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 規劃 Lync Server 2013 混合式部署

 

_**上次修改主題的時間：** 2015-08-19_

規劃混合式部署時，您必須考慮下列使用者需求及網路基礎結構。

## 基礎結構需求

您的環境必須具備下列可用項目，以便執行及設定 Lync Server 2013 混合式部署。

  - 啟用 Lync Online 的 Office 365 租用戶。

  - 內部部署或使用 Microsoft Azure 的 Active Directory Federation Services (AD FS) 伺服器。如需有關 AD FS 的詳細資訊，請參閱 [Active Directory Federation Services (AD FS) 2.0](http://go.microsoft.com/fwlink/p/?linkid=393795)，或 [設定 Windows Azure Pack 適用的 Active Directory Federation Services](http://go.microsoft.com/fwlink/p/?linkid=522475)。

  - 內部部署的 Lync Server 2013 或 Lync Server 2010 並裝有 Lync Server 2010 的累計更新 (2013 年 3 月或之後適用)。

  - Lync Server 2013 系統管理工具。

  - 目錄同步作業。如需「目錄同步作業」的詳細資訊，請參閱 [混合式身分識別管理](http://go.microsoft.com/fwlink/p/?linkid=231010)。

## Lync 用戶端支援

Lync 用戶端支援的功能與內部部署及線上環境的可用功能有些差異。您可以先檢視各種 Lync Server 設定的用戶端支援，再決定組織中要主控使用者的位置。下列用戶端在 Lync 混合部署中受 商務用 Skype Online 支援：

  - Lync 2010

  - Lync 2013

  - Lync Windows 市集應用程式

  - Lync Web App

  - Lync Mobile

  - Lync for Mac 2011

  - Lync Room System

  - Lync Basic 2013

如需用戶端支援的詳細資訊，請參閱下列主題：

  - [Lync Online 的用戶端](http://go.microsoft.com/fwlink/?linkid=281902)

  - [Lync Server 2013 的用戶端比較表](lync-server-2013-desktop-client-comparison-tables.md)

  - [Lync Server 2013 行動用戶端比較表](lync-server-2013-mobile-client-comparison-tables.md)

## 拓撲需求

如要使用 商務用 Skype Online 設定 Lync Server 2013 混合式部署，您必須具備下列其中一個受支援的拓撲：

  - 具有 Lync Server 2013 內部部署的 Microsoft Office Communications Server 2007 R2。 Lync Server 2013 同盟 Edge Server 與下一個同盟躍點伺服器 Edge Server 必須執行 Lync Server 2013，且必須部署一個「中央管理存放區」。 Edge Server 與集區必須為內部部署。
    
    > [!IMPORTANT]  
    > 雖然支援此拓撲，但部分功能可能會受限。例如，Microsoft Lync Online 使用者與內部部署 Office Communications Server 2007 R2 使用者之間的目前狀態資訊可能無法依預期運作。
    


  - 套用了 Lync Server 2010 累計更新 (2013 年 3 月) 且內部部署有 Lync Server 2013 系統管理工具的 Microsoft Lync Server 2010。同盟 Edge Server 與來自同盟的下一個躍點伺服器 Edge Server 必須執行套用 2013 年 3 月 (或之後) 累計更新的 Microsoft Lync Server 2010 或 Lync Server 2013。
    
    > [!IMPORTANT]  
    > Lync Server 2013 系統管理工具應安裝於另一個可連線到現有 Lync Server 2010 部署的伺服器上。用於將使用者從內部部署移至 Lync Online 的 Move-CsUser Cmdlet，必須從連線到內部部署的 Lync Server 2013 系統管理工具執行。
    


  - 所有伺服器皆執行 Lync Server 2013 的 Lync Server 2013 部署。

如需受支援拓撲的詳細資訊，請參閱[Lync Server 2013 中支援的拓撲](lync-server-2013-supported-topologies.md)與 [Lync Server 2013 Reference Topologies for Enterprise Hybrid Deployments](http://go.microsoft.com/fwlink/p/?linkid=398709)。

如需有關混合部署以及將 PowerShell 連接到 Lync Online 的疑難排解資訊，請參閱 [Lync Online：Lync PowerShell 和混合部署疑難排解](http://go.microsoft.com/fwlink/p/?linkid=306718) (英文)。

## 同盟允許/封鎖清單需求

「允許」網域清單包含有合作夥伴 Edge 完整網域名稱 (FQDN) 設定的網域。有時這些稱為「允許的合作夥伴伺服器」 或「直接同盟合作夥伴」 。您必須熟悉內部部署中「開放式同盟」與「封閉式同盟」的差異，它們分別稱為「合作夥伴探索」 和「允許合作夥伴網域清單」 。

如要成功設定混合式部署，必須符合下列需求：

  - 網域配對設定必須和內部部署及 Office 365 租用戶相同。如果合作夥伴探索在內部部署內啟動，那麼開放式同盟必須針對您的線上租用戶而設定。如果合作夥伴探索並未啟動，那麼封閉式同盟必須針對您的線上租用戶而設定。

  - 內部部署內的「封鎖」網域清單必須確實符合您線上租用戶的「封鎖」網域清單。

  - 內部部署內的「允許」網域清單必須確實符合您線上租用戶的「允許」網域清單。

  - 同盟必須針對線上租用戶的外部通訊進行啟動，並使用 Lync Online 控制台進行設定。

## DNS 設定

建立混合式部署的 DNS SRV 記錄時，\_sipfederationtls.\_tcp.\<網域\> 與 \_sip.\_tls.\<網域\> 記錄必須指向內部部署 Access Proxy。

## 防火牆考量因素

您網路上的電腦必須能執行標準網際網路 DNS 查閱。如果這些電腦可達到標準網際網路的網站，那麼您的網路符合此要求。

根據您 Microsoft Online Services 資料中心的位置，您也必須設定網路防火牆裝置，以接受根據萬用字元網域名稱 (如：所有來自 \*.outlook.com 的流量) 的連線。如果您組織的防火牆並不支援萬用字元名稱設定，那麼您將必須手動確定您要允許的 IP 位置範圍以及指定的連接埠。

參考＜說明＞主題 [Office 365 URL 和 IP 位址範圍](http://go.microsoft.com/fwlink/?linkid=252942)。

## 連接埠與通訊協定需求

除了內部 Lync Server 2013 通訊的連接埠需求，您也必須設定下列連接埠。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定 / 連接埠</th>
<th>應用程式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 443</p></td>
<td><p>開啟連入</p>
<ul>
<li><p>Active Directory Federation Services (同盟伺服器角色)</p>
<p>如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=281899">了解 AD FS 角色服務</a>。</p></li>
<li><p>Active Directory Federation Services (Proxy 伺服器角色)</p></li>
<li><p>Microsoft Online Services 入口網站</p></li>
<li><p>我的公司入口網站</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Lync 用戶端 (從內部部署 Lync Server 至 Lync Online 的通訊)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TCP 80 和 443</p></td>
<td><p>開啟連入</p>
<ul>
<li><p>Microsoft Online Services 目錄同步作業工具</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>TCP 5061</p></td>
<td><p>在 Edge Server 開啟連入/連出</p></td>
</tr>
<tr class="even">
<td><p>PSOM/TLS 443</p></td>
<td><p>開啟資料分享工作階段連入/連出</p></td>
</tr>
<tr class="odd">
<td><p>STUN/TCP 443</p></td>
<td><p>開啟音訊、視訊、應用程式分享工作階段連入/連出</p></td>
</tr>
<tr class="even">
<td><p>STUN/UDP 3478</p></td>
<td><p>開啟音訊及視訊工作階段連入/連出</p></td>
</tr>
<tr class="odd">
<td><p>RTP/TCP 50000-59999</p></td>
<td><p>開啟音訊及視訊工作階段連出</p></td>
</tr>
<tr class="even">
<td><p>TCP 443</p></td>
<td><p>開啟連入</p>
<ul>
<li><p>Active Directory Federation Services (同盟伺服器角色)</p>
<p>如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=281899">了解 AD FS 角色服務</a>。</p></li>
<li><p>Active Directory Federation Services (Proxy 伺服器角色)</p></li>
<li><p>Microsoft Online Services 入口網站</p></li>
<li><p>我的公司入口網站</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Lync 用戶端 (從內部部署 Lync Server 至 Lync Online 的通訊)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>TCP 80 和 443</p></td>
<td><p>開啟連入</p>
<ul>
<li><p>Microsoft Online Services 目錄同步作業工具</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TCP 5061</p></td>
<td><p>在 Edge Server 開啟連入/連出</p></td>
</tr>
<tr class="odd">
<td><p>PSOM/TLS 443</p></td>
<td><p>開啟資料分享工作階段連入/連出</p></td>
</tr>
<tr class="even">
<td><p>STUN/TCP 443</p></td>
<td><p>開啟音訊、視訊、應用程式分享工作階段連入/連出</p></td>
</tr>
<tr class="odd">
<td><p>STUN/UDP 3478</p></td>
<td><p>開啟音訊及視訊工作階段連入/連出</p></td>
</tr>
<tr class="even">
<td><p>RTP/TCP 50000-59999</p></td>
<td><p>開啟音訊及視訊工作階段連出</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 如果您需要透過執行 Office Communications Server 2007 的合作夥伴進行同盟，那麼您必須開啟連入/連出 RTP/UDP 和 RTP/TCP 連接埠 50000-59999。如需 A/V 防火牆要求條件的詳細資訊，請參閱＜ <a href="lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md">決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求</a>＞。如需連接埠與通訊協定的詳細資訊，請參閱＜ <a href="lync-server-2013-port-summary-scaled-consolidated-edge-with-hardware-load-balancers.md">Lync Server 2013 中的連接埠摘要 - 調整式合併 Edge (利用硬體負載平衡器)</a>＞。



## 使用者帳戶和資料

在 Lync Server 2013 混合式部署中，任何您想要設為 Lync Online 使用者的帳戶都必須先在內部部署中建立，該使用者帳戶才能在 Active Directory 網域服務 中建立。接著您可以將使用者移動到 商務用 Skype Online，它將移動使用者的連絡人清單。

當您使用 AD FS 與 Dirsync 在 Lync 內部部署與 Lync Online 部署之間同步使用者帳戶時，您需要替組織中位於內部部署與線上 Lync 部署的所有 Lync 使用者同步處理 AD 帳戶，即使使用者並未移至 Lync Online 亦然。如果您並未同步處理所有使用者，組織中的內部部署使用者與線上使用者可能無法如預期般正常通訊。

> [!IMPORTANT]  
> 如果使用 Office 365 線上入口網站建立使用者，那麼該使用者帳戶將不會與內部部署 Active Directory 進行同步處理，且該使用者將不會存在於內部部署 Active Directory。如果您已在 Lync Online 中建立使用者，並且想要設定與內部部署 Lync Server 的混合部署，請參閱<a href="lync-server-2013-moving-users-from-lync-online-to-lync-on-premises.md">將使用者從 Lync Online 移至 Lync Server 2013 的 Lync 內部部署</a>。



規劃混合式部署時，您也必須考量下列使用者相關議題。

  - **使用者連絡人**   Lync Online 使用者的連絡人上限是 250 人。超過該人數上限的連絡人將會在帳戶移至 Lync Online 後從使用者的連絡人清單中移除。

  - **立即訊息和目前狀態**   使用者連絡人清單、群組以及存取控制清單 (ACL) 將根據使用者帳戶進行移轉。

  - **會議資料、會議內容以及排定的會議**   此內容不會根據使用者帳戶進行移轉。使用者帳戶移轉至 Lync Online 後，使用者必須重新排定會議。

## 使用者原則與功能

  - 在 Lync Server 2013 混合式部署中，可針對立即訊息、語音及會議 (內部部署或是線上) 啟用使用者，但兩者不能同時進行。

  - **Lync 用戶端**    有些使用者移動至 Lync Online 時可能會需要新的用戶端版本。若為 Office Communications Server 2007 R2，則使用者移轉至 Lync Online 前必須先移動至 Lync Server 2013 集區。
    
    如需用戶端支援的詳細資訊，請參閱 [Lync Online 用戶端](http://go.microsoft.com/fwlink/p/?linkid=281902)與 [支援的 Lync 用戶端和網路連接埠設定](http://go.microsoft.com/fwlink/p/?linkid=281901)。 。

  - **內部部署原則與設定 (非使用者)**   線上及內部部署原則須個別設定。您無法設定適用於兩者的全域原則。


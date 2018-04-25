---
title: Lync Server 2013 中的公用立即訊息連線的支援
TOCTitle: Lync Server 2013 中的公用立即訊息連線的支援
ms:assetid: 9c6eb500-647b-4ccd-a00e-2b8dd7c44a76
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn458579(v=OCS.15)
ms:contentKeyID: 59602857
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的公用立即訊息連線的支援

 

_**上次修改主題的時間：** 2015-03-09_

## 公用立即訊息連線的支援

本文提供公用 IM 連線 (PIC) 支援的相關資訊。PIC 是 Microsoft Lync 的功能，可讓組織啟用其 Lync 使用者透過 Lync 用戶端與身分識別而與特定公用立即訊息 (IM) 服務的使用者進行連線的功能。

使用者將可享有在效期內與客戶、合作夥伴以及廠商進行連線的優勢。而 IT 人員不僅只需支援單一即時通訊用戶端，同時還能保有 Lync 的控制項、法規遵循以及封存功能。[於 2013 年 5 月公開發佈](http://blogs.technet.com/b/lync/archive/2013/05/23/lync-skype-connectivity-available-today.aspx)的 Lync-Skype 連線功能以 Lync/Office Communications Server (OCS)/Live Communications Server (LCS) 初期建置 PIC 以連線至 MSN/Windows Live、AOL 以及 Yahoo 的做法為基礎。如需 Lync-Skype 連線的詳細資訊，請參閱＜ [Lync-Skype 連線](http://office.microsoft.com/zh-tw/lync/lync-skype-connectivity-fx103789635.aspx)＞。與 Windows Live、AOL 以及 Yahoo 的同盟服務均已邁向尾聲。本頁面說明各服務的狀態。

若要使用 PIC，用戶必須啟動各個公用 IM 服務提供者服務。執行此操作的相關需求與詳細資訊，端視 IM 服務提供者與用戶的基本授權方案而定。

## Windows Live Messenger

Microsoft 已將 Windows Live Messenger 與 Skype 結合。在 2013 年 4 月，Messenger 使用者已完成移轉至 Skype 進行登入的作業。使用與 Messenger 之同盟服務的 Lync 用戶將能持續與其 Messenger 連絡人進行通訊，即使這些連絡人均已更新至 Skype。Lync 系統管理員或 Lync 使用者無需執行任何操作即可持續使用服務，且 Lync 對於這項功能的管理與先前對於 Messenger 的通訊管理相同。

當 Messenger 使用者使用其 Microsoft 帳戶 (即用於 Messenger 的相同認證) 登入 Skype 時，其所有 Messenger 連絡人，包括同盟的 Lync 連絡人，均會一併移至 Skype。這些連絡人可以進行 Skype 與 Lync 之間的目前狀態分享與立即訊息功能。

Lync-Skype 連線功能 (Lync 與 Skype 使用者之間的新增連絡人、目前狀態分享、立即訊息以及音訊撥號功能) 另外亦有提供所有 Lync 用戶使用。

## Yahoo\! 與 AOL Instant Messenger

針對 Lync (與 Office Communications Server) 用戶所提供之 Yahoo\! 及 AOL 的同盟服務均已邁向尾聲。Microsoft 是否能夠提供這些服務將取決於Yahoo\! 與 AOL 所提供的支援，而這些服務所存在的基本合約亦即將結束。對於 Yahoo\! 與 AOL 所提供的服務將持續至 2014 年 6 月。

  - **Yahoo** - 服務將持續至 2014 年 6 月，而用戶仍需取得與 Microsoft Lync 公用 IM 連線使用者訂閱授權 ("PIC USL") 的授權。自 2012 年 9 月 1 日起，PIC USL 無法再以新合約或續約的方式購買。於該日期之前購買授權的用戶將能夠與 Yahoo\! 維持同盟關係直至服務終止日或授權到期，以最早發生者為準。請閱讀 Lync 小組部落格上的[公告](http://blogs.technet.com/b/lync/archive/2012/11/26/lync-and-yahoo-federation-end-of-life.aspx)。倘若用戶所持有之 PIC 授權的合約效期超過 2014 年 6 月 30 日，將依照比例收到 2014 年 6 月 30 日之後所涵蓋之時間範圍的款項。

  - **AOL** - 於 2014 年 6 月 30 日之後，Lync 的 IM 連線 ("PIC") 服務將不再提供。為了避免服務結束時的用戶中斷情形，我們已停止提供新的用戶網域。直至 2014 年 6 月 30 日，用戶無需執行任何操作即可持續享有與 AIM 進行同盟通訊的支援。在該日期之後 (或是對於要佈建額外網域的用戶來說)，AOL 將直接提供替代服務。如需 AOL 之新服務的詳細資訊，請參閱＜[直接建立與 AIM 的同盟](http://aimenterprise.aol.com/pic.php)＞(英文) (會開啟 AOL.com 的新網頁)。

## 公用 IM 提供者摘要

下表提供公用 IM 服務提供者、與 Lync 的同盟功能，以及授權需求的摘要。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>公用 IM 服務提供者</th>
<th>同盟功能</th>
<th>授權需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Skype</p></td>
<td><p>IM、目前狀態、音訊</p></td>
<td><p>Lync Server 用戶端存取授權，Lync Online 方案 1/2/3</p></td>
</tr>
<tr class="even">
<td><p>Windows Live Messenger</p></td>
<td><p>IM、目前狀態、音訊/視訊</p></td>
<td><p>Lync Server 用戶端存取授權 (只要市面仍有 WLM 則會持續支援)</p></td>
</tr>
<tr class="odd">
<td><p>AOL</p></td>
<td><p>IM、目前狀態</p></td>
<td><p>Lync Server 用戶端存取授權；提供既有用戶相關支援至 2014 年 6 月。</p></td>
</tr>
<tr class="even">
<td><p>Yahoo!</p></td>
<td><p>IM、目前狀態</p></td>
<td><p>除了 Lync Server 用戶端存取授權外，另外還需要 Microsoft Lync 公用 IM 連線使用者訂閱授權 (“PIC USL”)。自 2012 年 9 月的價目表起，PIC USL 已不再提供購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至 2014 年 6 月 30 日的服務終止日。</p></td>
</tr>
</tbody>
</table>


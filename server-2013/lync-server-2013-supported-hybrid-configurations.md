---
title: Lync Server 2013：支援的混合式組態
TOCTitle: 支援的混合式組態
ms:assetid: 5d456d6c-ad71-420c-b6d8-4d9cd0324f86
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945633(v=OCS.15)
ms:contentKeyID: 52056138
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 支援的 Lync Server 2013 混合式組態

 

_**上次修改主題的時間：** 2015-03-09_

您可設定 Lync Server 2013 部署，以與 Microsoft Exchange Server 2010 和 Microsoft Exchange Server 2013 和 SharePoint Server 進行內部部署與線上整合。除非特別註明，否則所有的用戶端都支援下表列出的功能。如需用戶端支援的詳細資訊，請參閱 [Lync Server 2013 的用戶端比較表](lync-server-2013-desktop-client-comparison-tables.md)和＜Lync Online 用戶端比較表＞，其位於 [Lync Online 的用戶端](http://go.microsoft.com/fwlink/p/?linkid=281902)。

## 與 Exchange Server 整合

下表列出與 Microsoft Exchange Server 整合時混合部署所支援的功能。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Exchange 內部部署</th>
<th>Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Lync Server 2013 內部部署</strong></p></td>
<td><ul>
<li><p>Outlook 中的 IM/目前狀態</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-im-and-presence.md">Lync Server 2013 中的 IM 和目前狀態</a>＞</p></li>
<li><p>透過 Outlook 排程及加入線上會議</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-integrating-with-microsoft-exchange-server-2013.md">整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013</a>＞</p></li>
<li><p>Outlook Web App 中的 IM/目前狀態</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-lync-server-in-a-cross-premises-environment.md">在跨單位環境中設定 Microsoft Lync Server 2013</a>＞</p></li>
<li><p>透過 Outlook Web App 排程及加入線上會議</p></li>
<li><p>行動用戶端中的 IM/目前狀態</p></li>
<li><p>在行動用戶端中加入線上會議</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-deploying-mobility.md">在 Lync Server 2013 中部署行動性</a>＞</p></li>
<li><p>根據 Outlook 行事曆的空閒/忙碌資訊發佈狀態</p></li>
<li><p>連絡人清單 (透過整合連絡人存放區)</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-lync-server-to-use-the-unified-contact-store.md">設定 Microsoft Lync Server 2013 使用整合連絡人存放區</a>＞</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>需要有 Exchange 2013。<br />
需要 Lync 2013 桌面用戶端。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>Lync 2013 用戶端和 Lync Web App 中的高解析度連絡人相片。</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-the-use-of-high-resolution-photos.md">設定在 Microsoft Lync Server 2013 中使用高解析度相片</a>＞</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>需要有 Exchange 2013。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>會議委派</p>
<p>只有當雙方使用者在線上位於同一樹系或是同時位於內部部署時才支援。</p></li>
<li><p>未接交談記錄和通話記錄會寫入使用者的 Exchange 信箱。</p></li>
<li><p>Exchange 中的封存內容 (IM 和會議)</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-deployment-checklist-for-archiving.md">Lync Server 2013 中封存的部署檢查單</a>＞</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>需要有 Exchange 2013。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>搜尋封存的內容</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>需要有 Exchange 2013。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>語音信箱</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md">部署內部部署的 Exchange UM，以提供 Lync Server 2013 語音信箱</a>＞</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 中的 IM/目前狀態</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md">設定內部部署 Lync Server 2013 與 Exchange Online 整合</a>＞</p></li>
<li><p>透過 Outlook 排程及加入線上會議</p></li>
<li><p>OWA 中的 IM/目前狀態</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md">設定內部部署 Lync Server 2013 與 Exchange Online 整合</a>＞</p></li>
<li><p>從 Outlook Web App 排程及加入線上會議</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md">設定內部部署 Lync Server 2013 與 Exchange Online 整合</a>＞</p></li>
<li><p>行動用戶端中的 IM/目前狀態</p></li>
<li><p>在行動用戶端中加入線上會議</p></li>
<li><p>根據 Outlook 行事曆的空閒/忙碌資訊發佈狀態</p></li>
<li><p>連絡人清單 (透過整合連絡人存放區)。如需詳細資訊，請參閱＜ <a href="lync-server-2013-configuring-lync-server-to-use-the-unified-contact-store.md">設定 Microsoft Lync Server 2013 使用整合連絡人存放區</a>＞</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅限 Lync Server 2013。需要 Lync 2013 桌面用戶端。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>Lync 2013 用戶端和 Lync Web App 中的高解析度連絡人相片。</p>
<p>如需詳細資訊，請參閱 <a href="lync-server-2013-configuring-the-use-of-high-resolution-photos.md">設定在 Microsoft Lync Server 2013 中使用高解析度相片</a>。</p></li>
<li><p>會議委派</p>
<p>只有當雙方使用者在線上位於同一樹系或是同時位於內部部署時才支援。</p></li>
<li><p>未接交談記錄和通話記錄會寫入使用者的 Exchange 信箱。</p></li>
<li><p>Exchange 中的封存內容 (IM 和會議)。</p>
<p>如需詳細資訊，請參閱＜<a href="lync-server-2013-deployment-checklist-for-archiving.md">Lync Server 2013 中封存的部署檢查單</a>＞</p></li>
<li><p>搜尋封存的內容。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=285448">設定 Exchange for SharePoint eDiscovery Center</a></p></li>
<li><p>語音信箱。如需詳細資訊，請參閱＜ <a href="lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md">在主控 Exchange UM 上提供 Lync Server 2013 使用者語音信箱</a>＞</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Lync Online</strong></p></td>
<td><ul>
<li><p>Outlook 中的 IM 和目前狀態</p></li>
<li><p>透過 Outlook 排程及加入線上會議</p></li>
<li><p>行動用戶端中的 IM/目前狀態</p></li>
<li><p>未接交談記錄和通話記錄會寫入使用者的 Exchange 信箱。</p></li>
<li><p>Lync 2013 用戶端中的高解析度連絡人相片。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>需要有 Microsoft Exchange Server 2013。這在使用者位於 商務用 Skype Online 的 Lync Web App 中不受支援。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>在行動用戶端中加入線上會議</p></li>
<li><p>根據 Outlook 行事曆的空閒/忙碌資訊發佈狀態</p></li>
<li><p>會議委派</p>
<p>只有當雙方使用者在線上位於同一樹系或是同時位於內部部署時才支援。</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 中的 IM/目前狀態</p></li>
<li><p>透過 Outlook 排程及加入線上會議</p></li>
<li><p>Outlook Web App 中的 IM/目前狀態</p></li>
<li><p>從 Outlook Web App 排程及加入線上會議</p></li>
<li><p>行動用戶端中的 IM/目前狀態</p></li>
<li><p>在行動用戶端中加入線上會議</p></li>
<li><p>根據 Outlook 行事曆的空閒/忙碌資訊發佈狀態</p></li>
<li><p>未接交談記錄和通話記錄會寫入使用者的 Exchange 信箱。</p></li>
<li><p>連絡人清單 (透過整合連絡人存放區)</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>需要 Lync Server 2013 用戶端</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>Lync 2013 用戶端和 Lync Web App 中的高解析度連絡人相片。</p></li>
<li><p>會議委派</p>
<p>只有當雙方使用者在線上位於同一樹系或是同時位於內部部署時才支援。</p></li>
<li><p>Exchange 中的封存內容 (IM 和會議)</p></li>
<li><p>搜尋封存的內容</p></li>
<li><p>語音信箱</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 與 SharePoint 整合

下表列出與 SharePoint 整合時 Lync Server 2013 混合部署所支援的功能。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>SharePoint 內部部署</th>
<th>SharePoint Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Lync Server 2013 內部部署</strong></p></td>
<td><ul>
<li><p>技能搜尋</p></li>
<li><p>SharePoint 中的目前狀態</p></li>
</ul></td>
<td><ul>
<li><p>SharePoint 中的目前狀態</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Lync Online</strong></p></td>
<td><ul>
<li><p>SharePoint 中的目前狀態</p></li>
</ul></td>
<td><ul>
<li><p>SharePoint 中的目前狀態</p></li>
</ul></td>
</tr>
</tbody>
</table>


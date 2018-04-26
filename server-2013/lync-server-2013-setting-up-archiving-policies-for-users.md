---
title: 設定使用者的封存原則
TOCTitle: 設定使用者的封存原則
ms:assetid: 1bbb45df-0590-4c66-9d65-d25526f57790
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204722(v=OCS.15)
ms:contentKeyID: 49290253
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定使用者的封存原則

 

_**上次修改主題的時間：** 2012-10-09_

您可建立並設定使用者的封存原則，然後將其套用至特定使用者或使用者群組，以啟用或停用特定使用者的封存。使用者原則會覆寫任何全域原則或網站原則。僅有在您未使用 Microsoft Exchange 整合，或者，您有使用 Microsoft Exchange 整合，但擁有部分不位於 Exchange 2013 且其信箱為就地保留狀態的使用者時，才能套用封存原則。

如需封存原則運作方式的詳細資訊，包括全域、網站與使用者原則的階層，請參閱規劃或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您啟用部署的 Microsoft Exchange 整合，Exchange 就地保留原則可控制是否要針對位於 Exchange 2013 且其信箱為就地保留狀態的使用者啟用封存。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>＞。<br />
您應先在封存組態中指定所有適當的選項後，再啟用封存原則中內部或外部通訊的封存。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [設定使用者原則以在 Lync Server 中封存](lync-server-2013-setting-up-user-policies-for-archiving-in-lync-server.md)

  - [設定使用 Exchange Server 整合時的封存原則](lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md)


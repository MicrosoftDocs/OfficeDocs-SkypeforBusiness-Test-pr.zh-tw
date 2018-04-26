---
title: 設定使用者原則以在 Lync Server 中封存
TOCTitle: 設定使用者原則以在 Lync Server 中封存
ms:assetid: 22d6cc76-6b5c-4a8c-bb8a-7996450ec085
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204742(v=OCS.15)
ms:contentKeyID: 49290340
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定使用者原則以在 Lync Server 中封存

 

_**上次修改主題的時間：** 2012-10-10_

若要針對位於 Lync Server 2013 的特定使用者啟用或停用封存，您必須建立並設定一或多個使用者原則，然後將適當的原則套用至特定的使用者或使用者群組。使用者原則會覆寫網站和全域原則，但僅針對位於 Lync Server 2013 的使用者而言。

使用者一律是位於 Lync Server。若啟用了 Microsoft Exchange 整合，當使用者的信箱是位於 Microsoft Exchange Server 2013 時，即不需要在 Lync Server 中管理這些使用者的封存原則，而是由 Exchange 就地保留來管理這些具備封存功能的使用者。

如需封存原則運作方式的詳細資訊，包括全域、網站與使用者原則的階層，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您啟用部署的 Microsoft Exchange 整合，Exchange 就地保留原則可控制是否要針對位於 Exchange 2013 使用者啟用封存。若要針對這些使用者啟用封存，則其信箱必須為就地保留狀態。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>＞。<br />
您應先在封存設定中指定好所有適當的選項，然後再啟用封存。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 中建立和設定封存的使用者原則](lync-server-2013-creating-and-configuring-user-policies-for-archiving-in-lync-server.md)

  - [將 Lync Server 封存原則套用至使用者](lync-server-2013-applying-a-lync-server-archiving-policy-to-a-user.md)


---
title: 設定使用 Exchange Server 整合時的封存原則
TOCTitle: 設定使用 Exchange Server 整合時的封存原則
ms:assetid: 8b9b2bad-a4b3-42e1-85a7-04022e9442ad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205063(v=OCS.15)
ms:contentKeyID: 49291604
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定使用 Exchange Server 整合時的封存原則

 

_**上次修改主題的時間：** 2012-10-09_

如果位於 Exchange 2013 的使用者擁有設為 \[就地保留\] 的信箱，Exchange 就地保留原則會控制這些使用者的封存。如果您針對部署使用 Microsoft Exchange 整合，Exchange 2013 原則會針對位於 Exchange 2013 的使用者覆寫 Lync Server 封存原則。如需關於設定 Exchange 封存原則的資訊，請參閱 Exchange 2013 文件。如需關於針對位於 Lync Server 2013 的使用者設定使用者原則的詳細資訊，請參閱部署文件中的[設定使用者原則以在 Lync Server 中封存](lync-server-2013-setting-up-user-policies-for-archiving-in-lync-server.md)。如需關於原則如何運作的詳細資訊，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在相同樹系中部署 Exchange 2013 和 Lync Server 2013，您的 Exchange 2013 就地保留原則會控制封存。如果您在不同樹系中部署 Exchange 2013 和 Lync Server 2013，請參閱＜<a href="lync-server-2013-deployment-checklist-for-archiving.md">Lync Server 2013 中封存的部署檢查單</a>＞中的＜在不同樹系中部署 Lync Server 和 Microsoft Exchange＞。</td>
</tr>
</tbody>
</table>


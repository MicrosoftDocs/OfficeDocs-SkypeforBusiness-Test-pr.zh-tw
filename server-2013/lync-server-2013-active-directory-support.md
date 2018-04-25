---
title: Lync Server 2013 Active Directory 支援
TOCTitle: Active Directory 支援
ms:assetid: 28ed9ac4-586d-4803-ad45-99c4fa793f54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425756(v=OCS.15)
ms:contentKeyID: 49290397
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Active Directory 支援

 

_**上次修改主題的時間：** 2012-12-04_

以下是 Lync Server 2013 支援的 Active Directory 網域服務 內部部署拓撲：

  - 具單一網域的單一樹系

  - 具單一樹狀結構和多個網域的單一樹系

  - 具多重樹狀結構和斷續命名空間的單一樹系

  - 中央樹系拓撲中的多重樹系

  - 資源樹系拓撲中的多重樹系

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 不支援單一標籤網域。例如，單一標籤根網域名稱為 <strong>contoso.local</strong> 的樹系是受支援的，名為 <strong>local</strong> 的根網域則不受支援。如需詳細資訊，請參閱 Microsoft 知識庫文章 300684＜為具有單一標籤 DNS 名稱之網域設定 Windows 的相關資訊＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=143752%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=143752&amp;clcid=0x404</a>。</td>
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
<td>Lync Server 2013 不支援重新命名的網域。如果您需要重新命名已部署 Lync Server 的網域，您必須先解除安裝 Lync Server，然後重新命名網域，接著重新安裝 Lync Server。</td>
</tr>
</tbody>
</table>


如需內部部署支援的拓撲與需求的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中 Active Directory 網域服務需求、支援和拓撲](lync-server-2013-active-directory-domain-services-requirements-support-and-topologies.md)＞。


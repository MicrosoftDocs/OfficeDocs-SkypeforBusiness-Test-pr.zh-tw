---
title: Lync Server 2013：舊部署支援的用戶端
TOCTitle: 舊部署支援的用戶端
ms:assetid: 69d427f8-57a5-4244-b2ed-f2eb7600285e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398499(v=OCS.15)
ms:contentKeyID: 49291201
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中舊部署支援的用戶端

 

_**上次修改主題的時間：** 2015-03-09_

在共存的案例中， Lync Server 2013 用戶端可與舊版 Lync Server 和 Office Communications Server 的用戶端互動。與舊版不同的是， Lync Server 2010 可支援新的 Lync 2013 用戶端。這樣可讓從 Lync Server 2010 進行升級的組織部署與 Lync Server 升級無關的新用戶端。

## 支援的伺服器和用戶端組合

下表顯示支援的用戶端版本和伺服器版本組合。 Lync Server 2013 支援兩種舊版用戶端，而 Lync Server 2010 支援新的 Lync 2013 用戶端。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>Lync Server 2013</th>
<th>Lync Server 2010</th>
<th>Office Communications Server 2007 R2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync Web App 2013</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 Attendant</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 群組聊天</p></td>
<td><p>不適用</p></td>
<td><p>支援1</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>Lync Web App 2010</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 Attendee</p></td>
<td><p>不支援2</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>可互通3</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Communications Server 2007 R2 Attendant</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="even">
<td><p>Office Communicator 2007</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="odd">
<td><p>Office Live Meeting 2007</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
</tbody>
</table>


1Microsoft Lync Server 2010 可利用群組聊天伺服器提供群組聊天功能，此為 Lync Server 2010 適用的協力廠商信任應用程式。 Lync 2013 用戶端與 Lync Server 2010 群組聊天不相容。

2Lync Web App 2013 現在提供完整的會議參與經驗，包括電腦音訊與視訊，且被視為可取代 Lync 2010 Attendee。

3Office Communicator 2007 R2 的目前狀態和 IM 功能可與 Lync Server 2013 相容，但會議功能則不相容。從 Office Communications Server 2007 R2 移轉的期間， Office Communicator 2007 R2 適用於目前狀態和 IM 互通性，但使用者應該使用 Lync Web App 2013 加入 Lync Server 2013 會議。

> [!NOTE]  
> 如需 Lync Server 2013 用戶端與 Lync Server 和 Office Communications Server 舊版用戶端共存以及進行互動之能力的詳細資訊，請參閱規劃文件中的 <a href="lync-server-2013-client-interoperability-in-lync-2013.md">Lync 2013 中的用戶端互通性</a>。



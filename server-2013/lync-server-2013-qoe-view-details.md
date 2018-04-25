---
title: Lync Server 2013 中的 QoE 檢視詳細資料
TOCTitle: Lync Server 2013 中的 QoE 檢視詳細資料
ms:assetid: 6a658318-a317-4546-a44c-a9c473d8e86a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688081(v=OCS.15)
ms:contentKeyID: 49890103
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 QoE 檢視詳細資料

 

_**上次修改主題的時間：** 2015-03-09_

檢視涵蓋從 QoE SQL 資料庫傳回資料時最常見的案例。此為建議的檢視，可用來建立自訂報告，而非直接存取資料庫資料表；那是因為檢視較可能維持與日後版本的回溯相容性。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>檢視名稱</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-audiostreamdetail-view.md">AudioStreamDetail 檢視</a></p></td>
<td><p>儲存資料庫中每個音訊資料流的資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-medialine-view.md">MediaLine 檢視</a></p></td>
<td><p>儲存資料庫中每個媒體行的資訊。一個音訊工作階段通常包含一個音訊媒體行。一個音訊和視訊 (A/V) 工作階段通常包含一個音訊媒體行和一個視訊媒體行；不過，如果使用會議裝置或使用圖庫檢視，則工作階段可能包含兩個媒體行。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-networkconfigurationsettings-view.md">NetworkConfigurationSettings 檢視</a></p></td>
<td><p>儲存網路設定的資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-session-view.md">Session 檢視</a></p></td>
<td><p>儲存在資料庫中擁有記錄之工作階段的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-useragent-view.md">UserAgent 檢視</a></p></td>
<td><p>儲存使用者代理程式的資訊，這些使用者代理程式與在資料庫中擁有記錄的工作階段相關。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-videostreamdetail-view.md">VideoStreamDetail 檢視</a></p></td>
<td><p>儲存在資料庫中每個視訊資料流的資訊。</p></td>
</tr>
</tbody>
</table>


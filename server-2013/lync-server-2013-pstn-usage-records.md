---
title: Lync Server 2013：PSTN 使用方式記錄
TOCTitle: PSTN 使用方式記錄
ms:assetid: b5f624aa-abe8-455b-a8e3-c228be230463
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412878(v=OCS.15)
ms:contentKeyID: 49292074
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 PSTN 使用方式記錄

 

_**上次修改主題的時間：** 2015-03-09_

PSTN 使用方式記錄的規劃主要是列出目前組織中有效的所有通話權限 (上至執行長，下至臨時人員、顧問和約聘員工)。這個程序也會提供重新檢查現有通話權限並進行修改的機會。您只能針對套用到預期 Enterprise Voice 使用者的通話權限建立 PSTN 使用方式記錄，但是比較理想的長期解決方案會是針對所有通話權限建立 PSTN 使用方式記錄，不論是否有一些通話權限目前可能不會套用到要啟用 Enterprise Voice 的使用者群組。如果通話權限變更，或是加入了具有不同通話權限的新使用者，您便已擁有建立好的 PSTN 使用方式記錄可因應新需求。

下表說明傳統的 PSTN 使用方式。

### PSTN 使用方式記錄

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>電話屬性</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local</p></td>
<td><p>本地電話</p></td>
</tr>
<tr class="even">
<td><p>Long-Distance</p></td>
<td><p>長途電話</p></td>
</tr>
<tr class="odd">
<td><p>International</p></td>
<td><p>國際電話</p></td>
</tr>
<tr class="even">
<td><p>Delhi</p></td>
<td><p>Delhi 全職員工</p></td>
</tr>
<tr class="odd">
<td><p>Redmond</p></td>
<td><p>Redmond 全職員工</p></td>
</tr>
<tr class="even">
<td><p>RedmondTemps</p></td>
<td><p>Redmond 臨時員工</p></td>
</tr>
<tr class="odd">
<td><p>Zurich</p></td>
<td><p>Zurich 全職員工</p></td>
</tr>
</tbody>
</table>


PSTN 使用方式記錄本身並不會執行任何動作。如果要讓 PSTN 使用方式記錄運作，您必須將其與下列項目產生關聯：

  - 指派給使用者的語音原則。

  - 指派給電話號碼的路由。

如需語音原則和路由的詳細資訊，請參閱＜ [Lync Server 2013 中的語音原則](lync-server-2013-voice-policies.md)＞和＜ [Lync Server 2013 中的語音路由](lync-server-2013-voice-routes.md)＞。如需如何建立和設定這兩者的詳細資訊，請參閱＜ [Lync Server 2013 中設定撥出電話的語音路由](lync-server-2013-configuring-voice-routes-for-outbound-calls.md)＞。


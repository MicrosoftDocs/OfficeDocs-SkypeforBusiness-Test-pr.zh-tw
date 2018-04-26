---
title: Lync Server 2013：VideoClientEvent 表格
TOCTitle: VideoClientEvent 表格
ms:assetid: e8ab963b-fe1d-45b3-b9bd-66a5f44c1629
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399039(v=OCS.15)
ms:contentKeyID: 49292672
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 VideoClientEvent 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄都包含視訊通話中某端點的用戶端事件。一通電話通常會有兩筆記錄，一筆為發話者，另一筆為受話者。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>參考來源： <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>參考來源： <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要</p></td>
<td><p>參考來源： <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>FromCaller</strong></p></td>
<td><p>bit</p></td>
<td><p>主要</p></td>
<td><p>0：受話者的資料</p>
<p>1：發話者的資料</p></td>
</tr>
<tr class="odd">
<td><p><strong>NetworkBandwidthLowEventRatio</strong></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 LowBandwidth 活動的工作階段百分比。可用的頻寬不足，無法提供可接受程度的語音經驗。</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkReceiveQualityEventRatio</strong></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 ReceiveSendQuality 事件的工作階段百分比。</p>
<p>出現抖動或封包遺失在網路品質來說相當嚴重，且會影響所接收的音訊品質。</p></td>
</tr>
</tbody>
</table>


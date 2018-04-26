---
title: AppSharingMetricsThreshold 表
TOCTitle: AppSharingMetricsThreshold 表
ms:assetid: 782cfab9-01a6-4843-aea1-28f47b0b51f7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205018(v=OCS.15)
ms:contentKeyID: 49291380
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# AppSharingMetricsThreshold 表

 

_**上次修改主題的時間：** 2015-03-09_

AppSharingMetricsThreshold 表格包含可與應用程式共用搭配使用之經驗品質計量適用的最佳值與可接受值。這些閾值可用來判斷應用程式共用經驗是否應該分類為不良。

此表格是在 Microsoft Lync Server 2013 中所引進。


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
<td><p><strong>通話類型</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>撥打的通話類型。</p></td>
</tr>
<tr class="even">
<td><p><strong>AppliedBandwidthLimitOptimal</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>適用於應用程式共用的最佳頻寬限制。預設值為 1000000。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AppliedBandwidthLimitAcceptable</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>適用於應用程式共用且可接受的頻寬限制。預設值為 500000。</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentTotalOptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>對於可用於分類應用程式共用品質之「已毀損」並排顯示的最佳百分比率。此值是來自未送達檢視者之共用者的內容百分比。當共用者從圖表來源中捨棄並排顯示或 ASMCU 並排顯示個別捨棄來自共用者的並排顯示時，內容可能會被捨棄 (或毀損)。預設值為 11 個百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SpoiledTilePercentTotalAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>對於可用於分類應用程式共用品質之「已毀損」並排顯示的可接受百分比率。此值是來自未送達檢視者之共用者的內容百分比。當共用者從圖表來源中捨棄並排顯示或 ASMCU 並排顯示個別捨棄來自共用者的並排顯示時，內容可能會被捨棄 (或毀損)。預設值為 36 個百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalOptimal</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 中未使用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>JitterInterArrivalAcceptable</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 中未使用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstDensityOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 中未使用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayBurstDensityAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 中未使用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyBurstDensityOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 中未使用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyBurstDensityAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 中未使用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayAverageOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>應用程式共用中所含之兩個媒體端點間適用於相對單向延遲的最佳值。此為單一躍點延遲措施。預設值為 1.0 秒。</p>
<p>此欄是在 Microsoft Lync Server 2013 中所引進。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayAverageAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>應用程式共用中所含之兩個媒體端點間適用於相對單向延遲的最佳值。此為單一躍點延遲措施。預設值為 1.75 秒。</p>
<p>此欄是在 Microsoft Lync Server 2013 中所引進。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyAverageOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>在檢視工作階段期間，AS 會議伺服器中平均 RDP 並排顯示處理延遲的最佳值。此計量並未涵蓋網路延遲。</p>
<p>高平均會反映檢視經驗中較長的延遲。負載過重的會議伺服器可能會發生較高的平均延遲。預設值為 200ms。</p>
<p>此欄是在 Microsoft Lync Server 2013 中所引進。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyAverageAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>在檢視工作階段期間，AS 會議伺服器中平均 RDP 並排顯示處理延遲的可接受值。此計量並未涵蓋網路延遲。</p>
<p>高平均會反映檢視經驗中較長的延遲。負載過重的會議伺服器可能會發生較高的平均延遲。預設值為 200ms。</p>
<p>此欄是在 Microsoft Lync Server 2013 中所引進。</p></td>
</tr>
</tbody>
</table>


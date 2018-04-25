---
title: Lync Server 2013：AudioStream 表格
TOCTitle: AudioStream 表格
ms:assetid: 49ccbbc3-2f73-45fc-80a6-e612535cbc10
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425961(v=OCS.15)
ms:contentKeyID: 49290821
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 AudioStream 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表一個音訊資料流。一個音訊媒體行通常包含兩個音訊資料流。


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
<td><p><strong>StreamID</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>媒體行中的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>JitterInterArrival</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>即時控制通訊協定 (RTCP) 統計資料的平均網路抖動。</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>通話期間的最大網路抖動。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketLossRate</strong></p></td>
<td><p>decimal(5.4)</p></td>
<td><p> </p></td>
<td><p>通話期間的平均封包遺失率</p></td>
</tr>
<tr class="even">
<td><p><strong>PacketLossRateMax</strong></p></td>
<td><p>decimal(5.4)</p></td>
<td><p> </p></td>
<td><p>通話期間監測所得的最大封包遺失率</p></td>
</tr>
<tr class="odd">
<td><p><strong>BurstDensity</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p> </p></td>
<td><p>通話期間封包遺失量激增時的封包遺失平均密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>BurstDuration</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>通話期間封包遺失量激增期的封包遺失平均持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BurstGapDensity</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p> </p></td>
<td><p>封包遺失量激增期之間的間歇期封包遺失平均密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>BurstGapDuration</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>封包遺失量激增期之間的間歇期平均持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketUtilization</strong></p></td>
<td><p>Int</p></td>
<td><p> </p></td>
<td><p>音訊資料流的封包計數。</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEst</strong></p></td>
<td><p>Int</p></td>
<td><p> </p></td>
<td><p>音訊資料流的頻寬預估值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DegradationAvg</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>整個通話的網路 MOS 降低。範圍為 0.0 到 5.0。此計量顯示因為抖動及封包遺失而導致的網路 MOS 降低量。就可接受的品質而言，其應低於 0.5。</p></td>
</tr>
<tr class="even">
<td><p><strong>DegradationMax</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>通話期間的最大網路 MOS 降低。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DegradationJitterAvg</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>抖動所導致的網路 MOS 降低。</p></td>
</tr>
<tr class="even">
<td><p><strong>DegradationPacketLossAvg</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>封包遺失所導致的網路 MOS 降低。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioPayloadDescription</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話的音訊轉碼器，參考來源：PayloadDescription 表格。</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioSampleRate</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>音訊資料流的取樣率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RoundTrip</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>RTCP 統計資料中的來回時間。就可接受的品質而言，此應低於 100 毫秒。</p></td>
</tr>
<tr class="even">
<td><p><strong>RoundTripMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>音訊資料流的最大來回時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OverallAvgNetworkMOS</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>通話的平均寬頻網路 MOS。此計量取決於封包遺失、抖動及所使用的轉碼器。範圍為 [1.0 到 5.0]。</p></td>
</tr>
<tr class="even">
<td><p><strong>OverallMinNetworkMOS</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>通話的最小寬頻網路 MOS。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendListenMOS</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>所傳送之音訊的平均預測寬頻傾聽 MOS 分數，包括語音層級、雜訊層級和擷取裝置特性。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendListenMOSMin</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>通話的最小 SendListenMOS。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvListenMOS</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>從網路接收之音訊的平均預測寬頻傾聽 MOS 分數，包括語音層級、雜訊層級、轉碼器、網路狀況和擷取裝置特性。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvListenMOSMin</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>通話的最小 RecvListenMOS。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioFECUsed</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>指出是否將音訊 FEC 用於通話的標幟。</p></td>
</tr>
<tr class="even">
<td><p><strong>RatioConcealedSamplesAvg</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p></p></td>
<td><p>音訊修復所產生之隱藏樣本與一般樣本的平均比率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RatioStretchedSamplesAvg</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p></p></td>
<td><p>音訊修復所產生之延伸樣本與一般樣本的平均比率。</p></td>
</tr>
<tr class="even">
<td><p><strong>RatioCompressedSamplesAvg</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p></p></td>
<td><p>音訊修復所產生之壓縮樣本與一般樣本的平均比率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inbound</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>接收端所收到的資料流資料。</p></td>
</tr>
<tr class="even">
<td><p><strong>Outbound</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>傳送端所收到的資料流資料。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SenderIsCallerPAI</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 表示資料流是從發話者流向受話者。</p>
<p>0 表示資料流是從被呼叫者流向呼叫者。</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalSD</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>抖動到達時間的標準差。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConcealRatioMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>修復隱藏封包的最大比率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConcealRatioSD</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>修復隱藏封包率的標準差。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HealerPacketDropRatio</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>與收到封包總數相比的修復捨棄封包率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>HealerFECPacketUsedRatio</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>與收到封包總數相比的正向錯誤修正封包使用率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCompressedSamples</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>修復壓縮的音訊封包上限。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>LossCongestionPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>表示通話處於遺漏壅塞狀態時的時間百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelayCongestionPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>表示因網路封包延遲抵達造成壅塞期間的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentionDetectedPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>表示通話爭用網路資源時的時間百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEstMin</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估最小值。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEstMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估最大值。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEstStdDev</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估標準差。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEstAvge</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估平均值。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向延遲的總數量。相對單向延遲是測量用戶端與伺服器之間的延遲時間。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向延遲的平均數量。相對單向延遲是測量用戶端與伺服器之間的延遲時間。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向延遲的最大數量。相對單向延遲是測量用戶端與伺服器之間的延遲時間。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>單向高載發生總次數。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。此計量測量用戶端與伺服器之間的資料流動。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向高載總密度。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。此計量測量用戶端與伺服器之間的資料流動。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向高載總持續時間。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。此計量測量用戶端與伺服器之間的資料流動。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>單向缺口發生總次數。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。缺口指的是這些高載之間的延遲。此計量測量用戶端與伺服器之間的資料流動。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向缺口總密度。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。缺口指的是這些高載之間的延遲。此計量測量用戶端與伺服器之間的資料流動。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向缺口總持續時間。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。缺口指的是這些高載之間的延遲。此計量測量用戶端與伺服器之間的資料流動。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>DecodeStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>解碼為立體聲的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AecRenderStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>由迴音效果取消器轉換為立體聲的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioPostFECPLR</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>已套用正向錯誤修正後的封包遺失率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EncodeStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>編碼為立體聲的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>AecCaptureStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>由迴音效果取消器擷取為立體聲的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
</tbody>
</table>


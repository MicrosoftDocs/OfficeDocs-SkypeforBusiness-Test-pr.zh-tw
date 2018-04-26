---
title: Lync Server 2013：VideoStream 表格
TOCTitle: VideoStream 表格
ms:assetid: 4275ede7-5467-4a97-b8c8-a4b00917bf32
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425928(v=OCS.15)
ms:contentKeyID: 49290736
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 VideoStream 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表一個視訊資料流。一個視訊媒體行通常包含兩個視訊資料流。


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
<td><p><strong>VideoPayloadDescription</strong></p></td>
<td><p>smallint</p></td>
<td><p>外部、主要</p></td>
<td><p>承載描述。如需詳細資訊，請參閱 <a href="lync-server-2013-payloaddescription-table.md">Lync Server 2013 中的 PayloadDescription 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrival</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>即時控制通訊協定 (RTCP) 統計資料的平均網路抖動。</p></td>
</tr>
<tr class="odd">
<td><p><strong>JitterInterArrivalMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>視訊工作階段期間的最大網路抖動。</p></td>
</tr>
<tr class="even">
<td><p><strong>RoundTrip</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>RTCP 統計資料中的來回時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RoundTripMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>視訊資料流的最大來回時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>PacketLossRate</strong></p></td>
<td><p>decimal(5.4)</p></td>
<td><p> </p></td>
<td><p>通話期間的平均封包遺失率</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketLossRateMax</strong></p></td>
<td><p>decimal(5.4)</p></td>
<td><p> </p></td>
<td><p>通話期間監測所得的最大封包遺失率</p></td>
</tr>
<tr class="even">
<td><p><strong>PacketUtilization</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>視訊資料流的封包計數 (即時傳輸控制通訊協定 (RTP))。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEst</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>視訊資料流的頻寬預估值。</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoResolution</strong></p></td>
<td><p>char(9)</p></td>
<td><p> </p></td>
<td><p>視訊的解析度 (像素寬度乘以像素高度)。報告成字串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoBitRateAvg</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>視訊資料流的平均位元速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>InboundVideoFrameRateAvg</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p> </p></td>
<td><p>收到的視訊播放速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutboundVideoFrameRateAvg</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p> </p></td>
<td><p>傳送的視訊播放速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoBitRateMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>視訊工作階段期間的最大視訊位元速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoFrameLossRate</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p> </p></td>
<td><p>遺失之視訊框總數的百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoFEC</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>無法使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoLocalFrameLossPercentageAvg</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p></p></td>
<td><p>遺失之視訊框總數的百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>CIFQualityRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>Common Interchange Format (CIF) 解析度之通話的百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>VGAQualityRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>VGA 解析度之通話的百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>HD720QualityRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>HD720 解析度之通話的百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NoneDropRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>未捨棄框架的通話時間百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>BDropRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>捨棄 B 框架的通話時間百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPDropRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>捨棄 BP 框架的通話時間百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>BPSPDropRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>捨棄 BPSP 框架的通話時間百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPSPIDropRatio</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>捨棄 BPSPI 框架的通話時間百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>Inbound</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>接收端所收到的資料流資料。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Outbound</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>傳送端所收到的資料流資料。</p></td>
</tr>
<tr class="even">
<td><p><strong>SenderIsCallerPAI</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 表示資料流是從呼叫者流向被呼叫者。</p>
<p>0 表示資料流是從被呼叫者流向呼叫者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LossCongestionPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>表示通話處於遺漏壅塞狀態時的時間百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>DelayCongestionPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>表示因網路封包延遲抵達造成壅塞期間的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ContentionDetectedPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>表示通話爭用網路資源時的時間百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEstMin</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估最小值。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEstMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估最大值。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEstStdDev</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估標準差。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEstAvge</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>通話期間測得的頻寬預估平均值。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>LowBandwidthForMultiview</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>因網路連線無法支援 multiview 視訊所判定的端點所在之通話百分比。</p>
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
<td><p>int</p></td>
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
<td><p><strong>VideoPacketLossRate</strong></p></td>
<td><p>decimal(9.4)</p></td>
<td><p></p></td>
<td><p>視訊封包遺失率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoAllocateBWAvg</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>分配給視訊的頻寬平均量。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendCodecTypes</strong></p></td>
<td><p>smallint</p></td>
<td><p>外部</p></td>
<td><p>傳送者使用的視訊轉碼器類型。如需詳細資訊，請參閱 <a href="lync-server-2013-codecdescription-table.md">CodecDescription 表</a>。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendResolutionWidth</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>傳送者使用的解析度寬度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendResolutionHeight</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>傳送者使用的解析度高度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendFrameRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者使用的平均視訊播放速率傳輸。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendBitRateMaximum</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>傳送者的最大位元速率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendBitRateAverage</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>傳送者的平均位元速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendVideoStreamsMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>傳送者使用的視訊資料流最大數量。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvCodecTypes</strong></p></td>
<td><p>smallint</p></td>
<td><p>外部</p></td>
<td><p>接收者使用的視訊編碼。如需詳細資訊，請參閱 <a href="lync-server-2013-codecdescription-table.md">CodecDescription 表</a>。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvResolutionWidth</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者使用的解析度寬度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvResolutionHeight</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者使用的解析度高度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvFrameRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>接收者使用的平均視訊播放速率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvBitRateMaximum</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者的最大位元速率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvBitRateAverage</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者的平均位元速率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvVideoStreamsMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者的最大視訊資料流。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvVideoStreamsMin</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者的最小視訊資料流。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvVideoStreamsMode</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>接收者的視訊模式 (例如圖庫或單一資料流)。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoPostFECPLR</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>已套用正向錯誤修正後的封包遺失率。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DynamicCapabilityPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>使用動態功能旗幟的時間百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResolutionMin</strong></p></td>
<td><p>char(9)</p></td>
<td><p></p></td>
<td><p>通話期間測得的最小解析度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LowBitRateCallPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>低位元速率臨界值 (每秒 70 Kbps) 以下的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>LowFrameRateCallPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>低播放速率臨界值 (每秒 7.5 個畫面數，輸入) 以下的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LowResolutionCallPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以最低解析度進行的通話百分比。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>DurationSeconds</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>通話長度 (秒)。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsAggregatedData</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>表示資料是否已從多個通話中彙整完畢。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
</tbody>
</table>


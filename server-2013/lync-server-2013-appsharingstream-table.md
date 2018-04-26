---
title: AppSharingStream 表
TOCTitle: AppSharingStream 表
ms:assetid: 391490cb-d7b8-44ca-b4d1-429600da909c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204808(v=OCS.15)
ms:contentKeyID: 49290617
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# AppSharingStream 表

 

_**上次修改主題的時間：** 2015-03-09_

AppSharingStream 表格包含的「經驗品質」計量是針對用於應用程式共用的網路資料流。此表格推出於 Microsoft Lync Server 2013。


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
<td><p>日期時間</p></td>
<td><p>主要，外部</p></td>
<td><p>工作階段開始的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>順序識別碼，用於區分同日期、同時間開始的工作階段。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>tinyint</p></td>
<td><p>主要，外部</p></td>
<td><p>代表通話中使用的視訊線路類型。允許的值為：</p>
<ul>
<li><p>0 – 音訊</p></li>
<li><p>1 – 視訊</p></li>
<li><p>2 -- 全景視訊</p></li>
<li><p>3 – 應用程式/桌面共用</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>StreamID</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>應用程式共用資料流的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>JitterInterArrival</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>RTP 封包之間抵達時間的平均抖動。(抖動是估算通話「不穩定」的方法)。高抖動值通常是由下列幾種狀況造成：壅塞，或是媒體伺服器超載，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>RTP 封包之間抵達時間的最大抖動。(抖動是估算通話「不穩定」的方法)。高抖動值通常是由下列幾種狀況造成：壅塞，或是媒體伺服器超載，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RoundTrip</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包傳送至另一個端點再返回，平均所需的時間 (以毫秒為單位)。可接受的品質為來回時間 200 毫秒或更短。</p>
<p>國際電話路由、路由設定錯誤，或者媒體伺服器超過負載時，會造成來回時間值變得相當大。來回時間長會造成雙向、即時語音交談發生問題。</p></td>
</tr>
<tr class="even">
<td><p><strong>RoundTripMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包傳送至另一個端點再返回，最長所需的時間 (以毫秒為單位)。可接受的品質為來回時間 200 毫秒或更短。</p>
<p>國際電話路由、路由設定錯誤，或者媒體伺服器超過負載時，會造成來回時間值變得相當大。來回時間長會造成雙向、即時語音交談發生問題。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketLossRate</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包遺漏的平均速率 (當 RTP 封包 (在網際網路傳輸音訊和視訊使用的通訊協定) 無法抵達目的地時，就會發生封包遺漏)。高遺漏值通常是由下列幾種狀況造成：壅塞、頻寬不足、無線網路壅塞或干擾，或是媒體伺服器超載。封包遺漏一般會導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>PacketLossRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包遺漏的最大速率 (當 RTP 封包 (在網際網路傳輸音訊和視訊使用的通訊協定) 無法抵達目的地時，就會發生封包遺漏)。高遺漏值通常是由下列幾種狀況造成：壅塞、頻寬不足、無線網路壅塞或干擾，或是媒體伺服器超載。封包遺漏一般會導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketUtilization</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>傳送的封包數。</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEst</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>工作階段結束時估計可用的單向頻寬。報告值為每秒位元數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AppSharingPayloadDescription</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>應用程式共用裝載的說明。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向延遲的總數量。相對單向延遲是測量用戶端與伺服器之間的延遲時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向延遲的平均數量。相對單向延遲是測量用戶端與伺服器之間的延遲時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向延遲的最大數量。相對單向延遲是測量用戶端與伺服器之間的延遲時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>單向高載發生總次數。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。此計量測量用戶端與伺服器之間的資料流動。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向高載總密度。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。此計量測量用戶端與伺服器之間的資料流動。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向高載總持續時間。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。此計量測量用戶端與伺服器之間的資料流動。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>單向缺口發生總次數。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。缺口指的是這些高載之間的延遲。此計量測量用戶端與伺服器之間的資料流動。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向缺口總密度。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。缺口指的是這些高載之間的延遲。此計量測量用戶端與伺服器之間的資料流動。</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>單向缺口總持續時間。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。缺口指的是這些高載之間的延遲。此計量測量用戶端與伺服器之間的資料流動。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ApplicationSharingType</strong></p></td>
<td><p>Varchar(256)</p></td>
<td><p></p></td>
<td><p>應用程式角色 (共用者或檢視者) 及內容類型。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚的總處理時間。時間越長表示檢視時會感覺延遲越久。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚的平均處理時間。時間越長表示檢視時會感覺延遲越久。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚的最大處理時間。時間越長表示檢視時會感覺延遲越久。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚時處理時間內的高載發生次數。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚之處理時間內的高載密度。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚之處理時間內的高載持續時間。傳輸中資料以無法預測的爆衝方式流動，而非穩定的資料流，稱為「高載」傳輸。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚之處理時間內的缺口發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚之處理時間內的缺口密度。低缺口密度表示檢視的感覺較佳。</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>遠端桌面通訊協定 (RDP) 磚之處理時間內的缺口持續時間。缺口持續時間短表示檢視的感覺較佳。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CaptureTileRateTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>擷取磚的總速率 (單位為每秒磚數)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CaptureTileRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>擷取磚的平均速率 (單位為每秒磚數)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CaptureTileRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>擷取磚的最大速率 (單位為每秒磚數)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CaptureTileRateBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以擷取磚速率表示的高載發生次數 (單位為每秒磚數)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CaptureTileRateBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以擷取磚速率表示的高載密度 (單位為每秒磚數)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CaptureTileRateBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以擷取磚速率表示的高載持續時間 (單位為每秒磚數)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CaptureTileRateGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以擷取磚速率表示的缺口發生次數 (單位為每秒磚數)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CaptureTileRateGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以擷取磚速率表示的缺口密度 (單位為每秒磚數)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CaptureTileRateGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以擷取磚速率表示的缺口持續時間 (單位為每秒磚數)。</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的總百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SpoiledTilePercentAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的平均百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的最大百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SpoiledTilePercentBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的高載發生次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的高載密度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SpoiledTilePercentBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的高載持續時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的缺口發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SpoiledTilePercentGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>未抵達檢視者而被捨棄並以更新內容覆寫之內容的缺口密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>ScrapingFrameRateTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>從圖形來源消去的畫面總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>ScrapingFrameRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>從圖形來源消去的畫面平均數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ScrapingFrameRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>從圖形來源消去的畫面最大數。</p></td>
</tr>
<tr class="even">
<td><p><strong>ScrapingFrameRateBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以從圖形來源消去之畫面數表示的高載發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ScrapingFrameRateBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以從圖形來源消去之畫面數表示的高載密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>ScrapingFrameRateBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以從圖形來源消去之畫面數表示的高載持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ScrapingFrameRateGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以從圖形來源消去之畫面數表示的缺口發生次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>ScrapingFrameRateGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以從圖形來源消去之畫面數表示的缺口密度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ScrapingFrameRateGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以從圖形來源消去之畫面數表示的缺口持續時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingTileRateTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>檢視者接收到的傳入畫面總速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingTileRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>檢視者接收到的傳入畫面平均速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingTileRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>檢視者接收到的傳入磚最大速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingTileRateBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入磚速率表示之高載發生次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingTileRateBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入磚速率表示之高載密度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingTileRateBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入磚速率表示之高載持續時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingTileRateGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入磚速率表示之缺口發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingTileRateGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入磚速率表示之缺口密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingTileRateGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入磚速率表示之缺口持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingFrameRateTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>檢視者接收到的傳入畫面總速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingFrameRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>檢視者接收到的傳入畫面平均速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingFrameRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>檢視者接收到的傳入畫面最大速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingFrameRateBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入畫面速率表示之高載發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingFrameRateBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入畫面速率表示之高載密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingFrameRateBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入畫面速率表示之高載持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingFrameRateGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入畫面速率表示之缺口發生次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>IncomingFrameRateGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入畫面速率表示之缺口密度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IncomingFrameRateDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以檢視者接收到的傳入畫面速率表示之缺口持續時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingTileRateTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者的傳出磚總速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingTileRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者的傳出磚平均速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingTileRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者的傳出磚最大速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingTileRateBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出磚速率表示的高載發生次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingTileRateBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出磚速率表示的高載密度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingTileRateBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出磚速率表示的高載持續時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingTileRateGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出磚速率表示的缺口發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingTileRateGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出磚速率表示的缺口密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingTileRateGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出磚速率表示的缺口持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingFrameRateTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者的傳出畫面總速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingFrameRateAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者的傳出畫面平均速率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingFrameRateMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>傳送者的傳出畫面最大速率。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingFrameRateBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出畫面速率表示的高載發生次數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingFrameRateBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出畫面速率表示的高載密度。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingFrameRateBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出畫面速率表示的高載持續時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingFrameRateGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出畫面速率表示的缺口發生次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>OutgoingFrameRateGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出畫面速率表示的缺口密度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutgoingFrameRateGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>以傳送者之傳出畫面速率表示的缺口持續時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>AverageRectangleHeight</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>視訊解析度的平均高度 (以像素為單位)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AverageRectangleWidth</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>視訊解析度的平均寬度 (以像素為單位)。</p></td>
</tr>
<tr class="even">
<td><p><strong>Inbound</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>輸入傳輸的平均畫面速率 (以每秒畫面數為單位)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Outbound</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>輸出傳輸的平均畫面速率 (以每秒畫面數為單位)。</p></td>
</tr>
<tr class="even">
<td><p><strong>SenderIsCallerPAI</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>1 表示資料流是從呼叫者流向被呼叫者。</p>
<p>0 表示資料流是從被呼叫者流向呼叫者。</p></td>
</tr>
</tbody>
</table>


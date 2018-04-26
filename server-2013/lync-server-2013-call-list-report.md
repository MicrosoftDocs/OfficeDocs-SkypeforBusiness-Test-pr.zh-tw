---
title: Lync Server 2013：通話清單報告
TOCTitle: 通話清單報告
ms:assetid: 9739f9f0-7a37-4844-91d5-f089d2011013
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615020(v=OCS.15)
ms:contentKeyID: 49291727
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話清單報告

 

_**上次修改主題的時間：** 2015-03-09_

「通話清單報告」可為貴組織中撥打和接聽的個別通話提供經驗品質 (QoE) 計量。請注意，實際報告的計量將取決於您存取通話清單報告的方式。例如，如果您是從 [Lync Server 2013 中的裝置報告](lync-server-2013-device-report.md)開啟報告，將會看到如下計量 (這些計量也會出現在裝置報告中)：

  - 來電者的麥克風

  - 來電者的喇叭

  - 被呼叫者的麥克風

  - 被呼叫者的喇叭

  - 語音交換時間的比率

但是，如果您是從 [Lync Server 2013 中的位置報告](lync-server-2013-location-report.md)開啟通話清單報告，將看不到這些計量，而是看到如下的計量：

  - 來回時間 (ms)

  - 降低 (MOS)

  - 封包遺漏

  - 抖動 (ms)

這些是位置報告中會報告的計量。但是，您可以隨時按一下通話清單報告中的 \[詳細資料\] 計量，以獲得任何通話的完整 QoE 資訊。

## 存取通話清單報告

您可以從下列任何報告存取通話清單報告：

  - [Lync Server 2013 中的位置報告](lync-server-2013-location-report.md) (按一下 \[通話數量\] 或 \[收訊不良通話百分比\] 計量)

  - [Lync Server 2013 中的裝置報告](lync-server-2013-device-report.md) (按一下 \[通話數量\] 或 \[收訊不良通話百分比\] 計量)

  - [Lync Server 2013 中的媒體品質摘要報告](lync-server-2013-media-quality-summary-report.md) (按一下 \[通話數量\] 或 \[收訊不良通話百分比\] 計量)

  - [Lync Server 2013 中的伺服器效能報告](lync-server-2013-server-performance-report.md) (按一下 \[通話數量\] 或 \[收訊不良通話百分比\] 計量)

在通話清單報告中，按一下 \[詳細資料\] 計量即可存取 [Lync Server 2013 中的詳細通話報告](lync-server-2013-call-detail-report.md)。

## 充分運用通話清單報告

如果您記不得通話清單報告的某些計量 (例如 \[語音交換時間的比率\]) 實際在測量些什麼，請將滑鼠移到計量標籤，隨即會出現工具提示來提供該計量的簡短說明。

## 篩選器

無。您無法篩選通話清單報告。

## 計量

下表列出了通話清單報告針對每段通話提供的資訊。

### 通話清單報告計量

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序這個項目嗎？</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>詳細資料</strong></p></td>
<td><p>否</p></td>
<td><p>按一下它，就會顯示出有關該通話的其他資訊報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>來電者</strong></p></td>
<td><p>是</p></td>
<td><p>發話者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>受話者</strong></p></td>
<td><p>是</p></td>
<td><p>受話者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>開始時間</strong></p></td>
<td><p>是</p></td>
<td><p>通話的開始日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>結束時間</strong></p></td>
<td><p>是</p></td>
<td><p>通話的結束日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>呼叫者使用者代理程式</strong></p></td>
<td><p>是</p></td>
<td><p>發話的一方所使用的軟體。</p></td>
</tr>
<tr class="odd">
<td><p><strong>被呼叫者使用者代理程式</strong></p></td>
<td><p>是</p></td>
<td><p>受話的一方所使用的軟體。</p></td>
</tr>
<tr class="even">
<td><p><strong>來回時間 (ms)</strong></p></td>
<td><p>是</p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包傳送至另一個端點再返回，平均所需的時間 (毫秒)。來回時間為 100 ms (毫秒) 或更少被視為可接受的品質。</p>
<p>國際電話路由、路由設定錯誤，或者媒體伺服器超過負載時，會造成來回時間值變得相當大。來回時間太長會使得雙向、即時的音訊通話變得難以進行。</p></td>
</tr>
<tr class="odd">
<td><p><strong>降低 (MOS)</strong></p></td>
<td><p>是</p></td>
<td><p>通話時經歷的平均意見分數 (MOS) 平均降級量。降級值的範圍可以從 0.0 (低) 到 5.0 (高)。值為 0.5 或更少的時間表示可接受的降級。根據歷史經驗，平均意見分數的計算方式就是讓使用者為通話品質打上 1 到 5 的分數。在 Lync Server 中， Lync Server 使用一組演算法來預測使用者如何為通話打分數。</p>
<p>網路堵塞、頻寬不足、無線網路堵塞或受到干援，或者媒體伺服器或端點超過負載，都會造成降級值變得相當高。降級太高會造成音訊扭曲或遺漏。</p></td>
</tr>
<tr class="even">
<td><p><strong>封包遺漏</strong></p></td>
<td><p>是</p></td>
<td><p>RTP 封包遺漏的平均速率 (當 RTP 封包 (在網際網路傳輸音訊和視訊使用的通訊協定) 無法抵達目的地時，就會發生封包遺漏)。高遺漏值通常是由下列幾種狀況造成：壅塞、頻寬不足、無線網路壅塞或干擾，或是媒體伺服器超載。封包遺漏一般會導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>抖動</strong></p></td>
<td><p>是</p></td>
<td><p>RTP 封包之間抵達時間的平均抖動。(抖動是估算通話「不穩定」的方法)。高抖動值通常是由下列幾種狀況造成：壅塞，或是媒體伺服器超載，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>修復隱藏比率</strong></p></td>
<td><p>是</p></td>
<td><p>隱藏音訊樣本與樣本總數的平均比率 (隱藏音訊樣本是一種用於平滑音訊因一般網路封包遺漏而造成突然轉變的技術)。高比值表示因為封包遺漏或抖動而運用了大量的遺失隱藏技術，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>修復延伸比率</strong></p></td>
<td><p>是</p></td>
<td><p>延伸音訊樣本與樣本總數的平均比率 (延伸音訊是指當偵測到網路封包遺漏時，為了維持通話品質而延展的音訊)。高比值表示有大量因抖動產生的樣本延伸，導致音訊聽起來像機器人或扭曲。</p></td>
</tr>
<tr class="even">
<td><p><strong>修復壓縮比率</strong></p></td>
<td><p>是</p></td>
<td><p>壓縮音訊樣本與樣本總數的平均比率 (壓縮音訊是指當偵測到網路封包遺漏時，為了維持通話品質而壓縮的音訊)。高比值表示有大量因抖動產生的樣本壓縮，導致音訊聽起來變快或扭曲。</p></td>
</tr>
<tr class="odd">
<td><p><strong>連接性</strong></p></td>
<td><p>是</p></td>
<td><p>無線通訊連結的類型。一般來說會是下面其中一種：</p>
<ul>
<li><p>中繼</p></li>
<li><p>直接</p></li>
</ul></td>
</tr>
</tbody>
</table>


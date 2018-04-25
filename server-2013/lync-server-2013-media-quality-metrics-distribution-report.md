---
title: 媒體品質計量散佈報告
TOCTitle: 媒體品質計量散佈報告
ms:assetid: d07996e6-b0a5-4ff8-9512-ab707762b4e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205262(v=OCS.15)
ms:contentKeyID: 49292381
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 媒體品質計量散佈報告

 

_**上次修改主題的時間：** 2015-03-09_

媒體品質計量散佈報告顯示的圖表，可讓您看出散佈的經驗品質計量值，例如抖動或封包遺漏。舉例來說，假設使用者總共撥打 10 通電話；這 10 通電話回報下列的往返時間：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>電話編號</th>
<th>往返時間 (毫秒)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>50</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>50</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p>50</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>4550</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>50</p></td>
</tr>
</tbody>
</table>


這些來回時間的平均值為 500 毫秒 (5000 除以 10)。500 毫秒可說是極長的來回時間；因此，您可能 是遇到嚴重的網路壅塞問題 (網路超過負載通常會導致來回時間冗長)。

事實上，90% 的通話都有極佳的來回時間；只不過，有一通來回時間過長的電話拖累整體結果。如果您只查看平均的來回時間，所得到的結論可能會錯得離譜。

媒體品質計量散佈報告可以圖形來顯示指定計量的散佈情形 (例如來回時間)，以免您妄下定論。這些圖表讓您一目了然，清楚知道品質很佳的電話有 9 通，而品質很差的電話只有 1 通。不可否認，您仍會想進一步調查該通電話；不過，10 通電話裡有 9 通品質很好的電話，表示至少目前不必對網路做出任何變更。

## 篩選器

篩選可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。下表列出您可以搭配媒體品質計量散佈報告使用的篩選條件。

### 媒體品質計量散佈報告篩選器

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>從</strong></p></td>
<td><p>時間範圍的開始日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>在 X 軸上的最小值</strong></p></td>
<td><p>要在圖表 X 軸上顯示的最低值。</p></td>
</tr>
<tr class="even">
<td><p><strong>在 X 軸上的最大值</strong></p></td>
<td><p>要在圖表 X 軸上顯示的最高值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>存取類型</strong></p></td>
<td><p>指出撥打電話時，用戶端是登入內部網路或外部網路。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>內部</p></li>
<li><p>外部</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>VPN</strong></p></td>
<td><p>指出撥打電話時，外部用戶端是否使用虛擬私人網路 (VPN) 連線。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>VPN</p></li>
<li><p>非 VPN</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>網路類型</strong></p></td>
<td><p>指出撥打電話時，用戶端連線的網路類型。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>有線</p></li>
<li><p>無線</p></li>
</ul></td>
</tr>
</tbody>
</table>


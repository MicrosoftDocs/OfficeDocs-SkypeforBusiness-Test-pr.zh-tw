---
title: Lync Server 2013：詳細通話報告
TOCTitle: 詳細通話報告
ms:assetid: 38862e35-3fec-41b9-a035-0b301942d446
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558637(v=OCS.15)
ms:contentKeyID: 49290608
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的詳細通話報告

 

_**上次修改主題的時間：** 2015-03-09_

\[通話詳細資料報告\] 可提供個別通話的詳細資訊；報告中包含幾乎所有 Lync Server 所收集的「經驗品質」計量及統計資料，分為如下的報告區段：

  - 通話資訊

  - 呼叫者裝置和訊號計量

  - 被呼叫者裝置和訊號計量

  - 呼叫者用戶端事件

  - 被呼叫者用戶端事件

  - 音訊資料流 (呼叫者至被呼叫者)

  - 視訊資料流 (呼叫者至被呼叫者)

  - 音訊資料流 (被呼叫者至呼叫者)

  - 視訊資料流 (被呼叫者至呼叫者)

請注意，在指定報告上所見的類別及計量取決於兩個因素：工作階段類型，以及工作階段中所使用的端點類型。例如，純音訊通話不會報告視訊資料流計量，這是因為該通話沒有視訊資料流。同樣地，報告可能會只列出呼叫者統計資料，而沒有被呼叫者統計資料。這通常是因為被呼叫者並非使用 SIP 相容的裝置。端點會負責在通話結束時報告統計資料；不過行動電話 (對 SIP 或 SIP 統計資料一無所悉) 就無法報告該類資訊。如果您與某人通話，而他們使用行動電話接聽，則通話結束時將無法從該行動電話取得報告。

當您想確認指定通話為何發生媒體品質問題的確切原因時，\[通話詳細資料報告\] 最派得上用場。

## 存取通話詳細資料報告

您可從下列報告中存取 \[通話詳細資料報告\]：

  - [Lync Server 2013 中的位置報告](lync-server-2013-location-report.md) (按一下 \[通話數\] 或 \[通話不良百分比\] 計量)

  - [Lync Server 2013 中的媒體品質摘要報告](lync-server-2013-media-quality-summary-report.md) (按一下 \[通話數\] 或 \[通話不良百分比\] 計量)

  - [Lync Server 2013 中的媒體品質比較報表](lync-server-2013-media-quality-comparison-report.md) (按一下 \[ [Lync Server 2013 中的通話清單報告](lync-server-2013-call-list-report.md)\] 及 \[詳細資料\] 計量)。

  - [Lync Server 2013 中的伺服器效能報告](lync-server-2013-server-performance-report.md) (按一下 \[通話數\] 或 \[通話不良百分比\] 計量)

  - [Lync Server 2013 中的通話清單報告](lync-server-2013-call-list-report.md) (按一下 \[詳細資料\] 計量)

如要從 \[通話詳細資料報告\] 中存取 \[ [Lync Server 2013 中的裝置報告](lync-server-2013-device-report.md)\]，可按一下下列計量之一：

  - 擷取裝置

  - 轉換裝置

按一下 \[A/V Edge Server\] 計量也可存取 \[伺服器媒體品質趨勢報告\]。

## 發揮通話詳細資料報告的最大效用

\[通話詳細資料報告\] 通常涵蓋超過 250 個不同的計量，包括麥克風時間戳記漂移、低 SNR 時間及近端回音時間等項目。如果不記得這些計量實際上測量什麼，可嘗試將滑鼠移至計量標籤上，通常會顯示工具提示來說明該計量。

如果找不到某個計量，可在搜尋方塊中輸入部分計量標籤，然後按一下 \[搜尋\]。例如，如果找不到 \[低 Low SNR 時間\] 計量，可在搜尋方塊中輸入 SNR，然後按一下 \[搜尋\]。

請注意，報告只會追蹤有關通話的資訊。並不會記錄通話本身。

## 篩選器

無。您無法篩選詳細通話報告。

## 計量

下表列出每個通話的詳細通話報告。

### 詳細通話報告計量

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
<td><p><strong>呼叫者 PAI</strong></p></td>
<td><p>否</p></td>
<td><p>撥打通話之使用者的 P-Asserted-Identity。P-Asserted-Identity 可用來傳達信任網路中之使用者經驗證的身分識別。</p></td>
</tr>
<tr class="even">
<td><p><strong>呼叫者 URI</strong></p></td>
<td><p>否</p></td>
<td><p>撥打通話之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>呼叫者者端點</strong></p></td>
<td><p>否</p></td>
<td><p>用來撥打通話的裝置。</p></td>
</tr>
<tr class="even">
<td><p><strong>呼叫者使用者代理程式</strong></p></td>
<td><p>否</p></td>
<td><p>撥打通話之裝置上所使用的軟體。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話開始</strong></p></td>
<td><p>否</p></td>
<td><p>啟動通話的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>中繼伺服器旁路通話</strong></p></td>
<td><p>否</p></td>
<td><p>指出通話是連接至 PSTN 語音閘道或完整 IP-PBX，而未通過中繼伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>呼叫者 OS</strong></p></td>
<td><p>否</p></td>
<td><p>呼叫者電腦的作業系統。</p></td>
</tr>
<tr class="even">
<td><p><strong>呼叫者 CPU</strong></p></td>
<td><p>否</p></td>
<td><p>安裝在啟動通話之使用者電腦上的 CPU。</p></td>
</tr>
<tr class="odd">
<td><p><strong>呼叫者 CPU 核心編號</strong></p></td>
<td><p>否</p></td>
<td><p>啟動通話者所使用電腦的處理器編號。</p></td>
</tr>
<tr class="even">
<td><p><strong>呼叫者 CPU 速度</strong></p></td>
<td><p>否</p></td>
<td><p>啟動通話者所使用電腦的 CPU 時脈速度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>呼叫者 CPU 模擬</strong></p></td>
<td><p>否</p></td>
<td><p>啟動通話者所使用電腦上的虛擬化 (若有的話)。</p></td>
</tr>
<tr class="even">
<td><p><strong>被呼叫者 PAI</strong></p></td>
<td><p>否</p></td>
<td><p>受邀加入通話之使用者的 P-Asserted-Identity。P-Asserted-Identity 可用來傳達信任網路中之使用者經驗證的身分識別。</p></td>
</tr>
<tr class="odd">
<td><p><strong>被呼叫者 URI</strong></p></td>
<td><p>否</p></td>
<td><p>被呼叫使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>被呼叫者端點</strong></p></td>
<td><p>否</p></td>
<td><p>用來接收通話的裝置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>被呼叫者使用者代理程式</strong></p></td>
<td><p>否</p></td>
<td><p>接收通話之裝置上所使用的軟體。</p></td>
</tr>
<tr class="even">
<td><p><strong>持續期間</strong></p></td>
<td><p>否</p></td>
<td><p>通話時間長度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>媒體旁路警告旗標</strong></p></td>
<td><p>否</p></td>
<td><p>略過中繼伺服器時發出的警告。</p></td>
</tr>
<tr class="even">
<td><p><strong>被呼叫者 OS</strong></p></td>
<td><p>否</p></td>
<td><p>被呼叫使用者的電腦作業系統。</p></td>
</tr>
<tr class="odd">
<td><p><strong>被呼叫者 CPU</strong></p></td>
<td><p>否</p></td>
<td><p>安裝在被呼叫使用者電腦上的 CPU。</p></td>
</tr>
<tr class="even">
<td><p><strong>被呼叫者核心編號</strong></p></td>
<td><p>否</p></td>
<td><p>被呼叫者所使用電腦中的處理器編號。</p></td>
</tr>
<tr class="odd">
<td><p><strong>被呼叫者 CPU 速度</strong></p></td>
<td><p>否</p></td>
<td><p>被呼叫者所使用電腦中的 CPU 時脈速度。</p></td>
</tr>
<tr class="even">
<td><p><strong>被呼叫者 CPU 虛擬</strong></p></td>
<td><p>否</p></td>
<td><p>被呼叫者所使用電腦上的虛擬化 (若有的話)。</p></td>
</tr>
</tbody>
</table>


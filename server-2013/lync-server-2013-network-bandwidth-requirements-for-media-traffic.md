---
title: 媒體流量的網路頻寬需求
TOCTitle: 媒體流量的網路頻寬需求
ms:assetid: 83e83b16-0f0e-4d87-901a-0faa4618cdc2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688118(v=OCS.15)
ms:contentKeyID: 49890148
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 媒體流量的網路頻寬需求

 

_**上次修改主題的時間：** 2015-03-09_

網路規劃中一個重要的部份是確保網路能夠處理 Lync Server 所產生的媒體流量。本節將協助您規劃這類媒體流量。

## 媒體流量網路使用方式

由於不同變數 (例如轉碼器使用率、解析度和活動層級) 的數目，計算媒體流量頻寬使用率將是一項挑戰。頻寬使用率是使用的轉碼器和資料流活動的函數，這兩者會根據案例的不同而有所差異。下表列出在 Lync Server 2013 案例中常用的音訊轉碼器。

### 音訊轉碼器頻寬

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>音訊轉碼器</th>
<th>案例</th>
<th>音訊承載位元速率 (KBPS)</th>
<th>僅頻寬音訊承載和 IP 標頭 (Kbps)</th>
<th>頻寬音訊承載、IP 標頭、UDP、RTP 和 SRTP (Kbps)</th>
<th>頻寬音訊承載、IP 標頭、UDP、RTP、SRTP 和正向錯誤更正 (Kbps)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTAudio 寬頻</p></td>
<td><p>對等</p></td>
<td><p>29.0</p></td>
<td><p>45.0</p></td>
<td><p>57.0</p></td>
<td><p>86.0</p></td>
</tr>
<tr class="even">
<td><p>RTAudio 窄頻</p></td>
<td><p>對等，PSTN</p></td>
<td><p>11.8</p></td>
<td><p>27.8</p></td>
<td><p>39.8</p></td>
<td><p>51.6</p></td>
</tr>
<tr class="odd">
<td><p>G.722</p></td>
<td><p>會議</p></td>
<td><p>64.0</p></td>
<td><p>80.0</p></td>
<td><p>95.6</p></td>
<td><p>159.6</p></td>
</tr>
<tr class="even">
<td><p>G.722 立體聲</p></td>
<td><p>對等，會議</p></td>
<td><p>128.0</p></td>
<td><p>144.0</p></td>
<td><p>159.6</p></td>
<td><p>223.6</p></td>
</tr>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>PSTN</p></td>
<td><p>64.0</p></td>
<td><p>80.0</p></td>
<td><p>92.0</p></td>
<td><p>156.0</p></td>
</tr>
<tr class="even">
<td><p>Siren</p></td>
<td><p>會議</p></td>
<td><p>16.0</p></td>
<td><p>32.0</p></td>
<td><p>47.6</p></td>
<td><p>63.6</p></td>
</tr>
</tbody>
</table>


上表中的頻寬數字以 20ms 封包 (每秒 50 個封包) 為依據，對於 Siren 和 G.722 包括會議案例中的安全即時傳輸通訊協定 (SRTP) 額外負荷，因此假定資料流處於 100% 活動狀態。連結上發生封包遺失時將動態使用正向錯誤更正 (FEC)，以協助維護音訊資料流的品質。

G.722 轉碼器的立體聲版本由採用 Lync Room System 為基礎的系統所使用，能夠進行立體聲麥克風擷取，以便聆聽者更能夠辨別會議室中的多位說話者。

對於視訊，預設轉碼器是 H.264/MPEG-4 Part 10 Advanced Video Coding 標準版 (加裝暫時擴充的可調整視訊編碼擴充)。為了維持與 Lync 2010 或 Office Communicator 2007 R2 用戶端的互通性，對於 Lync 2013 和舊版用戶端之間的對等通話仍將使用 RTVideo 轉碼器。在與 Lync 2013 和舊版用戶端進行的會議工作階段中，Lync 2013 端點可能會使用視訊轉碼器將視訊編碼，並將 H.264 位元資料流傳送到 Lync 2013，而且將 RTVideo 位元資料流傳送到 Lync 2010 或 Office Communicator 2007 R2 用戶端。

所需頻寬依解析度、品質和播放速率而定。對於每個解析度，有兩個特別的位元速率：

  - **最大承載位元速率**   這是 Lync 2013 端點將用於此解析度支援的最大播放速率解析度的位元速率。此值特別的原因在於它允許最高品質和播放速率視訊。

  - **最小承載位元速率**   這是 Lync 2013 端點將切換到次低解析度的位元速率。為了確保達到一定的解析度，可用的視訊承載位元速率不可低於該解析度的位元速率下限。此值很特別，您可以從而了解最大位元速率不可用或不可行的情況下可能的最小值。對於某些使用者，如此的低位元速率視訊可能會被視為無法接受的視訊體驗，因此請謹慎使用這些位元速率。請注意，對於使用者很少或沒有動作的視訊場景，實際的位元速率可能暫時低於位元速率下限。

Lync 2013 支援更多解析度。這能夠讓您更加調整為不同的網路頻寬和接收用戶端功能。此外，Lync 2013 的預設外觀比例也變更為 16:9。對於無法以 16:9 外觀比例擷取的網路攝影機，仍然支援 4:3 外觀比例。

### 視訊解析度頻寬

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>視訊轉碼器</th>
<th>解析度和外觀比例</th>
<th>最大視訊承載位元速率 (Kbps)</th>
<th>最小視訊承載位元速率 (Kbps)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>320x180 (16:9)</p>
<p>212x160 (4:3)</p></td>
<td><p>250</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>H.264/RTVideo</p></td>
<td><p>424x240 (16:9)</p>
<p>320x240 (4:3)</p></td>
<td><p>350</p></td>
<td><p>100</p></td>
</tr>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>480x270 (16:9)</p>
<p>424x320 (4:3)</p></td>
<td><p>450</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>H.264/RTVideo</p></td>
<td><p>640x360 (16:9)</p>
<p>640x480 (4:3)</p></td>
<td><p>800</p></td>
<td><p>300</p></td>
</tr>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>848x480 (16:9)</p></td>
<td><p>1500</p></td>
<td><p>400</p></td>
</tr>
<tr class="even">
<td><p>H.264</p></td>
<td><p>960x540 (16:9)</p></td>
<td><p>2000</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>H.264/RTVideo</p></td>
<td><p>1280x720 (16:9)</p></td>
<td><p>2500</p></td>
<td><p>700</p></td>
</tr>
<tr class="even">
<td><p>H.264</p></td>
<td><p>1920x1080 (16:9)</p></td>
<td><p>4000</p></td>
<td><p>1500</p></td>
</tr>
<tr class="odd">
<td><p>H.264/RTVideo</p></td>
<td><p>960x144 (20:3)</p></td>
<td><p>500</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>H.264</p></td>
<td><p>1280x192 (20:3)</p></td>
<td><p>1000</p></td>
<td><p>250</p></td>
</tr>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>1920x288 (20:3)</p></td>
<td><p>2000</p></td>
<td><p>500</p></td>
</tr>
</tbody>
</table>


使用視訊 FEC 時，它包括在視訊承載位元速率中，因此有還是沒有視訊 FEC，都沒有單獨的值。

端點不會持續對音訊或視訊封包進行資料流處理。依據不同的案例，有不同層級的資料流活動來指示為資料流傳送封包的頻率。資料流的活動依媒體和案例而定，而不是取決於使用的轉碼器。在對等案例中：

  - 端點只在使用者說話時傳送音訊資料流。

  - 這兩個參與者都會接收音訊資料流。

  - 如果使用視訊，這兩個端點會在整個通話期間傳送和接收視訊資料流。

  - 對於很少或沒有動作的視訊場景，實際的位元速率可能暫時變得相當低，因為視訊轉碼器將略過視訊的編碼區域而不變更。

在會議案例中：

  - 端點只在使用者說話時傳送音訊資料流。

  - 所有參與者都會接收音訊資料流。

  - 如果使用視訊，所有參與者都能夠接收多達五個接收視訊資料流和一個全景 (例如，外觀比例 20:3) 視訊資料流。根據預設，五個接收視訊資料流以目前發言者記錄為依據，但是使用者也可手動選取要接收視訊資料流的參與者。

  - 各個開啟使用者傳送視訊資料流的參與者都將傳送一個或多個視訊資料流。Lync 2013 新增傳送多達五個視訊資料流的功能，使所有接收用戶端的視訊品質最佳化。傳送的視訊資料流實際數目由傳送者依據 CPU 能力、可用上行連結頻寬和要求特定視訊串流的接收用戶端數目所決定。最常見的情況是，舊版用戶端加入會議時，傳送一個 H.264 和一個 RTVideo 視訊資料流。另一個常見的情況是，傳送多個 H.264 視訊資料流 (例如，不同視訊解析度的視訊資料流)，以配合不同的接收方要求。

除了音訊和視訊媒體的即時傳輸通訊協定 (RTP) 流量所需的頻寬，即時傳輸控制通訊協定 (RTCP) 也需要頻寬。RTCP 用於報告統計資料和頻外控制 RTP 資料流。為了規畫，將下表中的頻寬數字用於 RTCP 流量。這些值表示用於 RTCP 的最大頻寬及音訊和視訊資料流的不同 (由於控制資料的不同)

### RTCP 頻寬

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>媒體</th>
<th>RTCP 最大頻寬 (Kbps)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音訊</p></td>
<td><p>5</p></td>
</tr>
<tr class="even">
<td><p>視訊 (僅傳送/接收 H.264 或 RTVideo)</p></td>
<td><p>10</p></td>
</tr>
<tr class="odd">
<td><p>視訊 (傳送/接收 H.264 或 RTVideo)</p></td>
<td><p>15</p></td>
</tr>
</tbody>
</table>


為了進行容量規劃，需要以下兩種頻寬：

  - **沒有 FEC 的最大頻寬**   資料流將使用的最大頻寬，包括資料流的一般活動和沒有 FEC 的案例中使用的一般轉碼器。在此頻寬下，資料流處於 100% 活動狀態並且觸發使用 FEC 時沒有封包遺失。特別用於運算必須配置多少頻寬才能讓轉碼器在指定案例中使用。

  - **具有 FEC 的最大頻寬**   資料流使用的最大頻寬，包括資料流的一般活動和具有 FEC 的案例中使用的一般轉碼器。在此頻寬下，資料流處於 100% 活動狀態並且觸發使用 FEC 以改善品質時封包遺失。特別用於運算必須配置多少頻寬才能讓轉碼器在指定案例中使用，並且在封包遺失的情況下允許使用 FEC 保留品質。

下表還列出其他頻寬值**一般頻寬**。這是資料流使用的平均頻寬，包括資料流的一般活動和案例中使用的一般轉碼器。此頻寬可用於近似運算媒體流量在任何指定時間使用多少頻寬，而不可用於容量規劃，因為活動層級高於平均值時個別通話將超過此值。下表所列的一般視訊資料流以所測量的客戶資料中得到的不同視訊解析度為依據。例如，在對等工作階段中，大多數的使用者使用預設的視訊轉換時間，而某一比例的使用者將 Lync 提高或達到最大程度，以允許較高的視訊解析度。

下表提供了各種案例的三種頻寬值。

### 對等工作階段的音訊/視訊容量規劃

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>媒體</th>
<th>轉碼器</th>
<th>一般資料流頻寬 (Kbps)</th>
<th>沒有 FEC 的最大資料流頻寬</th>
<th>具有 FEC 的最大資料流頻寬</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音訊</p></td>
<td><p>RTAudio 寬頻</p></td>
<td><p>39.8</p></td>
<td><p>62</p></td>
<td><p>91</p></td>
</tr>
<tr class="even">
<td><p>音訊</p></td>
<td><p>RTAudio 窄頻</p></td>
<td><p>29.3</p></td>
<td><p>44.8</p></td>
<td><p>56.6</p></td>
</tr>
<tr class="odd">
<td><p>呼叫 Lync 2013 端點時的主要視訊</p></td>
<td><p>H.264</p></td>
<td><p>460</p></td>
<td><p>4010 (對於 1920x1080 的最大解析度)</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>呼叫 Lync 2010 或 Office Communicator 2007 R2 端點時的主要視訊</p></td>
<td><p>RTVideo</p></td>
<td><p>460</p></td>
<td><p>2510 (對於 1280x720 的最大解析度)</p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>呼叫 Lync 2013 端點時的全景視訊</p></td>
<td><p>H.264</p></td>
<td><p>190</p></td>
<td><p>2010 (對於 1920x288 的最大解析度)</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>呼叫 Lync 2010 或 Office Communicator 2007 R2 端點時的全景視訊</p></td>
<td><p>RTVideo</p></td>
<td><p>190</p></td>
<td><p>510 (對於 960x144 的最大解析度)</p></td>
<td><p>無</p></td>
</tr>
</tbody>
</table>


### 會議的音訊/視訊容量規劃

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>媒體</th>
<th>一般轉碼器</th>
<th>一般資料流頻寬 (Kbps)</th>
<th>沒有 FEC 的最大資料流頻寬</th>
<th>具有 FEC 的最大資料流頻寬</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音訊</p></td>
<td><p>G.722</p></td>
<td><p>46.1</p></td>
<td><p>100.6</p></td>
<td><p>164.6</p></td>
</tr>
<tr class="even">
<td><p>音訊</p></td>
<td><p>Siren</p></td>
<td><p>25.5</p></td>
<td><p>52.6</p></td>
<td><p>68.6</p></td>
</tr>
<tr class="odd">
<td><p>主要視訊接收</p></td>
<td><p>H.264 及/或 RTVideo</p></td>
<td><p>260</p></td>
<td><p>8015</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>主要視訊傳送</p></td>
<td><p>H.264 及/或 RTVideo</p></td>
<td><p>270</p></td>
<td><p>8015</p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>全景視訊接收</p></td>
<td><p>H.264 及/或 RTVideo</p></td>
<td><p>190</p></td>
<td><p>2010 (對於 1920x288 的最大解析度)</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>全景視訊傳送</p></td>
<td><p>H.264 及/或 RTVideo</p></td>
<td><p>190</p></td>
<td><p>2515 (對於使用多個解析度/轉碼器傳送位元資料流)</p></td>
<td><p>無</p></td>
</tr>
</tbody>
</table>


對於主要視訊，一般和最大資料流頻寬分別是所有接收視訊資料流的彙總頻寬和所有傳送視訊資料流的彙總頻寬。即使對於多個視訊資料流，一般視訊頻寬也小於對等工作階段的頻寬，因為許多視訊會議使用內容共用，使得視訊頻寬縮小，而導致視訊解析度降低。對於這兩個傳送和接收資料流，例如兩個連入 1920x1080p 視訊資料流，支援的最大彙總視訊承載頻寬為 8000 Kbps。

全景視訊的一般資料流頻寬是以僅傳輸 960x144 全景視訊的目前可用裝置為依據。一旦 1920x288 全景視訊的裝置可供使用，一般資料流頻寬便可望增加。

### PSTN 的音訊容量規劃

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>媒體</th>
<th>一般轉碼器</th>
<th>一般資料流頻寬 (Kbps)</th>
<th>沒有 FEC 的最大資料流頻寬</th>
<th>具有 FEC 的最大資料流頻寬</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音訊</p></td>
<td><p>G.711</p></td>
<td><p>64.8</p></td>
<td><p>97</p></td>
<td><p>161</p></td>
</tr>
<tr class="even">
<td><p>音訊</p></td>
<td><p>RTAudio 窄頻</p></td>
<td><p>30.9</p></td>
<td><p>44.8</p></td>
<td><p>56.6</p></td>
</tr>
</tbody>
</table>


這些表中的網路頻寬數字僅表示單向流量，包括每個資料流的 5 Kbps RTCP 流量負荷。對於視訊，最大視訊位元速率用於運算最大資料流。


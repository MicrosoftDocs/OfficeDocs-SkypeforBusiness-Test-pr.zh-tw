---
title: Lync Server 2013：AudioSignal 表格
TOCTitle: AudioSignal 表格
ms:assetid: 0013c8c6-cdf9-4d70-bc2a-cddd1560f66b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398064(v=OCS.15)
ms:contentKeyID: 49289883
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 AudioSignal 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄都代表一個端點的音訊訊號計量。通常，每個通話都會有兩筆記錄：一筆是針對發話者，另一筆則是針對受話者。


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
<td><p><strong>SendSignalLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>代表後類比增益控制音訊信號層級。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 30 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvSignalLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>請參閱 SendSignalLevel。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendNoiseLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>代表後類比增益控制音訊雜訊層級。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 35 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvNoiseLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>請參閱 SendNoiseLevel。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EchoReturn</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>回音往返失真增強計量。這個計量單位是 dB。愈低的值代表較少的回音。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioSpeakerGlitchRate</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>每五分鐘喇叭呈現平均故障數。為了達到優良的品質，此值應小於每五分鐘一次。非由 A/V 會議伺服器、中繼伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioMicGlitchRate</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>每五分鐘麥克風擷取平均故障數。為了達到優良的品質，此值應小於每五分鐘一次。非由 A/V 會議伺服器、中繼伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioTimestampDriftRateMic</strong></p></td>
<td><p>decimal(9.2)</p></td>
<td><p> </p></td>
<td><p>麥克風裝置時脈相對於 CPU 時脈的漂移率。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioTimestampDriftRateSpk</strong></p></td>
<td><p>decimal(9.2)</p></td>
<td><p> </p></td>
<td><p>喇叭裝置時脈相對於 CPU 時脈的漂移率。</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioTimestampErrorMicMs</strong></p></td>
<td><p>decimal(9.2)</p></td>
<td><p> </p></td>
<td><p>喇叭裝置時脈相對於 CPU 時脈的漂移率。</p>
<p>通話的最後 20 秒中，平均麥克風擷取資料流時間戳記錯誤 (毫秒)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioTimestampErrorSpkMs</strong></p></td>
<td><p>decimal(9.2)</p></td>
<td><p> </p></td>
<td><p>通話的最後 20 秒中，平均喇叭呈現資料流時間戳記錯誤 (毫秒)。</p></td>
</tr>
<tr class="even">
<td><p><strong>VsEntryCauses</strong></p></td>
<td><p>smallint</p></td>
<td><p> </p></td>
<td><p>語音切換是半雙工模式，具降低中斷功能。造成語音切換項目的原因：</p>
<p>ENTER_VS_BADTS 0x01</p>
<p>ENTER_VS_ECHO 0x02</p>
<p>ENTER_VS_FORCEORCONVERGENCE 0x04</p>
<p>ENTER_VS_DNLP 0x08</p>
<p>原因可能是這些個別原因的組合。ENTER_VS_FORCEORCONVERGENCE 只可基於測試目的，而由登錄機碼啟用。</p>
<p>此欄的資料類型在 Microsoft Lync Server 2013 中已變更。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EchoEventCauses</strong></p></td>
<td><p>Tinyint</p></td>
<td><p> </p></td>
<td><p>造成回音事件的原因：</p>
<p>ECHO_EVENT_BAD_TIMESTAMP 0x01</p>
<p>ECHO_EVENT_POSTAEC_ECHO 0x02</p>
<p>ECHO_EVENT_ANLP 0x04</p>
<p>ECHO_EVENT_DNLP 0x08</p>
<p>ECHO_EVENT_MIC_CLIPPING 0x10</p>
<p>ECHO_EVENT_BAD_STATE 0x20</p>
<p>原因可能是這些個別原因的組合。</p></td>
</tr>
<tr class="even">
<td><p><strong>EchoPercentMicIn</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>麥克風擷取資料流時偵測到回音的時間百分比。通常，耳機或話筒的值較低，而免持通話器或獨立喇叭的值較高。若是支援內建原音回音取消的裝置，較高的值表示回音流失。針對其他裝置，此計量不應用來評估裝置品質。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EchoPercentSend</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p></p></td>
<td><p>傳送資料流中偵測到的回音時間百分比。傳送資料流中有高百分比的回音代表回音流失。</p></td>
</tr>
<tr class="even">
<td><p><strong>RxAGCSignalLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>來自閘道的中繼伺服器上的接收信號層級；只適用於中繼伺服器。這個計量的單位是 dBoV。為了達到優良品質，可接受的範圍應該是 [-30 到 -18] dBoV。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RxAGCNoiseLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>來自閘道的中繼伺服器上的接收信號層級；只適用於中繼伺服器。這個計量的單位是 dBoV。為了達到優良品質，可接受的範圍應該小於 -50 dBoV。</p></td>
</tr>
<tr class="even">
<td><p><strong>RxAvgAGCGain</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>中繼伺服器端的自動增益控制 (AGC)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InitialSignalLevelRMS</strong></p></td>
<td><p>float</p></td>
<td><p> </p></td>
<td><p>傳入訊號的均方根 (RMS) (最高至通話前 30 秒)。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvSignalLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 1 上接收的訊號等級。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvSignalLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 2 上接收的訊號等級。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvNoiseLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 1 上接收的雜訊強度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvNoiseLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 2 上接收的雜訊強度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendSignalLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 1 上傳送的訊號等級。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendSignalLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 2 上傳送的訊號等級。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>SendNoiseLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 1 上傳送的雜訊強度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendNoiseLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>頻道 2 上傳送的雜訊強度。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
</tbody>
</table>


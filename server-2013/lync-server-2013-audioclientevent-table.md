---
title: Lync Server 2013：AudioClientEvent 表格
TOCTitle: AudioClientEvent 表格
ms:assetid: fef73d8f-7261-4e5b-9769-82435b007979
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413086(v=OCS.15)
ms:contentKeyID: 49292928
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 AudioClientEvent 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄都包含音訊通話中某端點的用戶端事件。一通電話通常會有兩筆記錄，一筆為發話者，另一筆為受話者。


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
<td><p><strong>NetworkSendQualityEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 NetworkSendQuality 事件的工作階段百分比。</p>
<p>出現抖動或封包遺失在網路品質來說相當嚴重，且會影響所接收的音訊品質。</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkReceiveQualityEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 ReceiveSendQuality 事件的工作階段百分比。</p>
<p>出現抖動或封包遺失在網路品質來說相當嚴重，且會影響所接收的音訊品質。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NetworkDelayEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 Delay 事件的工作階段百分比。網路延遲是嚴重問題，且會因無法進行互動通訊而影響使用體驗</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkBandwidthLowEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 LowBandwidth 活動的工作階段百分比。可用的頻寬不足，無法提供可接受程度的語音經驗。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CPUInsufficientEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 insufficient CPU 事件的工作階段百分比。CPU 週期不足以處理目前作用中的工作形式與應用程式。這會導致聲道失真。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceHalfDuplexAECEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceHalfDuplexAEC 事件的工作階段百分比。為避免發出回音，系統會進入半雙工。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceRenderNotFunctioningEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceRenderNotFunctioning 事件的工作階段百分比。目前會為運作不正常的工作階段使用轉換裝置。這可能會導致單向音訊問題。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceCaptureNotFunctioningEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceCaptureNotFunctioning 事件的工作階段百分比。目前會為運作不正常的工作階段使用擷取裝置。這可能會導致單向音訊問題。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceGlitchesEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceGlitches 事件的工作階段百分比。轉換音訊時發生嚴重故障，導致失真。這些故障有可能是因為驅動器問題、程序呼叫延期 (DPC) 風暴 (驅動器) 以及 CPU 使用率過高。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceLowSNREventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceLowSNR 事件的工作階段百分比。擷取品質非常糟，有可能是非常吵雜或使用者離麥克風太遠說話。這會導致失真。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceLowSpeechLevelEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceLowSpeechLevel 事件的工作階段百分比。使用者說話聲音太小且系統無法再加大。這有可能會導致失真或發現變成單向音訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceClippingEventRatio</strong></p></td>
<td><p>Decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceClipping 事件的工作階段百分比。</p>
<p>在近端麥克風上出現?嗒聲時，遠端因為此雜音而失真。請儘量避免在近端麥克風上出現?嗒聲。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceEchoEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceEchoEvent 事件的工作階段百分比。裝置或設定發出超過系統能力所能補償的回音。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceNearEndToEchoRatioEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p> </p></td>
<td><p>因「故障」狀態而觸發 DeviceNearEndToEchoRatio 事件的工作階段百分比。使用者說話聲音相較於目前所擷取到的回音來得小，如此會影響使用者體驗，讓原本可以輕易中斷使用者的動作變得不易執行。請降低喇叭音量，將麥克風移到和說話者較近的地方。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceMultipleEndpointsEventCount</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>在工作階段期間因「故障」狀態而觸發 DeviceMultipleEndpoints 事件的次數數目。已偵測到相同工作階段中有多個音訊端點，且系統已經由降低所呈現的音量而加以補償。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceHowlingEventCount</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>在工作階段期間因「故障」狀態而觸發 DeviceHowlingEvent 事件的次數數目。已偵測到音訊回饋迴路 (因多端點共用音訊路徑所導致)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceRenderZeroVolumeEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p></p></td>
<td><p>因為處於「不良」狀態而引發之 DeviceRenderZeroVolume 事件的工作階段百分比。已將轉換裝置設為零量。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceRenderMuteEventRatio</strong></p></td>
<td><p>decimal(5.2)</p></td>
<td><p></p></td>
<td><p>因為處於「不良」狀態而引發之 DeviceRenderMute 事件的工作階段百分比。已將轉換裝置靜音。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
</tbody>
</table>


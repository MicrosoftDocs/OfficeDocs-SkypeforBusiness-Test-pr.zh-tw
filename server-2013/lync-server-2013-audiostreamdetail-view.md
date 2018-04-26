---
title: AudioStreamDetail 檢視
TOCTitle: AudioStreamDetail 檢視
ms:assetid: b6a435b3-103c-41c4-96ed-33c3784534c0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721859(v=OCS.15)
ms:contentKeyID: 49890273
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# AudioStreamDetail 檢視

 

_**上次修改主題的時間：** 2015-03-09_

AudioStreamDetail 檢視可儲存資料庫中每個音訊資料流的資訊。此檢視已於 Microsoft Lync Server 2013 引進使用。.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SessionTime</p></td>
<td><p>datetime</p></td>
<td><p>參考來源：<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>SessionSeq</p></td>
<td><p>int</p></td>
<td><p>參考來源：<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>StreamId</p></td>
<td><p>int</p></td>
<td><p>媒體行中的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p>StartTime</p></td>
<td><p>datetime</p></td>
<td><p>工作階段的開始時間。</p></td>
</tr>
<tr class="odd">
<td><p>EndTime</p></td>
<td><p>datetime</p></td>
<td><p>工作階段的結束時間。</p></td>
</tr>
<tr class="even">
<td><p>DialogCategory</p></td>
<td><p>bit</p></td>
<td><p>對話類別；0 代表 Lync Server 到中繼伺服器計量；1 代表中繼伺服器到 PSTN 閘道計量。</p></td>
</tr>
<tr class="odd">
<td><p>MediationServerBypassFlag</p></td>
<td><p>bit</p></td>
<td><p>指出是否略過通話的旗標。</p></td>
</tr>
<tr class="even">
<td><p>MediaBypassWarningFlag</p></td>
<td><p>int</p></td>
<td><p>如果欄位出現的話，會說明為何某通電話未被略過，即便它符合要略過的識別碼。只定義一個值。</p>
<p>0x0001 – 預設網路介面卡未知的旁路識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>CallPriority</p></td>
<td><p>int</p></td>
<td><p>通話優先順序。</p></td>
</tr>
<tr class="even">
<td><p>CallerPool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者集區的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p>CalleePool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者集區的 FQDN。</p></td>
</tr>
<tr class="even">
<td><p>Caller</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>發話者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p>Callee</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>受話者的 URI。</p></td>
</tr>
<tr class="even">
<td><p>CallerUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者的使用者代理字串。</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>發話者的使用者代理類型。如需詳細資訊，請參閱 <a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>CallerUserAgentCategory</p></td>
<td><p>nvarchar(64)</p></td>
<td><p>發話者的使用者代理類別。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者的使用者代理字串。</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>受話者的使用者代理類型。如需詳細資訊，請參閱 <a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserAgentCategory</p></td>
<td><p>nvarchar(64)</p></td>
<td><p>受話者的使用者代理類別。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a>。</p></td>
</tr>
<tr class="even">
<td><p>CallerEndpoint</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者的端點名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeEndpoint</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者的端點名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerOS</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>發話者端點的作業系統 (OS)。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeOS</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>受話者端點的作業系統 (OS)。</p></td>
</tr>
<tr class="even">
<td><p>CallerCPUName</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>發話者端點的 CPU 名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCPUName</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>受話者端點的 CPU 名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerCPUNumberOfCores</p></td>
<td><p>smallint</p></td>
<td><p>發話者端點中的 CPU 核心數。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCPUNumberOfCores</p></td>
<td><p>smallint</p></td>
<td><p>受話者端點中的 CPU 核心數。</p></td>
</tr>
<tr class="even">
<td><p>CallerCPUProcessorSpeed</p></td>
<td><p>int</p></td>
<td><p>發話者端點的 CPU 處理器速度。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCPUProcessorSpeed</p></td>
<td><p>int</p></td>
<td><p>受話者端點的 CPU 處理器速度。</p></td>
</tr>
<tr class="even">
<td><p>CallerVirtualizationFlag</p></td>
<td><p>tinyint</p></td>
<td><p>指出發話者的系統是否在虛擬化環境中執行。如需詳細資訊，請參閱<a href="lync-server-2013-endpoint-table.md">Lync Server 2013 中的 Endpoint 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeVirtualizationFlag</p></td>
<td><p>tinyint</p></td>
<td><p>指出受話者的系統是否在虛擬化環境中執行。如需詳細資訊，請參閱<a href="lync-server-2013-endpoint-table.md">Lync Server 2013 中的 Endpoint 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>CorrelationKey</p></td>
<td><p></p></td>
<td><p>關聯索引鍵。參考來源：<a href="lync-server-2013-sessioncorrelation-table.md">Lync Server 2013 中的 SessionCorrelation 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>ConnectivityIce</p></td>
<td><p>tinyint</p></td>
<td><p>媒體路徑的相關資訊，例如直接或轉送。 如需詳細資訊，請參閱 <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>CallerIceWarningFlags</p></td>
<td><p>int</p></td>
<td><p>發話者的位元旗標中描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeIceWarningFlags</p></td>
<td><p>int</p></td>
<td><p>受話者的位元旗標中描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞。</p></td>
</tr>
<tr class="even">
<td><p>Transport</p></td>
<td><p>tinyint</p></td>
<td><p>傳輸類型：0 是 UDP，1 是 TCP。</p></td>
</tr>
<tr class="odd">
<td><p>CallerIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者的 IP 位址。這可能是 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="even">
<td><p>CallerPort</p></td>
<td><p>int</p></td>
<td><p>發話者使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p>CallerInside</p></td>
<td><p>bit</p></td>
<td><p>指出發話者是否位於內部網路：1 表示發話者位於企業網路，0 表示發話者位於外部網路。</p></td>
</tr>
<tr class="even">
<td><p>CalleeIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>受話者的 IP 位址。這可能是 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p>CalleePort</p></td>
<td><p>int</p></td>
<td><p>受話者使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CalleeInside</p></td>
<td><p>bit</p></td>
<td><p>指出受話者是否位於內部網路：1 表示受話者位於企業網路，0 表示受話者位於外部網路。</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserSite</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>發話者的網站名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerRegion</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>發話者網站的國家/地區名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserSite</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>受話者的網站名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRegion</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>受話者網站的國家/地區名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerRelayIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者使用之 A/V Edge Service 的 IP 位址。如需詳細資訊，請參閱 <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>。</p></td>
</tr>
<tr class="even">
<td><p>CallerRelayPort</p></td>
<td><p>int</p></td>
<td><p>發話者在 A/V Edge Service 上使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRelayIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>受話者使用之 A/V Edge Service 的 IP 位址機碼。如需詳細資訊，請參閱 <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRelayPort</p></td>
<td><p>int</p></td>
<td><p>受話者在 A/V Edge Service 上使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p>CallerCaptureDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的擷取裝置名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerRenderDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的轉換裝置名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerCaptureDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的擷取裝置驅動程式名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerRenderDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的轉換裝置驅動程式名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCaptureDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的擷取裝置名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRenderDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的轉換裝置名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCaptureDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的擷取裝置驅動程式名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRenderDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的轉換裝置驅動程式名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerNetworkConnectionType</p></td>
<td><p>tinyint</p></td>
<td><p>發話者的網路連線類型：0 是有線，1 是無線。</p></td>
</tr>
<tr class="even">
<td><p>CallerVPN</p></td>
<td><p>bit</p></td>
<td><p>指出發話者是否連線到虛擬私人網路：1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="odd">
<td><p>CallerLinkSpeed</p></td>
<td><p>decimal(18,0)</p></td>
<td><p>發話者端點的網路連結速度 (bps)。</p></td>
</tr>
<tr class="even">
<td><p>CalleeNetworkConnectionType</p></td>
<td><p>tinyint</p></td>
<td><p>受話者的網路連線類型：0 是有線，1 是無線。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeVPN</p></td>
<td><p>bit</p></td>
<td><p>指出發話者是否連線到虛擬私人網路：1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="even">
<td><p>CalleeLinkSpeed</p></td>
<td><p>decimal(18,0)</p></td>
<td><p>受話者端點的網路連結速度 (bps)。</p></td>
</tr>
<tr class="odd">
<td><p>ConversationalMOS</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>音訊工作階段的窄頻交談方式 MOS (兩種音訊資料流皆為依據)。</p></td>
</tr>
<tr class="even">
<td><p>AppliedBandwidthLimit</p></td>
<td><p>int</p></td>
<td><p>在指定各種原則設定 (TURN、API、SDP、Policy Server 等等) 的情況下，套用至指定傳送端資料流的實際頻寬。不要將這個與有效頻寬混淆，因為根據頻寬預估值，會有較低的有效頻寬。基本上，除了頻寬預估值規定的限制以外，這是傳送端資料流所能取得的最大頻寬。</p></td>
</tr>
<tr class="odd">
<td><p>JitterInterArrival</p></td>
<td><p>int</p></td>
<td><p>即時控制通訊協定 (RTCP) 統計資料的平均網路抖動。</p></td>
</tr>
<tr class="even">
<td><p>JitterInterArrivalMax</p></td>
<td><p>int</p></td>
<td><p>通話期間的最大網路抖動。</p></td>
</tr>
<tr class="odd">
<td><p>PacketLossRate</p></td>
<td><p>decimal(5,4)</p></td>
<td><p>通話期間的平均封包遺失率</p></td>
</tr>
<tr class="even">
<td><p>PacketLossRateMax</p></td>
<td><p>decimal(5,4)</p></td>
<td><p>通話期間監測所得的最大封包遺失率</p></td>
</tr>
<tr class="odd">
<td><p>BurstDensity</p></td>
<td><p>decimal(9,4)</p></td>
<td><p>通話期間封包遺失量激增時的封包遺失平均密度。</p></td>
</tr>
<tr class="even">
<td><p>BurstDuration</p></td>
<td><p>int</p></td>
<td><p>通話期間封包遺失量激增期的封包遺失平均持續時間。</p></td>
</tr>
<tr class="odd">
<td><p>BurstGapDensity</p></td>
<td><p>decimal(9,4)</p></td>
<td><p>封包遺失量激增期之間的間歇期封包遺失平均密度。</p></td>
</tr>
<tr class="even">
<td><p>BurstGapDuration</p></td>
<td><p>int</p></td>
<td><p>封包遺失量激增期之間的間歇期平均持續時間。</p></td>
</tr>
<tr class="odd">
<td><p>PacketUtilization</p></td>
<td><p>int</p></td>
<td><p>音訊資料流的封包計數。</p></td>
</tr>
<tr class="even">
<td><p>BandwidthEst</p></td>
<td><p>int</p></td>
<td><p>音訊資料流的頻寬預估值。</p></td>
</tr>
<tr class="odd">
<td><p>DegradationAvg</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>整個通話的網路 MOS 降低。範圍為 0.0 到 5.0。此計量顯示因為抖動及封包遺失而導致的網路 MOS 降低量。就可接受的品質而言，其應低於 0.5。</p></td>
</tr>
<tr class="even">
<td><p>DegradationMax</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>通話期間的最大網路 MOS 降低。</p></td>
</tr>
<tr class="odd">
<td><p>DegradationJitterAvg</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>抖動所導致的網路 MOS 降低。</p></td>
</tr>
<tr class="even">
<td><p>DegradationPacketLossAvg</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>封包遺失所導致的網路 MOS 降低。</p></td>
</tr>
<tr class="odd">
<td><p>PayloadDescription</p></td>
<td><p>int</p></td>
<td><p>通話的音訊轉碼器，參考來源：<a href="lync-server-2013-payloaddescription-table.md">Lync Server 2013 中的 PayloadDescription 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>AudioSampleRate</p></td>
<td><p>int</p></td>
<td><p>音訊資料流的取樣率。</p></td>
</tr>
<tr class="odd">
<td><p>CallerSendSignalLevel</p></td>
<td><p>int</p></td>
<td><p>發話者傳送之音訊的後類比增益控制音訊信號層級。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 30 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CallerRecvSignalLevel</p></td>
<td><p>int</p></td>
<td><p>發話者接收之音訊的音訊信號層級。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 30 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CallerSendNoiseLevel</p></td>
<td><p>int</p></td>
<td><p>發話者傳送之音訊的後類比增益控制音訊雜訊強度。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 35 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CallerRecvNoiseLevel</p></td>
<td><p>int</p></td>
<td><p>發話者接收之音訊的後類比增益控制音訊雜訊強度。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 35 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CallerEchoReturn</p></td>
<td><p>int</p></td>
<td><p>發話者的回音往返失真增強。這個計量單位是 dB。愈低的值代表較少的回音。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CallerSpeakerGlitchRate</p></td>
<td><p>int</p></td>
<td><p>每五分鐘發話者喇叭呈現平均故障數。為了達到優良的品質，此值應小於每五分鐘一次。非由 A/V 會議伺服器、中繼伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CallerMicGlitchRate</p></td>
<td><p>int</p></td>
<td><p>每五分鐘發話者麥克風擷取平均故障數。為了達到優良的品質，此值應小於每五分鐘一次。非由 A/V 會議伺服器、中繼伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CallerTimestampDriftRateMic</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>發話者的麥克風裝置時脈相對於 CPU 時脈的漂移率。</p></td>
</tr>
<tr class="odd">
<td><p>CallerTimestampDriftRateSpk</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>發話者的喇叭裝置時脈相對於 CPU 時脈的漂移率。</p></td>
</tr>
<tr class="even">
<td><p>CallerTimestampErrorMicMs</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>通話的最後 20 秒中，平均麥克風擷取資料流時間戳記錯誤 (毫秒)。</p></td>
</tr>
<tr class="odd">
<td><p>CallerTimestampErrorSpkMs</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>通話的最後 20 秒中，平均發話者的喇叭呈現資料流時間戳記錯誤 (毫秒)。</p></td>
</tr>
<tr class="even">
<td><p>CallerVsEntryCauses</p></td>
<td><p>smallint</p></td>
<td><p>語音切換是半雙工模式，具降低中斷功能。如需詳細資訊，請參閱 <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CallerEchoEventCauses</p></td>
<td><p>tinyint</p></td>
<td><p>發話者回音事件的原因。如需詳細資訊，請參閱 <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>CallerEchoPercentMicIn</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>發話者麥克風擷取資料流中偵測到的回音時間百分比。如果使用耳機，此值應該會較低。</p></td>
</tr>
<tr class="odd">
<td><p>CallerEchoPercentSend</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>發話者的傳送資料流中偵測到的回音時間百分比。傳送資料流中有高百分比的回音代表回音流失。</p></td>
</tr>
<tr class="even">
<td><p>CallerRxAGCSignalLevel</p></td>
<td><p>int</p></td>
<td><p>來自發話者音訊閘道的中繼伺服器上的接收信號層級；只適用於中繼伺服器。這個計量的單位是 dBoV。為了達到優良品質，可接受的範圍應該是 [-30 到 -18] dBoV。</p></td>
</tr>
<tr class="odd">
<td><p>CallerRxAGCNoiseLevel</p></td>
<td><p>int</p></td>
<td><p>來自發話者音訊閘道的中繼伺服器上的接收信號層級；這只適用於中繼伺服器。這個計量的單位是 dBoV。為了達到優良品質，可接受的範圍應該小於 -50 dBoV。</p></td>
</tr>
<tr class="even">
<td><p>CallerRxAGCGain</p></td>
<td><p>int</p></td>
<td><p>套用至發話者音訊之中繼伺服器端的自動增益控制 (AGC)。</p></td>
</tr>
<tr class="odd">
<td><p>CallerInitialSignalLevelRMS</p></td>
<td><p>float</p></td>
<td><p>最多通話前 30 秒，發話者接收的傳入訊號的平方根 (RMS)。</p></td>
</tr>
<tr class="even">
<td><p>CalleeSendSignalLevel</p></td>
<td><p>int</p></td>
<td><p>代表受話者傳送之音訊的後類比增益控制音訊信號層級。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 30 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRecvSignalLevel</p></td>
<td><p>int</p></td>
<td><p>受話者接收之音訊的音訊信號層級。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 30 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CalleeSendNoiseLevel</p></td>
<td><p>int</p></td>
<td><p>受話者傳送之音訊的後類比增益控制音訊雜訊強度。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 35 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRecvNoiseLevel</p></td>
<td><p>int</p></td>
<td><p>受話者接收之音訊的後類比增益控制音訊雜訊強度。這個計量單位是 dBmo。為了達到可接受的品質，至少應該有 35 dBmo。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CalleeEchoReturn</p></td>
<td><p>int</p></td>
<td><p>受話者的回音往返失真增強。這個計量單位是 dB。愈低的值代表較少的回音。此計量非由 A/V 會議伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeSpeakerGlitchRate</p></td>
<td><p>int</p></td>
<td><p>每五分鐘受話者喇叭呈現平均故障數。為了達到優良的品質，此值應小於每五分鐘一次。非由 A/V 會議伺服器、中繼伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="even">
<td><p>CalleeMicGlitchRate</p></td>
<td><p>int</p></td>
<td><p>每五分鐘受話者麥克風擷取平均故障數。為了達到優良的品質，此值應小於每五分鐘一次。非由 A/V 會議伺服器、中繼伺服器或 IP 電話所報告。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeTimestampDriftRateMic</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>受話者的麥克風裝置時脈相對於 CPU 時脈的漂移率。</p></td>
</tr>
<tr class="even">
<td><p>CalleeTimestampDriftRateSpk</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>受話者的喇叭裝置時脈相對於 CPU 時脈的漂移率。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeTimestampErrorMicMs</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>通話的最後 20 秒中，平均麥克風擷取資料流時間戳記錯誤 (毫秒)。</p></td>
</tr>
<tr class="even">
<td><p>CalleeTimestampErrorSpkMs</p></td>
<td><p>decimal(9,2)</p></td>
<td><p>通話的最後 20 秒中，平均受話者的喇叭呈現資料流時間戳記錯誤 (毫秒)。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeVsEntryCauses</p></td>
<td><p>smallint</p></td>
<td><p>語音切換是半雙工模式，具降低中斷功能。如需詳細資訊，請參閱 <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>CalleeEchoEventCauses</p></td>
<td><p>tinyint</p></td>
<td><p>受話者回音事件的原因。如需詳細資訊，請參閱 <a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeEchoPercentMicIn</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>受話者麥克風擷取資料流中偵測到的回音時間百分比。如果使用耳機，此值應該會較低。</p></td>
</tr>
<tr class="even">
<td><p>CalleeEchoPercentSend</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>受話者的傳送資料流中偵測到的回音時間百分比。傳送資料流中有高百分比的回音代表回音流失。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRxAGCSignalLevel</p></td>
<td><p>int</p></td>
<td><p>來自受話者音訊閘道的中繼伺服器上的接收信號層級；只適用於中繼伺服器。這個計量的單位是 dBoV。為了達到優良品質，可接受的範圍應該是 [-30 到 -18] dBoV。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRxAGCNoiseLevel</p></td>
<td><p>int</p></td>
<td><p>來自受話者音訊閘道的中繼伺服器上的接收信號層級；這只適用於中繼伺服器。這個計量的單位是 dBoV。為了達到優良品質，可接受的範圍應該小於 -50 dBoV。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRxAGCGain</p></td>
<td><p>int</p></td>
<td><p>套用至受話者音訊之中繼伺服器端的自動增益控制 (AGC)。</p></td>
</tr>
<tr class="even">
<td><p>CalleeInitialSignalLevelRMS</p></td>
<td><p>float</p></td>
<td><p>最多通話前 30 秒，受話者接收的傳入訊號的平方根 (RMS)。</p></td>
</tr>
<tr class="odd">
<td><p>RatioConcealedSamplesAvg</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>音訊修復所產生之隱藏樣本與一般樣本的平均比率。</p></td>
</tr>
<tr class="even">
<td><p>RatioStretchedSamplesAvg</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>音訊修復所產生之延伸樣本與一般樣本的平均比率。</p></td>
</tr>
<tr class="odd">
<td><p>RatioCompressedSamplesAvg</p></td>
<td><p>decimal(5,2)</p></td>
<td><p>音訊修復所產生之壓縮樣本與一般樣本的平均比率。</p></td>
</tr>
<tr class="even">
<td><p>RoundTrip</p></td>
<td><p>int</p></td>
<td><p>RTCP 統計資料中的來回時間。</p></td>
</tr>
<tr class="odd">
<td><p>RoundTripMax</p></td>
<td><p>int</p></td>
<td><p>音訊資料流的最大來回時間。</p></td>
</tr>
<tr class="even">
<td><p>OverallAvgNetworkMOS</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>通話的平均寬頻網路 MOS。此計量取決於封包遺失、抖動及所使用的轉碼器。範圍為 1.0 到 5.0。</p></td>
</tr>
<tr class="odd">
<td><p>OverallMinNetworkMOS</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>通話的最小寬頻網路 MOS。</p></td>
</tr>
<tr class="even">
<td><p>SendListenMOS</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>所傳送之音訊的平均預測寬頻傾聽 MOS 分數，包括語音層級、雜訊層級和擷取裝置特性。</p></td>
</tr>
<tr class="odd">
<td><p>SendListenMOSMin</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>通話的最小 SendListenMOS。</p></td>
</tr>
<tr class="even">
<td><p>RecvListenMOS</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>從網路接收之音訊的平均預測寬頻傾聽 MOS 分數，包括語音層級、雜訊層級、轉碼器、網路狀況和擷取裝置特性。</p></td>
</tr>
<tr class="odd">
<td><p>RecvListenMOSMin</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>通話的最小 RecvListenMOS。</p></td>
</tr>
<tr class="even">
<td><p>AudioFECUsed</p></td>
<td><p>bit</p></td>
<td><p>指出是否將音訊 FEC 用於通話。</p></td>
</tr>
<tr class="odd">
<td><p>SenderIsCallerPAI</p></td>
<td><p>bit</p></td>
<td><p>指出 P-Asserted Identity 資訊的方向；1 表示資料流方向從發話者到受話者；0 表示資料流方向從受話者到發話者。</p></td>
</tr>
</tbody>
</table>


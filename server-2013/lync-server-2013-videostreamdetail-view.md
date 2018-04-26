---
title: VideoStreamDetail 檢視
TOCTitle: VideoStreamDetail 檢視
ms:assetid: ec8c45e1-307d-40ec-a75e-6083306105f2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721928(v=OCS.15)
ms:contentKeyID: 49890376
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# VideoStreamDetail 檢視

 

_**上次修改主題的時間：** 2015-03-09_

VideoStreamDetail 檢視存放資料庫中各視訊串流的相關資訊。此檢視在 Microsoft Lync Server 2013 中介紹過。


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
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SessionTime</p></td>
<td><p>日期時間</p></td>
<td><p>參考來源：<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>SessionSeq</p></td>
<td><p>int</p></td>
<td><p>參考來源：<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>MediaLineLabel</p></td>
<td><p>tinyint</p></td>
<td><p>參考來源：<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p>StreamId</p></td>
<td><p>int</p></td>
<td><p>媒體行中的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>StartTime</p></td>
<td><p>日期時間</p></td>
<td><p>工作階段的開始時間。</p></td>
</tr>
<tr class="even">
<td><p>EndTime</p></td>
<td><p>日期時間</p></td>
<td><p>工作階段的結束時間。</p></td>
</tr>
<tr class="odd">
<td><p>CallPriority</p></td>
<td><p>int</p></td>
<td><p>通話優先順序。</p></td>
</tr>
<tr class="even">
<td><p>CallerPool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者集區 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p>CalleePool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者集區 FQDN。</p></td>
</tr>
<tr class="even">
<td><p>發話者</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>發話者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p>受話者</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>受話者的 URI。</p></td>
</tr>
<tr class="even">
<td><p>CallerUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>發話者的使用者代理程式字串。</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>發話者的使用者代理程式類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>CallerUserAgentCategory</p></td>
<td><p>nvarchar(64)</p></td>
<td><p>發話者的使用者代理程式類別。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>受話者的使用者代理程式字串。</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>受話者的使用者代理程式類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserAgentCategory</p></td>
<td><p>nvarchar(64)</p></td>
<td><p>受話者的使用者代理程式類別。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a>＞。</p></td>
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
<td><p>發話者端點的 CPU 核心名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCPUNumberOfCores</p></td>
<td><p>smallint</p></td>
<td><p>受話者端點的 CPU 核心數量。</p></td>
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
<td><p>顯示發話者的系統是否在虛擬環境中執行。如需詳細資訊，請參閱＜<a href="lync-server-2013-endpoint-table.md">Lync Server 2013 中的 Endpoint 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeVirtualizationFlag</p></td>
<td><p>tinyint</p></td>
<td><p>顯示受話者的系統是否在虛擬環境中執行。如需詳細資訊，請參閱＜<a href="lync-server-2013-endpoint-table.md">Lync Server 2013 中的 Endpoint 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>ConnectivityIce</p></td>
<td><p>tinyint</p></td>
<td><p>媒體路徑的相關資訊，例如直接或轉送。如需詳細資訊，請參閱＜<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CallerIceWarningFlags</p></td>
<td><p>int</p></td>
<td><p>發話者適用的位元旗標所描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞。</p></td>
</tr>
<tr class="even">
<td><p>CalleeIceWarningFlags</p></td>
<td><p>int</p></td>
<td><p>受話者適用的位元旗標所描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞。</p></td>
</tr>
<tr class="odd">
<td><p>傳輸</p></td>
<td><p>int</p></td>
<td><p>傳輸類型：0 是 UDP，1 是 TCP。</p></td>
</tr>
<tr class="even">
<td><p>CallerIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者的 IP 位址。可能為 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p>CallerPort</p></td>
<td><p>int</p></td>
<td><p>發話者使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CallerInside</p></td>
<td><p>bit</p></td>
<td><p>顯示發話者是否來自公司網路內部。1 代表企業網路內的發話者，0 代表網路外的發話者。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>受話者的 IP 位址。可能為 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="even">
<td><p>CalleePort</p></td>
<td><p>int</p></td>
<td><p>受話者使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeInside</p></td>
<td><p>bit</p></td>
<td><p>顯示受話者是否來自公司網路內部。1 代表企業網路內的受話者，0 代表網路外的受話者。</p></td>
</tr>
<tr class="even">
<td><p>CallerUserSite</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>發話者的網站名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerRegion</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>發話者網站的國家/區域名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserSite</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>受話者的網站名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRegion</p></td>
<td><p>nvarchar(128)</p></td>
<td><p>受話者網站的國家/區域名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerRelayIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者使用的 A/V Edge Service IP 位址。如需詳細資訊，請參閱＜<a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CallerRelayPort</p></td>
<td><p>int</p></td>
<td><p>發話者使用的 A/V Edge Service 連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRelayIPAddr</p></td>
<td><p>var(50)</p>
<p></p></td>
<td><p>受話者使用的 A/V Edge Service IP 位址格式碼。如需詳細資訊，請參閱＜<a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRelayPort</p></td>
<td><p>int</p></td>
<td><p>受話者使用的 A/V Edge Service 連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CallerCaptureDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的擷取裝置名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerRenderDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的轉換裝置名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerCaptureDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的擷取裝置驅動程式名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerRenderDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的轉換裝置驅動程式名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleeCaptureDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的擷取裝置名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRenderDev</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的轉換裝置名稱。</p></td>
</tr>
<tr class="even">
<td><p>CalleCaptureDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的擷取裝置驅動程式名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRenderDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的轉換裝置驅動程式名稱。</p></td>
</tr>
<tr class="even">
<td><p>CallerNetworkConnectionType</p></td>
<td><p>tinyint</p></td>
<td><p>發話者的網路連線類型：0 是有線，1 是無線。</p></td>
</tr>
<tr class="odd">
<td><p>CallerVPN</p></td>
<td><p>bit</p></td>
<td><p>顯示發話者是否連接到虛擬私人網路。1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="even">
<td><p>CallerLinkSpeed</p></td>
<td><p>decimal(18,)</p></td>
<td><p>發話者端點的網路連結速度，以 bps 為單位。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeNetworkConnectionType</p></td>
<td><p>tinyint</p></td>
<td><p>受話者的網路連線類型：0 是有線，1 是無線。</p></td>
</tr>
<tr class="even">
<td><p>CalleeVPN</p></td>
<td><p>bit</p></td>
<td><p>顯示受話者是否連接到虛擬私人網路。1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeLinkSpeed</p></td>
<td><p>decimal(18.0)</p></td>
<td><p>受話者端點的網路連結速度 (以 bps 為單位)。</p></td>
</tr>
<tr class="even">
<td><p>ConversationalMOS</p></td>
<td><p>decimal(3.2)</p></td>
<td><p>音訊工作階段的窄頻交談方式 MOS (兩種音訊資料流皆為依據)。</p></td>
</tr>
<tr class="odd">
<td><p>AppliedBandwidthLimit</p></td>
<td><p>int</p></td>
<td><p>在指定各種原則設定 (TURN、API、SDP、Policy Server 等等) 的情況下，套用至指定傳送端資料流的實際頻寬。不要將這個與有效頻寬混淆，因為根據頻寬預估值，會有較低的有效頻寬。基本上，除了頻寬預估值規定的限制以外，這是傳送端資料流所能取得的最大頻寬。</p></td>
</tr>
<tr class="even">
<td><p>JitterInterArrival</p></td>
<td><p>int</p></td>
<td><p>即時控制通訊協定 (RTCP) 統計資料的平均網路抖動。</p></td>
</tr>
<tr class="odd">
<td><p>JitterInterArrivalMax</p></td>
<td><p>int</p></td>
<td><p>通話期間的最大網路抖動。</p></td>
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
<td><p>PacketLossRate</p></td>
<td><p>decimal(5.4)</p></td>
<td><p>通話期間的平均封包遺失率</p></td>
</tr>
<tr class="odd">
<td><p>PacketLossRateMax</p></td>
<td><p>decimal(5.4)</p></td>
<td><p>通話期間監測所得的最大封包遺失率</p></td>
</tr>
<tr class="even">
<td><p>PacketUtilization</p></td>
<td><p>int</p></td>
<td><p>視訊資料流的封包計數 (即時傳輸控制通訊協定 (RTP))。</p></td>
</tr>
<tr class="odd">
<td><p>BandwidthEst</p></td>
<td><p>int</p></td>
<td><p>音訊資料流的頻寬預估值。</p></td>
</tr>
<tr class="even">
<td><p>PayloadDescription</p></td>
<td><p>int</p></td>
<td><p>通話使用的音訊轉碼器，參考來源為 <a href="lync-server-2013-payloaddescription-table.md">Lync Server 2013 中的 PayloadDescription 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p>VideoResolution</p></td>
<td><p>char(9)</p></td>
<td><p>視訊的解析度 (像素寬度乘以像素高度)。報告成字串。</p></td>
</tr>
<tr class="even">
<td><p>VideoBitRateAvg</p></td>
<td><p>int</p></td>
<td><p>視訊資料流的平均位元速率。</p></td>
</tr>
<tr class="odd">
<td><p>InboundVideoFrameRateAvg</p></td>
<td><p>decimal(9.4)</p></td>
<td><p>已接收視訊的畫面播放速率。</p></td>
</tr>
<tr class="even">
<td><p>OutboundVideoFrameRateAvg</p></td>
<td><p>decimal(9.4)</p></td>
<td><p>已傳送視訊的畫面播放速率。</p></td>
</tr>
<tr class="odd">
<td><p>ViideoBitRateMax</p></td>
<td><p>int</p></td>
<td><p>視訊工作階段期間的最大視訊位元速率。</p></td>
</tr>
<tr class="even">
<td><p>VideoPacketLossRate</p></td>
<td><p>decimal(9.4)</p></td>
<td><p>視訊封包丟失的速率。</p></td>
</tr>
<tr class="odd">
<td><p>VideoFrameLossRate</p></td>
<td><p>decimal(9.4)</p></td>
<td><p>總丟失視訊畫面的百分比。</p></td>
</tr>
<tr class="even">
<td><p>VideoFEC</p></td>
<td><p>bit</p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="odd">
<td><p>VideoAllocateBWAvg</p></td>
<td><p>int</p></td>
<td><p>配置到視訊的平均頻寬量。</p></td>
</tr>
<tr class="even">
<td><p>VideoLocalFrameLossPercentageAvg</p></td>
<td><p>decimal(9.4)</p></td>
<td><p>總丟失視訊畫面的百分比。</p></td>
</tr>
<tr class="odd">
<td><p>SenderIsCallerPAI</p></td>
<td><p>bit</p></td>
<td><p>p-asserted 識別資訊的串流方向。1 代表串流方向為發話者到受話者；0 代表串流方向為受話者到發話者。</p></td>
</tr>
</tbody>
</table>


---
title: Lync Server 2013：QoE 表格清單
TOCTitle: QoE 表格清單
ms:assetid: 176194d7-d184-4e23-94bb-cb62b4db47f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398236(v=OCS.15)
ms:contentKeyID: 49290212
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 QoE 表格清單

 

_**上次修改主題的時間：** 2015-03-09_

資料庫結構描述由下列表格所組成。

**支援的表格**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>表格</strong></th>
<th><strong>描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-appsharingmetricsthreshold-table.md">AppSharingMetricsThreshold 表</a></p></td>
<td><p>針對用於應用程式共用的經驗品質計量，儲存最佳且可接受的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-codecdescription-table.md">CodecDescription 表</a></p></td>
<td><p>將唯一轉碼器識別碼對應至其相對應的轉碼器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a></p></td>
<td><p>將 IP 位址對應至用在經驗品質資料庫其他地方的唯一 IP 位址識別碼。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-networkconnectiondetail-table.md">Lync Server 2013 中的 NetworkConnectionDetail 表</a></p></td>
<td><p>將網路連線類型對應至用在經驗品質資料庫其他地方的網路連線識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-purgesettings-table-qoe.md">PurgeSettings 表 (QoE)</a></p></td>
<td><p>儲存指定是否 (何時) 要從 QoE 資料庫中自動刪除過期經驗品質記錄的資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-traceroute-table.md">TraceRoute 表</a></p></td>
<td><p>儲存通話的路由資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-useragentdef-table-qoe.md">UserAgentDef 資料表 (QoE)</a></p></td>
<td><p>將使用者代理程式識別碼對應至代理程式的描述性名稱。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-videometricsthreshold-table.md">VideoMetricsThreshold 表</a></p></td>
<td><p>針對用於視訊通話的經驗品質計量，儲存最佳且可接受的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a></p></td>
<td><p>儲存音訊和視訊工作階段中所用的工作階段初始通訊協定 (SIP) 使用者代理程式 (UA) 字串與 UA 類型。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-user-table.md">Lync Server 2013 中的 User 表格</a></p></td>
<td><p>儲存音訊和視訊工作階段中所用的使用者、會議以及電話 URI。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-endpoint-table.md">Lync Server 2013 中的 Endpoint 表格</a></p></td>
<td><p>儲存參與音訊和視訊工作階段之端點的 FQDN 電腦名稱。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-pool-table.md">Lync Server 2013 中的 Pool 表格</a></p></td>
<td><p>儲存計量資料所屬之集區的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-device-table.md">Lync Server 2013 中的 Device 表格</a></p></td>
<td><p>儲存音訊/視訊通話中所用的擷取裝置和轉換裝置。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-devicedriver-table.md">Lync Server 2013 中的 DeviceDriver 表格</a></p></td>
<td><p>儲存音訊/視訊通話中所用的擷取裝置和轉換裝置驅動程式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-conference-table.md">Lync Server 2013 中的 Conference 表格</a></p></td>
<td><p>儲存會議案例的會議 URI 或是其他案例的 DialogID。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-sessioncorrelation-table.md">Lync Server 2013 中的 SessionCorrelation 表格</a></p></td>
<td><p>儲存 PSTN 通話的 CorrelationID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-payloaddescription-table.md">Lync Server 2013 中的 PayloadDescription 表格</a></p></td>
<td><p>儲存音訊/視訊通話中所用的轉碼器。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-appliedbandwidthsource-table.md">Lync Server 2013 中的 AppliedBandwidthSource 表格</a></p></td>
<td><p>儲存音訊/視訊通話中所用的頻寬來源。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-macaddress-table.md">Lync Server 2013 中的 MacAddress 表格</a></p></td>
<td><p>儲存參與音訊和視訊工作階段之端點的 MAC 位址。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-dialog-table.md">Lync Server 2013 中的 Dialog 表格</a></p></td>
<td><p>儲存音訊和視訊工作階段的對話方塊 ID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-region-table.md">Lync Server 2013 中的地區表格</a></p></td>
<td><p>儲存 NCS 設定中所定義的網路地區。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-usersite-table.md">Lync Server 2013 中的 UserSite 表格</a></p></td>
<td><p>儲存 NCS 設定中所定義的網站。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-subnet-table.md">Lync Server 2013 中的 Subnet 表格</a></p></td>
<td><p>儲存 NCS 設定中所定義的子網路。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-monitoredregionlink-table.md">Lync Server 2013 中的 MonitoredRegionLink 表格</a></p></td>
<td><p>儲存 NCS 設定中所定義的區域連結。</p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoredusersitelink-table.md">MonitoredUserSiteLink 表格</a></p></td>
<td><p>儲存 NCS 設定中所定義的網站連結。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-endpointsubnet-table.md">Lync Server 2013 中的 EndpointSubnet 表格</a></p></td>
<td><p>儲存參與音訊和視訊工作階段之端點的子網路。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-server-table.md">Lync Server 2013 中的 Server 表格</a></p></td>
<td><p>儲存媒體通過之伺服器的 FQDN 或 IP 位址。</p></td>
</tr>
</tbody>
</table>


**計量資料表格**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>表格</strong></th>
<th><strong>描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-appsharingstream-table.md">AppSharingStream 表</a></p></td>
<td><p>儲存用於應用程式共用之網路串流的經驗品質計量。用於應用程式共用之網路串流的經驗品質計量。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-session-table.md">Lync Server 2013 中的 Session 表格</a></p></td>
<td><p>儲存音訊或音訊/視訊工作階段的整體資訊。工作階段定義為兩個端點之間的音訊或視訊 SIP 對話。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a></p></td>
<td><p>儲存工作階段中每個媒體行的相關資訊。媒體行為一或多個音訊及視訊資料流的集合。一般來說，單一媒體行會有兩個音訊或視訊資料流。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-audiostream-table.md">Lync Server 2013 中的 AudioStream 表格</a></p></td>
<td><p>儲存媒體行中每個音訊資料流的音訊媒體品質計量。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-audiosignal-table.md">Lync Server 2013 中的 AudioSignal 表格</a></p></td>
<td><p>儲存媒體行中音訊媒體品質計量。這包括柔和式迴音效果取消 (AEC) 以及自動增益控制 (AGC) 計量。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-videostream-table.md">Lync Server 2013 中的 VideoStream 表格</a></p></td>
<td><p>儲存媒體行中每個音訊資料流的視訊媒體品質計量。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-audioclientevent-table.md">Lync Server 2013 中的 AudioClientEvent 表格</a></p></td>
<td><p>儲存從用戶端事件收集到的音訊媒體品質計量。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-videoclientevent-table.md">Lync Server 2013 中的 VideoClientEvent 表格</a></p></td>
<td><p>儲存從用戶端事件收集到的視訊媒體品質計量。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DiagnosticData 表格</strong></p></td>
<td><p>儲存僅限內部使用的診斷資料。</p></td>
</tr>
</tbody>
</table>


**摘要資料表格**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>表格</strong></th>
<th><strong>描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ServerSummary 表格</strong></p></td>
<td><p>儲存伺服器的摘要資料，這些資料僅用於經驗品質 (QoE) 報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserSummary 表格</strong></p></td>
<td><p>儲存使用者的摘要資料，這些資料僅用於經驗品質 (QoE) 報告。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallTypeSummary 表格</strong></p></td>
<td><p>儲存通話類型的摘要資料，這些資料僅用於經驗品質 (QoE) 報告。</p></td>
</tr>
</tbody>
</table>


**監控伺服器所用的內部使用表格**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>表格</strong></th>
<th><strong>描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DbConfigDateTime</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>DbConfigInt</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FrontEnd 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>Task 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SummaryTableConfiguration</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>DbErrorMessage</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MetricsThreshold</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>DaylightSavingYears</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TimeZoneConfiguration</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>TimeZones</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallSummary 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceCallSumary 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tenant 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoCallSummaryTable</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ASCallSummaryTable</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
</tbody>
</table>


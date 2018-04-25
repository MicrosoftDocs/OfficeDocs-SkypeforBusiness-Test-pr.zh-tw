---
title: Lync Server 2013：MediaLine 表格
TOCTitle: MediaLine 表格
ms:assetid: 414b1d63-ae97-4c27-bac0-c9ad0f808ff0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425920(v=OCS.15)
ms:contentKeyID: 49290719
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 MediaLine 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表一個媒體行。(一個音訊工作階段通常包含一個音訊媒體行。一個音訊和視訊 (A/V) 工作階段通常包含一個音訊媒體行和一個視訊媒體行，不過如果使用會議裝置或使用圖庫檢視，也可能包含兩個視訊媒體行。)


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
<td><p>參考來源： <a href="lync-server-2013-session-table.md">Lync Server 2013 中的 Session 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>參考來源： <a href="lync-server-2013-session-table.md">Lync Server 2013 中的 Session 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要</p></td>
<td><p>0 是主要音訊，1 是主要視訊，而 2 是全景視訊，3 是應用程式/桌面共用。這必須是單一工作階段中的唯一標籤。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConnectivityIce</strong></p></td>
<td><p>Tinyint</p></td>
<td><p> </p></td>
<td><p>此欄已出現，但未在 Microsoft Lync Server 2013 中使用。CallerConnectivityICE 和 CalleeConnectivityICE 兩欄已擷取了使用於媒體行的連線資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerIceWarningFlags</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>位元旗標中描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞ (可供下載)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeIceWarningFlags</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>與 CallerIceWarningFlags 相同，但是在受話方。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞ (可供下載)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Security</strong></p></td>
<td><p>Tinyint</p></td>
<td><p> </p></td>
<td><p>使用中的安全性設定檔。0 是無 (NONE)，1 是 SRTP，2 是 V1。</p></td>
</tr>
<tr class="even">
<td><p><strong>傳輸</strong></p></td>
<td><p>Tinyint</p></td>
<td><p> </p></td>
<td><p>0 是 UDP，1 是 TCP。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的 IP 位址。如需詳細資訊，請參閱＜ <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerPort</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>發話者使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerSubnet</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的子網路。如需詳細資訊，請參閱＜ <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>\ <strong>CallerInside</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 代表企業網路內的發話者，0 代表網路外的發話者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerMacAddress</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者的 MAC 位址，參考來源： <a href="lync-server-2013-macaddress-table.md">Lync Server 2013 中的 MacAddress 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerRelayIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者使用之 Lync Server A/V Edge Service 的 IP 位址。如需詳細資訊，請參閱＜ <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerRelayPort</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>發話者在 A/V Edge Service 上使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerCaptureDev</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者使用的擷取裝置。參考來源： <a href="lync-server-2013-device-table.md">Lync Server 2013 中的 Device 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerRenderDev</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者使用的轉換裝置。參考來源： <a href="lync-server-2013-device-table.md">Lync Server 2013 中的 Device 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerCaptureDevDriver</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者擷取裝置的驅動程式，參考來源： <a href="lync-server-2013-devicedriver-table.md">Lync Server 2013 中的 DeviceDriver 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerRenderDevDriver</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>發話者轉換裝置的驅動程式，參考來源： <a href="lync-server-2013-devicedriver-table.md">Lync Server 2013 中的 DeviceDriver 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerNetworkConnectionType</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>外部</p></td>
<td><p>指出發話者連線至網路的方式。值可透過 <a href="lync-server-2013-networkconnectiondetail-table.md">Lync Server 2013 中的 NetworkConnectionDetail 表</a>取得。值通常為 0 (代表有線連線)、1 (代表 WiFi 連線) 或 3 (代表乙太網路連線)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerBssid</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用無線時，這是發話者的 BSSID。參考來源： <a href="lync-server-2013-macaddress-table.md">Lync Server 2013 中的 MacAddress 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerVPN</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>發話者的連結。1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerLinkSpeed</strong></p></td>
<td><p>decimal(18.0)</p></td>
<td><p></p></td>
<td><p>發話者端點的網路連結速度 (bps)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者的 IP 位址。如需詳細資訊，請參閱＜ <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleePort</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>受話者使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeSubnet</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者的子網路。如需詳細資訊，請參閱＜ <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeInside</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 代表企業網路內的受話者，0 代表網路外的受話者。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeMacAddress</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者的 MAC 位址。參考來源： <a href="lync-server-2013-macaddress-table.md">Lync Server 2013 中的 MacAddress 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeRelayIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者使用之 A/V Edge Service 的 IP 位址。如需詳細資訊，請參閱＜ <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeRelayPort</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>受話者在 A/V Edge Service 上使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeCaptureDev</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者使用的擷取裝置。參考來源： <a href="lync-server-2013-device-table.md">Lync Server 2013 中的 Device 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeRenderDev</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者使用的轉換裝置。參考來源： <a href="lync-server-2013-device-table.md">Lync Server 2013 中的 Device 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeCaptureDevDriver</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>受話者擷取裝置的驅動程式。參考來源： <a href="lync-server-2013-devicedriver-table.md">Lync Server 2013 中的 DeviceDriver 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeRenderDevDriver</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>外部</p></td>
<td><p>受話者轉換裝置的驅動程式。參考來源： <a href="lync-server-2013-devicedriver-table.md">Lync Server 2013 中的 DeviceDriver 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeNetworkConnectionType</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>外部</p></td>
<td><p>指出受話者連線至網路的方式。值可透過 <a href="lync-server-2013-networkconnectiondetail-table.md">Lync Server 2013 中的 NetworkConnectionDetail 表</a>取得。值通常為 0 (代表有線連線)、1 (代表 WiFi 連線) 或 3 (代表乙太網路連線)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeBssid</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用無線時，這是受話者的 BSSID。參考來源： <a href="lync-server-2013-macaddress-table.md">Lync Server 2013 中的 MacAddress 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeVPN</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>受話者的連結；1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeLinkSpeed</strong></p></td>
<td><p>decimal(18.0)</p></td>
<td><p> </p></td>
<td><p>受話者端點的網路連結速度 (bps)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConversationalMOS</strong></p></td>
<td><p>decimal(3.2)</p></td>
<td><p> </p></td>
<td><p>音訊工作階段的窄頻交談方式 MOS (兩種音訊資料流皆為依據)。</p></td>
</tr>
<tr class="even">
<td><p><strong>AppliedBandwidthLimit</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>這是在指定各種原則設定 (TURN、API、SDP、Policy Server 等等) 的情況下，套用至指定傳送端資料流的實際頻寬。不要將這個與有效頻寬混淆，因為根據頻寬預估值，會有較低的有效頻寬。基本上，除了頻寬預估值規定的限制以外，這是傳送端資料流所能取得的最大頻寬。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AppliedBandwidthSourceKey</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>這是所規定的頻寬上限來源。其說明頻寬限制來自哪裡 (「Policy Server」、「TURN Server」、「Modality」 等等)。參考來源： <a href="lync-server-2013-appliedbandwidthsource-table.md">Lync Server 2013 中的 AppliedBandwidthSource 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>發話者</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>指出是否收到發話者的計量；1 為是，Null 值為否。</p></td>
</tr>
<tr class="odd">
<td><p><strong>受話者</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>指出是否收到受話者的計量；1 為是，Null 值為否。</p></td>
</tr>
<tr class="even">
<td><p><strong>MidCallReport</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>指出此報告是否屬於此工作階段的一部分或是完整的工作階段。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClassifiedPoorCall</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>指出是否將通話歸類為通話不良 (數值 1) 或良好通話 (0)。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerConnectivityICE</strong></p></td>
<td><p>tinyint</p></td>
<td><p></p></td>
<td><p>指出發話者是否使用 ICE 通訊協定 (網際網路連線建立) 連線至網路。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeConnectivityICE</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>指出發話者是否使用 ICE 通訊協定 (網際網路連線建立) 連線至網路。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerReflexiveLocalIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>撥打電話之使用者的自反 IP 位址。在使用 NAT (網路位址轉譯) 的組織中，自反 IP 位址為 Proxy 伺服器的 IP 位址。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerWiFiDriverDevicesDesc</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>撥打電話之使用者採用的 WiFi 驅動程式裝置描述。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerWiFiDriverVersion</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>撥打電話之使用者採用的 WiFi 驅動程式版本號碼。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleReflexiveLocalIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>接聽電話之使用者的自反 IP 位址。在使用 NAT (網路位址轉譯) 的組織中，自反 IP 位址為 Proxy 伺服器的 IP 位址。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeWiFiDriverDevicesDesc</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>接聽電話之使用者採用的 WiFi 驅動程式裝置描述。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeWiFiDriverVersion</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>接聽電話之使用者採用的 WiFi 驅動程式版本號碼。</p>
<p>Microsoft Lync Server 2013 中已採用此欄。</p></td>
</tr>
</tbody>
</table>


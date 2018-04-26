---
title: MediaLine 檢視
TOCTitle: MediaLine 檢視
ms:assetid: 132eca13-8913-4218-9eff-4960ced8c3dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687972(v=OCS.15)
ms:contentKeyID: 49889947
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# MediaLine 檢視

 

_**上次修改主題的時間：** 2015-03-09_

媒體行檢視會儲存資料庫中每一媒體行的相關資訊。一個音訊工作階段通常會包含一個音訊媒體行。一個音訊和視訊 (A/V) 工作階段通常會包含一個音訊媒體行和一個視訊媒體行；不過，如果使用會議裝置或圖庫檢視，工作階段可能會包含兩個視訊媒體行。Microsoft Lync Server 2013 中即引入了此檢視。


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
<td><p>ConferenceDateTime</p></td>
<td><p>datetime</p></td>
<td><p>參考來源：＜<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>SessionSeq</p></td>
<td><p>int</p></td>
<td><p>參考來源：＜<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>MediaLineLabel</p></td>
<td><p>tinyint</p></td>
<td><p>參考來源：＜<a href="lync-server-2013-medialine-table.md">Lync Server 2013 中的 MediaLine 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>CallerIceWarningFlags</p></td>
<td><p>int</p></td>
<td><p>發話者位元旗標中描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeIceWarningFlags</p></td>
<td><p>int</p></td>
<td><p>受話者位元旗標中描述之互動式連線建立 (ICE) 程序的相關資訊。如需詳細資訊，請參閱＜經驗品質監控伺服器通訊協定規格＞。</p></td>
</tr>
<tr class="even">
<td><p>安全性</p></td>
<td><p>tinyint</p></td>
<td><p>使用中的安全性設定檔。0 是無 (NONE)，1 是 SRTP，2 是 V1。</p></td>
</tr>
<tr class="odd">
<td><p>傳輸</p></td>
<td><p>tinyint</p></td>
<td><p>傳輸類型。0 是 UDP，1 是 TCP。</p></td>
</tr>
<tr class="even">
<td><p>CallerIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者的 IP 位址，可以是 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p>CallerPort</p></td>
<td><p>int</p></td>
<td><p>發話者使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CallerInside</p></td>
<td><p>bit</p></td>
<td><p>指出發話者是否在組織網路內。1 代表發話者在企業網路內。0 代表發話者在網路外。</p></td>
</tr>
<tr class="odd">
<td><p>CallerMacAddress</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者使用之網路介面的 MAC 位址。</p></td>
</tr>
<tr class="even">
<td><p>CallerRelayIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者使用之 A/V Edge Service 的 IP 位址。如需詳細資訊，請參閱＜<a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRelayPort</p></td>
<td><p>int</p></td>
<td><p>發話者在 A/V Edge Service 上使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CallerReflexiveIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>發話者的 IP 位址，如 A/V Edge Service 所報告。例如，如果用戶端位在 NAT 後面，此位址可能會不同於 CallerIPAddr。</p></td>
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
<td><p>CallerRenderDevDriver</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的轉換裝置驅動程式名稱。</p></td>
</tr>
<tr class="odd">
<td><p>CallerWifiDriverDeviceDesc</p></td>
<td><p>varchar(256</p></td>
<td><p>發話者的 Wifi 驅動程式說明。</p></td>
</tr>
<tr class="even">
<td><p>CallerWifiDriverVersion</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者的 Wifi 驅動程式版本。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeNetworkConnectionDetail</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者網路連線的詳細資料。如需詳細資訊，請參閱＜<a href="lync-server-2013-networkconnectiondetail-table.md">Lync Server 2013 中的 NetworkConnectionDetail 表</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>CallerBssid</p></td>
<td><p>varchar(256)</p></td>
<td><p>發話者 WiFi 連線所使用的基本服務組識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>CallerVPN</p></td>
<td><p>bit</p></td>
<td><p>指出發話者是否透過虛擬私人網路來連線。1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="even">
<td><p>CalleeIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>受話者的 IP 位址，可以是 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p>CalleePort</p></td>
<td><p>int</p></td>
<td><p>受話者使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CalleeInside</p></td>
<td><p>bit</p></td>
<td><p>指出受話者是否在企業網路內。1 代表受話者在企業網路內，0 代表受話者在網路外。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeMacAddress</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者使用之網路介面的 MAC 位址。</p></td>
</tr>
<tr class="even">
<td><p>CalleeRelayIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>受話者使用之 A/V Edge Service 的 IP 位址。如需詳細資訊，請參閱＜<a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeRelayPort</p></td>
<td><p>int</p></td>
<td><p>受話者在 A/V Edge Service 上使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p>CalleeReflexiveIPAddr</p></td>
<td><p>var(50)</p></td>
<td><p>受話者的 IP 位址，如 A/V Edge Service 所報告。例如，如果用戶端位在 NAT 後面，此位址可能會不同於 CalleeIPAddr。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeCaptureDev</p></td>
<td><p>var(50)</p></td>
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
<td><p>CalleeWifiDriverDeviceDesc</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者的 Wifi 驅動程式說明。</p></td>
</tr>
<tr class="even">
<td><p>CalleeWifiDriverVersion</p></td>
<td><p>varchar(256</p></td>
<td><p>受話者的 Wifi 驅動程式版本。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeNetworkConnectionDetail</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者網路連線的詳細資料。如需詳細資訊，請參閱＜<a href="lync-server-2013-networkconnectiondetail-table.md">Lync Server 2013 中的 NetworkConnectionDetail 表</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>CalleeBssid</p></td>
<td><p>varchar(256)</p></td>
<td><p>受話者 WiFi 連線所使用的基本服務組識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>CalleeVPN</p></td>
<td><p>bit</p></td>
<td><p>指出受話者是否透過虛擬私人網路來連線。1 是虛擬私人網路 (VPN)，0 是非 VPN。</p></td>
</tr>
<tr class="even">
<td><p>ConversationalMOS</p></td>
<td><p>decimal(3,2)</p></td>
<td><p>音訊工作階段的窄頻交談方式 MOS (兩種音訊資料流皆為依據)。</p></td>
</tr>
<tr class="odd">
<td><p>AppliedBandwidthLimit</p></td>
<td><p>int</p></td>
<td><p>這是在指定各種原則設定 (TURN、API、SDP、Policy Server 等等) 的情況下，套用至指定傳送端資料流的實際頻寬。不要將這個與有效頻寬混淆，因為根據頻寬預估值，會有較低的有效頻寬。基本上，除了頻寬預估值規定的限制以外，這是傳送端資料流所能取得的最大頻寬。</p></td>
</tr>
<tr class="even">
<td><p>AppliedBandwidthSource</p></td>
<td><p>varchar(256)</p></td>
<td><p>所採用的頻寬容量來源。其會說明頻寬限制的來源 (例如，「原則伺服器」、「TURN 伺服器」或「形式」)。</p></td>
</tr>
<tr class="odd">
<td><p>發話者</p></td>
<td><p>bit</p></td>
<td><p>指出是否收到發話者的計量；1 為是，0 為否。</p></td>
</tr>
<tr class="even">
<td><p>受話者</p></td>
<td><p>bit</p></td>
<td><p>指出是否收到受話者的計量；1 為是，0 為否。</p></td>
</tr>
<tr class="odd">
<td><p>MidCallReport</p></td>
<td><p>bit</p></td>
<td><p>指出此報告適用於部分通話或完整通話。</p></td>
</tr>
<tr class="even">
<td><p>ClassifiedPoorCall</p></td>
<td><p>bit</p></td>
<td><p>指出通話分類為通話不良 (1) 或通話良好 (0)。</p></td>
</tr>
<tr class="odd">
<td><p>CallerConnectivityICE</p></td>
<td><p>tinyint</p></td>
<td><p>指出發話者是否使用 ICE 通訊協定 (網際網路連線建立) 連線至網路。</p></td>
</tr>
<tr class="even">
<td><p>CalleeConnectivityICE</p></td>
<td><p>tinyint</p></td>
<td><p>指出受話者是否使用 ICE 通訊協定 (網際網路連線建立) 連線至網路。</p></td>
</tr>
</tbody>
</table>


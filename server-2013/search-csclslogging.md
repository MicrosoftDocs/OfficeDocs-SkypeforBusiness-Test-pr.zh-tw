---
title: Search-CsClsLogging
TOCTitle: Search-CsClsLogging
ms:assetid: a2eddada-a494-4bc6-b7d0-9b511dfc4ac1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619189(v=OCS.15)
ms:contentKeyID: 49291863
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Search-CsClsLogging

 

_**上次修改主題的時間：** 2015-03-09_

提供可用來搜尋集中式記錄服務記錄檔案的命令列選項。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Search-CsClsLogging [-AsXml <SwitchParameter>] [-CallId <String>] [-Components <String[]>] [-Computers <String[]>] [-ConferenceId <String>] [-CorrelationIds <String[]>] [-EndTime <DateTime>] [-IP <IPAddress>] [-LogLevel <String>] [-MatchAll <SwitchParameter>] [-MatchAny <SwitchParameter>] [-OutputFilePath <String>] [-Phone <String>] [-Pools <String[]>] [-SipContents <String>] [-SkipNetworkLogs <SwitchParameter>] [-StartTime <DateTime>] [-Uri <String>]

## 範例

## 範例 1

範例 1 所示的命令會在 atl-cs-001.litwareinc.com 電腦上找到的記錄檔中，搜尋 IP 位址 192.168.0.242。

    Search-CsClsLogging -Computers "atl-cs-001.litwareinc.com" -IP "192.168.0.242"

## 範例 2

在範例 2 中，會搜尋同時符合 IP 位址為 192.168.0.242 且 URI 為 sip:kenmyer@litwareinc.com 的項目。MatchAll 參數指定必須符合所有的條件，才會記錄為符合項目。

    Search-CsClsLogging -Computers "atl-cs-001.litwareinc.com" -IP "192.168.0.242" -Uri "sip:kenmyer@litwareinc.com" -MatchAll

## 範例 3

範例 3 所示的命令會搜尋符合 IP 位址為 192.168.0.242 或 URI 為 sip:kenmyer@litwareinc.com 的項目。MatchAny 參數指定只要符合其中一項條件，就會記錄為符合項目。

    Search-CsClsLogging -Computers "atl-cs-001.litwareinc.com" -IP "192.168.0.242" -Uri "sip:kenmyer@litwareinc.com" -MatchAny

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

**Search-CsClsLogging** Cmdlet 提供可用來搜尋集中式記錄服務所產生之記錄檔的命令列選項。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Search-CsClsLogging"}

**Lync Server 控制台：** **Search-CsClsLogging** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AsXml</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，會以 XML 格式從搜尋過的每部電腦傳回程式碼資訊，而不是字串值。</p></td>
</tr>
<tr class="even">
<td><p><em>CallId</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要搜尋的通話識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>Components</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>要搜尋的逗號分隔元件清單。</p></td>
</tr>
<tr class="even">
<td><p><em>Computers</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>要搜尋的逗號分隔電腦清單。例如：</p>
<p>-Computers &quot;server-cs-001.litwareinc.com&quot;, &quot;server-cs-002.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ConferenceId</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要搜尋的會議 ID。</p></td>
</tr>
<tr class="even">
<td><p><em>CorrelationIds</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>要搜尋的逗號分隔相互關聯識別碼清單。相互關聯是與每個要求相關聯的 32 位元整數。</p></td>
</tr>
<tr class="odd">
<td><p><em>EndTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>要搜尋的記錄項目結束日期與時間。以當地時區指定。如果不指定 StartTime，則預設為目前時間後的 5 分鐘；否則就預設為 StartTime 後的 30 分鐘。例如，在執行英文 (美國) 版 Lync Server 2013 的電腦上，下面這個語法限制搜尋在 2012 年 8 月 31 日早上 8 點之前記錄的項目：</p>
<p>-StartTime &quot;2012/8/31 8:00AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>IP</em></p></td>
<td><p>選用</p></td>
<td><p>System.Net.IPAddress</p></td>
<td><p>要搜尋的 IP 位址。這必須是實際的 IP 位址；指定位址時，不能使用萬用字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogLevel</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>指定至少要傳回的記錄項目類型。允許的值為：</p>
<p>* Fatal</p>
<p>* Error</p>
<p>* Warning</p>
<p>* Info</p>
<p>* Verbose</p>
<p>* Debug</p>
<p>* All</p>
<p>「至少要傳回的項目類型」表示 <strong>Search-CsClsLogging</strong> Cmdlet 將傳回該嚴重性層級的所有記錄項目以及更高嚴重性層級的所有記錄項目。例如，如果您將 LogLevel 設定為 Warning，Cmdlet 將傳回標示為 Fatal 與 Error 的項目，以及標示為 Warning 的項目。</p></td>
</tr>
<tr class="even">
<td><p><em>MatchAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>此參數存在時，必須符合包含的所有條件。這和 SQL Server 的 AND 查詢類似。</p></td>
</tr>
<tr class="odd">
<td><p><em>MatchAny</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>此參數存在時，只要符合包含的其中一個條件即可。這和 SQL Server 的 OR 查詢類似。這是預設值。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputFilePath</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>此參數存在時，可指定要寫入文字檔案 (包含搜尋結果) 的完整路徑。否則便會寫入主控台。</p></td>
</tr>
<tr class="odd">
<td><p><em>Phone</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要搜尋的電話號碼。您應該使用 E.164 格式來輸入這個號碼，而且不可以包含萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Pools</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>要搜尋的逗號分隔集區清單。例如：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;, &quot;red-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SipContents</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要在 SIP 訊息本文內搜尋的任意文字。</p></td>
</tr>
<tr class="even">
<td><p><em>SkipNetworkLogs</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果使用此參數，即會指示 <strong>Search-CsClsLogging</strong> Cmdlet 避免搜尋網路記錄。</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>要搜尋的記錄項目開始日期與時間。以當地時區指定。預設為 EndTime 前的 30 分鐘。例如，在執行英文 (美國) 版 Lync Server 2013 的電腦上，下面這個語法限制搜尋在 2012 年 8 月 1 日早上 8 點之後記錄的項目：</p>
<p>-StartTime &quot;8/1/2012 8:00AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要搜尋的 URI。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Search-CsClsLogging** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

字串值或 XML。

## 請參閱

#### 其他資源

[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)


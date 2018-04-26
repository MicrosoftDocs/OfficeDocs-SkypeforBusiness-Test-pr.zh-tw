---
title: Lync Server 2013：IP 電話清查報告
TOCTitle: IP 電話清查報告
ms:assetid: aa7d6b31-cb09-4e68-b020-aa5dd0081c20
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615027(v=OCS.15)
ms:contentKeyID: 49291953
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 IP 電話清查報告

 

_**上次修改主題的時間：** 2015-03-09_

「IP 電話清查報告」提供目前在組織中使用的 IP 電話相關資訊。「IP 清查報告」提供在指定的報告期間內實際使用之 IP 電話的詳細清單。除此之外，此報告可讓系統管理員得知是否仍在使用應替換的老舊、過時電話；也可以警示系統管理員有關組織中有鮮少使用的昂貴電話。在購買新電話或重新分配現有電話時，這類資訊可能非常珍貴 (例如，可能會要求鮮少使用其昂貴電話的使用者，與較頻繁使用其電話的使用者交換電話)。

請注意，若作為真正的清查報告使用，這份報告的確有一些限制。「IP 電話報告」僅列出在指定的期間內登入 Lync Server 的所有電話，並依其最近登入時間排序。如果電話未在指定的期間內登入，則不會列在清查報告中。其中包含在期間開始前登入，但仍在指定的時間間隔內登入的電話。例如，假設您要查看 2012 年 7 月的所有電話清查資料。同時假設在 2012 年 6 月 30 日有好幾支電話登入 Lync Server，但仍在 7 月 1 日進行登入。這些電話不會顯示在 7 月 1 日的清查報告上。

此外請特別注意，清查報告可能包含貴組織不再使用的電話。例如，假設有些 Fabrikam 電話在 2012 年 7 月 1 日登入系統；5 天後，貴組織以較新的 Contoso 型號汰換掉這些 Fabrikam 電話。只因為 Fabrikam 電話在 7 月間登入了系統，所以這些電話仍會出現在「清查」報告上。

此外，「IP 電話清查報告」不會提供各種電話類型的總計。例如，假設您有 105 支 Polycom CX600 電話。此報告不會告訴您您有其中 105 支電話；您只會看見 Polycom Cx600 的 105 個個別項目。要知道 Polycom Cx600 有 105 項的唯一方法就是手動計算各個項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>或者，匯出資料並使用 Microsoft Excel 或 Windows PowerShell 進行計算。</td>
</tr>
</tbody>
</table>


## 存取 IP 電話清查報告

「IP 電話清查報告」是從「監控報告」首頁存取。如果您按一下 \[使用 URI\] 計量，即可存取該使用者的「使用者活動報告」。按一下最新的活動標準以進行對等通話會將您導向「對等工作階段詳細資料報告」；按一下相同標準以進行會議會將您導向「會議詳細資料報告」。

## 充分利用 IP 電話清查報告

如果您只對特定一種電話的使用情況資訊有興趣 (例如，「使用者使用 Polycom CX600 電話的頻率為何？」)，您可以篩選該特定種類的電話，進而直接從「IP 電話清查報告」取得該資訊。但是，如果您想要所有電話的摘要資訊 (有多少人在使用 Polycom CX600、有多少人在使用 LG-Nortel IP8540 等)，您就必須匯出資料，並使用其他應用程式 (如 Windows PowerShell) 進行該類型的分析。舉例來說，假設您將資料匯出成逗號分隔值檔案 (C:\\Data\\IP\_Phone\_Inventory\_Report.csv)。在這種情況下，您可使用以下兩個命令來提供所有電話的摘要資料；

    $phones = Import-Csv "C:\Data\IP_Phone_Inventory_Report.csv"
    $phones |Group-Object Manufacturer, "Hardware version" | Select-Object Count, Name | Sort-Object Count -Descending

將傳回類似下列的資料：

    Count    Name
    -----    ----
      267    POLYCOM, CX700
      267    POLYCOM, CX600
      166    POLYCOM, C
       68    Microsoft, CPE
       64    LG-Nortel, IP8540
       59    Aastra, 6725ip
       37    LG-Nortel, IP
       22    POLYCOM, CX3000
       11    Microsoft, CPE_A
        9    POLYCOM, CX500
        7    Aastra, 6721ip

同樣地，這兩個命令可讓您知道有哪些電話登入系統，但從未實際用於撥打電話 (上次活動計量值空白，表示沒有任何上次活動)：

    $phones = Import-Csv "C:\Data\IP_Phone_Inventory_Report.csv"
    $phones | Where-Object {$_."Last activity" -eq ""}

針對尚未使用的每部電話傳回類似以下的資料：

    Manufacturer     : POLYCOM
    Hardware version : CX600
    MAC address      : 00-04-F2-00-01-76
    User URI         : 422
    User agent       : CPE/4.0.7423.1 OCPhone/4.0.7423.1 (Microsoft Lync 2010 (Beta) Phone Edition)
    Last logon time  : 8/30/2010 4:44:48 PM
    Last logoff time : 8/30/2010 5:59:07 PM
    Last activity    :

另一種使用「IP 電話清查報告」的有趣方式：如果您有 IP 電話的 MAC 位址，只需在 \[MAC 位址\] 文字方塊中輸入該位址，即可找出最後使用該電話的使用者。「IP 電話清查報告」將會回報使用該電話進行登入之使用者的 SIP 位址。此外，您可以輸入使用者 SIP 位址 (在 \[使用者 URI 首碼\] 方塊中)，以找出該使用者使用過的所有電話。

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，\[IP 電話清查\] 可讓您只檢視某家公司所生廠的電話，甚至是某特定版本的電話。您也可以選擇資料的分組方式。在本文件中，登錄項目會依小時、日、星期或月進行分組。

下表列出了可搭配 IP 電話清查報告使用的篩選器。

### IP 電話清查報告的篩選器

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>從</strong></p></td>
<td><p>時間範圍的開始日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>製造商</strong></p></td>
<td><p>生產該 IP 電話的公司名稱。此篩選器的值會依據資料庫目前所有的 IP 電話自動填入。</p></td>
</tr>
<tr class="even">
<td><p><strong>硬體版本</strong></p></td>
<td><p>IP 電話的版本號碼；您可以利用製造商硬體版本篩選器，單獨列出特定類型的電話。此篩選器的值會依據資料庫目前所有的 IP 電話自動填入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>使用者代理程式</strong></p></td>
<td><p>IP 電話所使用之軟體的識別碼。此篩選器的值會依據資料庫目前所有的 IP 電話自動填入。</p></td>
</tr>
<tr class="even">
<td><p><strong>MAC 位址</strong></p></td>
<td><p>IP 電話網路介面的唯一識別碼。媒體存取控制 (MAC) 位址通常會在出廠時加以指派，並寫在裝置硬體中。</p>
<p>若要搜尋某 MAC 位址的記錄，只要輸入該位址即可。例如：</p>
<p>00-08-5D-16-16-48</p>
<p>請務必輸入完整的位址。若只輸入部分位址 (如 00-08-5D)，將不會傳回任何資料。</p></td>
</tr>
<tr class="odd">
<td><p><strong>以下天數前的最後活動</strong></p></td>
<td><p>選取下列其中一值：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>10</p></li>
<li><p>20</p></li>
<li><p>30</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>以下天數前的最後登出時間</strong></p></td>
<td><p>選取下列其中一值：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>10</p></li>
<li><p>20</p></li>
<li><p>30</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>使用者 URI 字首</strong></p></td>
<td><p>使用 IP 電話之使用者的 SIP 位址。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出 IP 電話清查報告提供的資訊。

### IP 電話清查報告計量

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
<td><p><strong>製造商</strong></p></td>
<td><p>是</p></td>
<td><p>生產該 IP 電話的公司名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>硬體版本</strong></p></td>
<td><p>是</p></td>
<td><p>IP 電話的版本號碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MAC 位址</strong></p></td>
<td><p>是</p></td>
<td><p>IP 電話網路介面的唯一識別碼。此 MAC 位址通常會在出廠時加以指派，並寫在裝置硬體中。</p></td>
</tr>
<tr class="even">
<td><p><strong>使用者 URI</strong></p></td>
<td><p>是</p></td>
<td><p>使用 IP 電話之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>使用者代理程式</strong></p></td>
<td><p>是</p></td>
<td><p>IP 電話所使用之軟體的識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>上次登入時間</strong></p></td>
<td><p>是</p></td>
<td><p>IP 電話上次登入 Lync Server 的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>上次登出時間</strong></p></td>
<td><p>是</p></td>
<td><p>IP 電話上次登出 Lync Server 的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>上次活動</strong></p></td>
<td><p>是</p></td>
<td><p>上次使用 IP 電話的日期與時間。</p></td>
</tr>
</tbody>
</table>


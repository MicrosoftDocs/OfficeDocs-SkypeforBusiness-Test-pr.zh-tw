---
title: Lync Server 2013：PSTN 會議摘要報告
TOCTitle: PSTN 會議摘要報告
ms:assetid: 8e2f0862-4dfa-4c2b-bf8d-ad71419f15d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615014(v=OCS.15)
ms:contentKeyID: 49291627
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 PSTN 會議摘要報告

 

_**上次修改主題的時間：** 2015-03-09_

在 Microsoft Lync Server 2013 中，PSTN 會議是任何至少有一位參與者是使用 PSTN (公用交換電話網路) 電話撥入音訊部分的會議 (PSTN 電話是「室內電話」、行動電話或任何其他未使用 VoIP 的電話)。即使在監控報告中稱為 PSTN 會議，這些會議更為全域的名稱或許是電話撥入式會議。

PSTN 會議摘要報告提供關於貴組織中所舉行之所有 PSTN 會議的資訊 (也就是所有至少有一位撥入使用者的會議)。此報告包含 PSTN 會議總數、參與這些會議的總人數，或許還有最重要的撥入使用者總數 (PSTN 參與者總數衡量標準) 等相關資訊。

## 存取 PSTN 會議摘要報告

PSTN 會議摘要報告只能從 \[監控報告\] 首頁存取。此報告未連結至任何其他報告。請注意，您無法擷取某個 PSTN 會議的詳盡通話資訊，有一部分是因為有個別端點會負責提交此資訊。PSTN 電話無法追蹤或提交通話詳細資訊。

## PSTN 會議摘要報告的最佳用法

若要判斷所有包含撥入使用者之會議的百分比，請將 \[PSTN 會議總數\] 衡量標準的值與可在 [Lync Server 2013 中的會議摘要報告](lync-server-2013-conference-summary-report.md)中找到的 \[會議總數\] 衡量標準進行比較。

如果您看見的 PSTN 會議數目不如您預期的多，請記住，召集允許撥入使用者之會議的功能會根據指派給使用者的會議原則而定：如果允許舉行 PSTN 會議的使用者人數非常少，很顯然地，您看見的 PSTN 會議數目就會非常少。您可以快速確認會議原則中有哪些 (如果有的話) 允許使用者透過從 Lync Server 管理命令介面執行下列命令來排程 PSTN 會議：

    Get-CsConferencingPolicy | Select-Object Identity, EnableDialInConferencing

將傳回類似下列的資料：

    Identity                                EnableDialInConferencing
    --------                                ------------------------
    Global                                                      True
    site:Redmond                                               False
    site:Dublin                                                False
    Tag:RedmondDialInUsers                                      True
    Tag:DublinDialInUsers                                       True

將傳回類似下列的資料：

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，PSTN 會議摘要報告可讓您選擇資料分組的方式。在這個情況下，會議會按照小時、日、星期或月份而加以分組。

下表列出您可以搭配 PSTN 會議摘要報告的篩選器。

### PSTN 會議摘要報告的篩選器

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
<td><p><strong>間隔</strong></p></td>
<td><p>時間間隔。請選取下列其中一項：</p>
<ul>
<li><p>每小時 (最多可以顯示 25 個小時)</p></li>
<li><p>每日 (最多可以顯示 31 天)</p></li>
<li><p>每週 (最多可以顯示 12 週)</p></li>
<li><p>每月 (最多可以顯示 12 個月)</p></li>
</ul>
<p>若開始與結束日期超出所選間隔允許的上限值，則將只會顯示上限值 (從開始日期開始顯示)。例如，若您選取 [每日] 間隔，並將開始與結束日期分別設為 7/7/2012 及 2/28/2012，則將只會顯示 8/7/2012 12:00 AM 至 9/7/2012 12:00 AM 這段期間的資料 (亦即只會顯示 31 天的資料)。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出 PSTN 會議摘要報告中的資訊。

### PSTN 會議摘要報告計量

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
<td><p><strong>每小時</strong></p>
<p><strong>每日</strong></p>
<p><strong>每週</strong></p>
<p><strong>每月</strong></p></td>
<td><p>否</p></td>
<td><p>顯示所選的時間間隔。在適用的情況下，只要按一下所指出的時間間隔，即可檢視該間隔的詳細資訊。例如，您若是使用 [每日] 間隔，然後按一下 7/7/2012，將會顯示使用者所登錄該日每小時的活動。</p></td>
</tr>
<tr class="even">
<td><p><strong>PSTN 會議總數</strong></p></td>
<td><p>否</p></td>
<td><p>允許撥入存取的會議總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>參與者總數</strong></p></td>
<td><p>否</p></td>
<td><p>參與允許撥入存取之會議的總人數</p></td>
</tr>
<tr class="even">
<td><p><strong>A/V 會議總分鐘數</strong></p></td>
<td><p>否</p></td>
<td><p>音訊/視訊會議的總時數</p></td>
</tr>
<tr class="odd">
<td><p><strong>A/V 會議參與者總分鐘數</strong></p></td>
<td><p>否</p></td>
<td><p>音訊/視訊會議的參與者總時數。例：一位參與者在某場 A/V 會議參與了 5 分鐘，另一位參與者在同一場 A/V 會議參與了 3 分鐘，則這場 A/V 會議的參與者總時數等於 8 分鐘。</p></td>
</tr>
<tr class="even">
<td><p><strong>PSTN 參與者總數</strong></p></td>
<td><p>否</p></td>
<td><p>撥入參與允許撥入存取之會議的總人數</p></td>
</tr>
<tr class="odd">
<td><p><strong>PSTN 參與者總分鐘數</strong></p></td>
<td><p>否</p></td>
<td><p>撥入使用者參與會議的總時數。例：一位撥入參與者在某場會議參與了 5 分鐘，另一位參與者在同一場會議參與了 3 分鐘，則 PSTN 參與者總時數等於 8 分鐘。</p></td>
</tr>
<tr class="even">
<td><p><strong>會議個別召集人總數</strong></p></td>
<td><p>否</p></td>
<td><p>召集至少一場允許撥入存取之會議的使用者總人數。召集一場以上會議的使用者，和只召集一場會議的使用者一樣，都只計算為 1 位個別召集人。</p></td>
</tr>
</tbody>
</table>


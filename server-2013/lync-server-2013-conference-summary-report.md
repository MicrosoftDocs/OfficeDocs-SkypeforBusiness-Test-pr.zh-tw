---
title: Lync Server 2013：會議摘要報告
TOCTitle: 會議摘要報告
ms:assetid: 62f54812-5700-45a3-8526-8f58b0f77fbc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558656(v=OCS.15)
ms:contentKeyID: 49291117
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的會議摘要報告

 

_**上次修改主題的時間：** 2015-03-09_

會議摘要報告提供線上會議工作階段的整體檢視。會議通常涉及 2 位使用者以上，並且需要使用 Microsoft Lync Server 2013 會議服務。相較之下，對等工作階段通常只涉及兩位使用者，而且不需要使用 Lync Server 的會議服務。對等活動會在 [Lync Server 2013 中的對等活動摘要報告](lync-server-2013-peer-to-peer-activity-summary-report.md)中報告。

會議摘要報告不但告訴您在指定期間內 (每小時、每日、每週、每月) 舉行多少場會議，還可告訴您參與那些會議的總人數，以及專屬會議召集人的總數。

「專屬」召集人是任何至少排程一場會議的人。例如，如果 Pilar Ackerman 排程一場會議，她就算是一位專屬召集人。如果 Ken Myer 排程 148 場會議，他也算是一位專屬召集人。 例如，下表顯示排程 8 場會議，但只有 3 位專屬召集人 (Ken Myer、Pilar Ackerman 及 David Ahs)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>會議召集人</th>
<th>會議日期</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>David Ahs</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 1:00 PM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 2:00 PM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
</tbody>
</table>


會議摘要報告還會指出多少場會議包含音訊和/或視訊。

## 存取會議摘要報告

從 \[監控報告\] 首頁可存取會議摘要報告。按下列計量，即可向下切入至會議活動報告：

  - 會議總數

  - 參與者總數

## 發揮會議摘要報告的最大效用

會議摘要報告上大多數所用計量的總數值可見於報告下方；向下捲動即可見到這些值，例如指定期間內舉行的會議總數，以及參與這些會議的總人數。報告下方未總計的一個計量是專屬會議召集人總數。理由何在？原因之一是，假設您在檢視一個月的資料，第一天有 34 位專屬會議召集人，第二天有 27 位專屬會議召集人。這表示兩天總共有 61 位專屬會議召集人嗎？這可不一定。畢竟在第二天召集會議的所有 27 位人員有有可能就在第一天召集會議的 34 位人員之中。例如，在下列簡單報告中，注意到 Ken Myer 與 Pilar Ackerman 在 7/7/2012 和 7/2/2012 兩天都有排程會議：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>會議召集人</th>
<th>會議日期</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>David Ahs</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 1:00 PM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 2:00 PM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
</tbody>
</table>


若要更清楚了解召集會議之專屬使用者的總數，請變更時間間隔；例如，按月而不是按日來檢視資料。

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，會議摘要報告可讓您選擇如何將資料分組。在這種情況下，會議會按照小時、日、星期或月加以分組。

下表列出您可以用於會議摘要報告的篩選器。

### 會議摘要報告篩選器

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
<p>若開始與結束日期超出所選間隔允許的上限值，將只會顯示上限值 (從開始日期開始顯示)。例如，若您選取 [每日] 間隔，並將開始與結束日期分別設為 7/7/2012 及 2/28/2012，將只會顯示 8/7/2012 12:00 AM 點到 9/7/2012 12:00 AM 點這段期間的資料 (亦即只會顯示 31 天的資料)。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出會議摘要報告提供的資訊。

### 會議摘要報告計量

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
<td><p>在篩選工具列上顯示您所選取的時間間隔。在適用的情況下，只要按一下所指出的時間間隔，即可檢視該間隔的詳細資訊。例如，您若是使用 [每日] 間隔，然後按一下 7/7/2012，將會顯示使用者所登錄該日每小時的活動。</p></td>
</tr>
<tr class="even">
<td><p><strong>會議總數</strong></p></td>
<td><p>否</p></td>
<td><p>已舉辦的會議總數 (無論會議類型為何)。當您按一下此項目，報告即顯示所選定時段的會議活動報告。</p></td>
</tr>
<tr class="odd">
<td><p><strong>參與者總數</strong></p></td>
<td><p>否</p></td>
<td><p>參加會議的總人數。當您按一下此項目，報告即顯示所選定時段的會議活動報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>每次會議的平均參加人數</strong></p></td>
<td><p>否</p></td>
<td><p>參加給定會議的平均人數。將會議總數除以參與者總數得之。</p></td>
</tr>
<tr class="odd">
<td><p><strong>A/V 會議總數</strong></p></td>
<td><p>否</p></td>
<td><p>包含音訊或視訊的會議總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>A/V 會議總分鐘數</strong></p></td>
<td><p>否</p></td>
<td><p>用於音訊/視訊會議的總分鐘數。</p>
<p>「A/V 會議總分鐘數」度量會摘要顯示所有音訊/視訊會議類型，包含 A/V 會議、IM 會議、App 共用會議、資料會議和 PSTN 會議。</p></td>
</tr>
<tr class="odd">
<td><p><strong>A/V 會議參與者總分鐘數</strong></p></td>
<td><p>否</p></td>
<td><p>用於音訊/視訊會議的參與者總分鐘數。例如，假設一位使用者花 5 分鐘參加音訊/視訊會議，而另一位使用者花 3 分鐘參加相同的會議。所以參與者總分鐘數為 8 分鐘：5 分鐘加 3 分鐘。</p></td>
</tr>
<tr class="even">
<td><p><strong>A/V 會議平均分鐘數</strong></p></td>
<td><p>否</p></td>
<td><p>每次音訊/視訊會議的平均分鐘數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>會議專屬召集人總數</strong></p></td>
<td><p>否</p></td>
<td><p>至少召集過一次會議的使用者總數。召集過多次會議的使用者計為一個專屬召集人，就像只召集過一次會議的使用者一樣。</p></td>
</tr>
<tr class="even">
<td><p><strong>會議訊息總數</strong></p></td>
<td><p>否</p></td>
<td><p>會議期間傳送的立即訊息總數。</p></td>
</tr>
</tbody>
</table>


---
title: Lync Server 2013：Top Failures 報告
TOCTitle: Top Failures 報告
ms:assetid: 438942e2-580a-4b67-9d42-f116111fb26a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558640(v=OCS.15)
ms:contentKeyID: 49290752
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Top Failures 報告

 

_**上次修改主題的時間：** 2015-03-09_

Top Failures 報告列出最常發生的失敗及其在一段時間後的趨勢。

  - **診斷 ID** 。附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)。診斷 ID 可以在疑難排解通話相關錯誤時提供實用的資訊。

  - **回應碼** 。回應碼是用於 SIP 通訊工作階段，藉此回應 SIP 要求。舉例來說，假設 Ken 傳送 INVITE 要求給 Pilar Ackerman (亦即假設 Ken Myer 打電話給 Pilar Ackerman)，若 Pilar 接聽，電話就會傳送回應碼 200 (確定)，Ken 的電話就會得知 Pilar 已接聽。最大失敗報告僅包含已傳送的回應碼，作為通話失敗回應； Lync Server 不會追蹤通話期間所有發佈的回應碼。

資訊回報內容不僅有發生失敗的工作階段總數，還有因失敗受到影響的使用者總數。

## 存取最大失敗報告

可以從監視報告首頁存取最大失敗報告。按一下已回報工作階段計量可帶領您前往 [Lync Server 2013 中的失敗散佈報告](lync-server-2013-failure-distribution-report.md)。

## 善用最大失敗報告

在某方面而言，最大失敗報告顯得十分特別：此報告最多能讓您一次篩選 5 個診斷 ID (通常一次只能篩選一個項目，例如一個使用者 SIP 位址)。若要篩選多個診斷 ID，只要在「診斷 ID」方塊中輸入各個 ID，並以逗號區隔即可 (也可以在每個逗號後面留下空格)。例如：

1011, 2412, 1033, 52116, 1008

完成後，只會顯示回報五個診斷 ID 中至少有一個 ID 的失敗通話。

如果您將滑鼠移到回應碼時會看到工具提示，說明有問題的回應代碼所代表的涵義。例如將滑鼠移到回應碼 486，會看到此訊息：

此處非常忙碌。

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，「最大失敗報告」可讓您依據活動類型之類的項目 (對等工作階段或會議工作階段)，或是依失敗工作階段隨附的 SIP 回應碼，篩選傳回的資料。您也可以選擇資料的分組方式。在這種情況下，使用量會按照小時、日、星期或月加以分組。

下表列出您可以用於最大失敗報告的篩選器。

### 最大失敗報告篩選器

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
<td><p><strong>活動類型</strong></p></td>
<td><p>活動的類型。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>對等</p></li>
<li><p>會議</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>形式</strong></p></td>
<td><p>目前唯一可用的選項是 [全部] 。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>登錄器集區或 Edge Server 的完整網域名稱 (FQDN)。您可以選取個別的集區，或是按一下 [全部] 檢視所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。</p></td>
</tr>
<tr class="even">
<td><p><strong>類別</strong></p></td>
<td><p>遇到的失敗類型。請選取下列其中一項：</p>
<ul>
<li><p>預期及未預期的失敗</p></li>
<li><p>未預期的失敗</p></li>
</ul>
<p>「預期的失敗」是指預期會發生的失敗。 例如，當使用者將其狀態設為「勿打擾」時，即應預期所有撥話給該使用者的通話皆會失敗。「未預期的失敗」是指起因於系統不健全的失敗。 例如，當發話者處於保留狀態時，不應掛斷通話。 當發生此狀況時，會將其標幟為未預期的失敗。</p></td>
</tr>
<tr class="odd">
<td><p><strong>回應碼</strong></p></td>
<td><p>會議失敗時所傳送的 SIP 回應碼。請輸入完整的回應碼，例如：</p>
<p>400</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。診斷標頭為選用 (也可能有 SIP 工作階段不包含這些標頭)。只有發生特定問題的工作階段才會回報診斷識別碼。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出前幾名失敗報告提供的資訊。

### 最大失敗報告計量

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
<td><p><strong>排名</strong></p></td>
<td><p>是</p></td>
<td><p>依據所報告之工作階段數的相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>報告的工作階段</strong></p></td>
<td><p>是</p></td>
<td><p>依據診斷識別碼及 SIP 回應碼的失敗工作階段總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>受影響的使用者</strong></p></td>
<td><p>是</p></td>
<td><p>受失敗工作階段影響的使用者總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>失敗資訊</strong></p></td>
<td><p>否</p></td>
<td><p>失敗的詳細資訊，包括診斷識別碼、SIP 回應碼，以及工作階段為什麼失敗的說明。</p></td>
</tr>
<tr class="odd">
<td><p><strong>過去的趨勢</strong></p></td>
<td><p>否</p></td>
<td><p>一段時間的失敗工作階段圖表。</p></td>
</tr>
</tbody>
</table>


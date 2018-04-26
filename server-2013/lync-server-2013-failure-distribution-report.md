---
title: Lync Server 2013：失敗散佈報告
TOCTitle: 失敗散佈報告
ms:assetid: 365c7beb-24d4-40f5-92e7-4978b9688916
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558635(v=OCS.15)
ms:contentKeyID: 49290570
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的失敗散佈報告

 

_**上次修改主題的時間：** 2015-03-09_

失敗散佈報告會在下列類別中為失敗的工作階段進行排名：

  - 前幾名診斷原因

  - 前幾名形式

  - 前幾名集區

  - 前幾名來源

  - 前幾名元件

  - 前幾名發話使用者

  - 前幾名受話使用者

  - 最常見來源使用者代理程式

您可以使用這些類別來判斷確實發生問題的地方，並在某些情況下判斷發生問題的原因。例如，假設您在某一天記錄了 242 個失敗的音訊/視訊工作階段。如果您查看失敗散佈報告，其中可能會顯示有 237 個失敗的工作階段是發生在您的 Dublin 集區中。這讓您在追蹤和診斷這些失敗背後的原因時可以有一個良好的開端。如果您按一下 **\[最常見集區\]** 類別下方的 Dublin 集區，就只會看見該集區的失敗散佈報告。接著，您可以開始分析為什麼 Dublin 集區會遇到這麼多問題。

## 檢視失敗散佈報告

您可以按一下 **\[預期失敗次數\]** 或 **\[未預期失敗次數\]** 計量，從下列任一個報告存取失敗散佈報告：

  - [Lync Server 2013 中的 Top Failures 報告](lync-server-2013-top-failures-report.md)

  - [Lync Server 2013 中的會議診斷報告](lync-server-2013-conference-diagnostic-report.md)

  - [Lync Server 2013 中的對等活動診斷報告](lync-server-2013-peer-to-peer-activity-diagnostic-report.md)

從失敗散佈報告中，您可以按一下下列任一個計量，以檢視 [Lync Server 2013 中的失敗清單報告](lync-server-2013-failure-list-report.md)：

  - 熱門診斷原因 (工作階段)

  - 熱門形式 (工作階段)

  - 熱門集區 (工作階段)

  - 熱門來源 (工作階段)

  - 熱門元件 (工作階段)

  - 源自使用者的熱門項目 (工作階段)

  - 流向使用者的熱門項目 (工作階段)

  - 源自使用者代理的熱門項目 (工作階段)

## 使用失敗散佈報告

根據您的監視器大小和螢幕解析度而定，當您在螢幕上檢視失敗散佈報告時，該報告中顯示的部分資料可能被截斷。這種情況特別會出現在像是使用者代理程式的計量中，因為這類計量含有非常長的標籤。例如，名稱像是 "UCCAPI/4.0.7400.0 OC/4.0.7400.0 (Microsoft Lync 2013)" 的使用者代理程式可能只會在螢幕上顯示部分名稱：

UCCAPI/4.0.7400.0 OC/4.0.7400.0 (Microsoft Ly...

幸運地是，您只需在截斷的值上按住滑鼠，就可以看見完整的標籤。

有一個您可以使用失敗散佈報告來篩選的特別計量是診斷識別碼。如果您在其他報告中看見經過剪裁的相同診斷識別碼，就可以在失敗散佈報告中使用該識別碼來篩選，並取得在失敗工作階段執行期間該識別碼確實出現在何處以及出現的頻率等非常詳盡的內容。

## 篩選器

篩選可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，失敗散佈報告可讓您依活動類型 (對等工作階段或會議工作階段) 之類的項目，或是依每個失敗工作階段隨附的診斷識別碼篩選。

下表列出您可以用於失敗散佈報告的篩選。

### 失敗散佈報告篩選

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
<p>7/7/12</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>3/7/12</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/12</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>3/7/12</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>登錄器集區 或 Edge Server 的完整網域名稱 (FQDN)。您可選取個別集區，或按一下 [全部] 以檢查所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。</p></td>
</tr>
<tr class="even">
<td><p><strong>活動類型</strong></p></td>
<td><p>篩選的活動類型。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>對等</p></li>
<li><p>會議</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段類別</strong></p></td>
<td><p>指出有疑問的活動為成功或失敗。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>成功</p></li>
<li><p>預期的失敗</p></li>
<li><p>未預期的失敗</p></li>
</ul>
<p>「預期的失敗」是指預期會發生的失敗。 例如，當使用者將其狀態設為「勿打擾」時，即應預期所有撥話給該使用者的通話皆會失敗。「未預期的失敗」是指起因於系統不健全的失敗。 例如，當發話者處於保留狀態時，不應掛斷通話。 當發生此狀況時，會將其標幟為未預期的失敗。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。診斷標頭為選用 (也可能有 SIP 工作階段不包含這些標頭)。只有發生特定問題的工作階段才會回報診斷識別碼。</p></td>
</tr>
</tbody>
</table>


## 前幾名診斷原因的計量

下表依據最常報告的診斷識別碼，列出失敗散佈報告中提供的資訊。

### 前幾名診斷原因的計量

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
<td><p>否</p></td>
<td><p>依據診斷識別碼的失敗工作階段相對排名。診斷識別碼是附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名診斷原因</strong></p></td>
<td><p>否</p></td>
<td><p>在工作階段產生的診斷識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>產生所指定之診斷識別碼的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名形式的計量

下表依據最常發生失敗的工作階段形式，列出失敗散佈報告中提供的資訊。

### 前幾名形式的計量

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
<td><p>否</p></td>
<td><p>依據工作階段類型 (例如，音訊/視訊會議或對等檔案傳輸工作階段) 的失敗工作階段相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名形式</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段類型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>與指定形式有關的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名集區的計量

下表依據最常發生失敗的集區，列出失敗散佈報告中提供的資訊。

### 前幾名集區的計量

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
<td><p>否</p></td>
<td><p>依據執行工作階段所在之 登錄器集區或 Edge Server 的失敗工作階段相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名集區</strong></p></td>
<td><p>否</p></td>
<td><p>登錄器集區或 Edge Server 的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>每個 登錄器集區或 Edge Server 的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名來源的計量

下表依據最常發生失敗的電腦，列出失敗散佈報告中提供的資訊。

### 前幾名來源的計量

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
<td><p>否</p></td>
<td><p>每部電腦的失敗工作階段相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名來源</strong></p></td>
<td><p>否</p></td>
<td><p>與失敗工作階段相關的電腦名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>每部電腦的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名元件的計量

下表依據最常發生失敗的 Microsoft Lync Server 2010 元件，列出失敗散佈報告中提供的資訊。

### 前幾名元件的計量

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
<td><p>否</p></td>
<td><p>依據 Lync Server 2010 元件 (例如 ExumRouting、GroupChat 或 MediationServer) 的失敗工作階段相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名元件</strong></p></td>
<td><p>否</p></td>
<td><p>與失敗工作階段相關的元件名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>每個元件的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名發話使用者的計量

下表依據最常在嘗試呼叫他人時發生失敗的使用者 (即所謂的「發話」使用者)，列出失敗散佈報告中提供的資訊。

### 前幾名發話使用者的計量

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
<td><p>否</p></td>
<td><p>依據受邀參加工作階段之使用者的失敗工作階段相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名發話使用者</strong></p></td>
<td><p>否</p></td>
<td><p>受邀參加工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>每位使用者的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名受話使用者的計量

下表依據最常在其他使用者呼叫他們時發生失敗的使用者 (即所謂的「受話」使用者)，列出失敗散佈報告中提供的資訊。


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
<td><p>否</p></td>
<td><p>依據啟動工作階段之使用者的失敗工作階段相對排名。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名受話使用者</strong></p></td>
<td><p>否</p></td>
<td><p>啟動工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>每位使用者的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


## 前幾名使用者代理程式的計量

下表依據最常發生失敗的端點軟體，列出失敗通訊報告中提供的資訊。

### 前幾名使用者代理程式的計量

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
<td><p>否</p></td>
<td><p>依據與工作階段相關之使用者代理程式 (軟體) 的失敗工作階段相對排名。例如：RTCC/4.0.0.0 輸入路由/4.0.0.0。</p></td>
</tr>
<tr class="even">
<td><p><strong>前幾名使用者代理程式</strong></p></td>
<td><p>否</p></td>
<td><p>與失敗工作階段相關的使用者代理程式名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>每個使用者代理程式的失敗工作階段總數。</p></td>
</tr>
</tbody>
</table>


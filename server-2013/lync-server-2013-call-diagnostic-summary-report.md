---
title: Lync Server 2013：通話診斷摘要報告
TOCTitle: 通話診斷摘要報告
ms:assetid: 9091de56-13e6-440e-9353-f57c10c906fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615016(v=OCS.15)
ms:contentKeyID: 49291658
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話診斷摘要報告

 

_**上次修改主題的時間：** 2015-03-09_

通話診斷摘要報告提供關於失敗之對等工作階段與會議工作階段的整體概觀。此報告會顯示這兩個工作階段類型的整體失敗率，並依據工作階段形式類型進一步細分失敗資訊：

  - 立即訊息

  - 應用程式共用

  - 檔案傳輸

  - 音訊

  - 視訊

## 存取通話診斷摘要報告

通話診斷摘要報告可以從 \[監控報告\] 首頁進行存取。從通話診斷摘要報告中，您可以按一下報告之 \[對等工作階段摘要\] 區段下方的 \[失敗率\] 計量，來存取 [Lync Server 2013 中的對等活動診斷報告](lync-server-2013-peer-to-peer-activity-diagnostic-report.md)。您也可以按一下下列會議計量來存取 [Lync Server 2013 中的會議診斷報告](lync-server-2013-conference-diagnostic-report.md)：

  - 整體工作階段失敗率

  - Focus 失敗率

  - MCU 失敗率

## 通話診斷摘要報告的最佳用法

通話診斷摘要報告所包含的圖表可以比較 Microsoft Lync Server 2013 中所使用之各種形式的失敗率。這些圖表中的欄實際上是熱門連線；例如，如果您按一下對等工作階段的立即訊息欄，將向下切入至 [Lync Server 2013 中的對等活動診斷報告](lync-server-2013-peer-to-peer-activity-diagnostic-report.md)的執行個體，此報告會提供其他關於通話診斷摘要報告中所含之所有立即訊息工作階段的詳細資料。

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，通話診斷摘要報告可讓您篩選工作階段中使用的登錄器集區或 Edge Server。您也可以選擇資料的分組方式。在這種情況下，通話會按照小時、日、星期或月加以分組。

下表列出您可以搭配通話診斷摘要報告的篩選器。

### 通話診斷摘要報告篩選器

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
<td><p><strong>間隔</strong></p></td>
<td><p>時間間隔。請選取下列其中一項：</p>
<ul>
<li><p>每小時 (最多可以顯示 25 個小時)</p></li>
<li><p>每日 (最多可以顯示 31 天)</p></li>
<li><p>每週 (最多可以顯示 12 週)</p></li>
<li><p>每月 (最多可以顯示 12 個月)</p></li>
</ul>
<p>若開始與結束日期超出所選間隔允許的上限值，將只會顯示上限值 (從開始日期開始顯示)。例如，若您選取 [每日] 間隔，並將開始與結束日期分別設為 7/7/2012 及 2/28/2012，將只會顯示 8/7/2012 上午 12 點至 9/7/2012 上午 12 點這段期間的資料 (亦即只會顯示 31 天的資料)。</p></td>
</tr>
<tr class="even">
<td><p><strong>集區</strong></p></td>
<td><p>登錄器集區或 Edge Server 的完整網域名稱 (FQDN)。您可以選取個別的集區，或是按一下 [全部] 檢視所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。</p></td>
</tr>
</tbody>
</table>


## 對等工作階段的計量

下表列出對等工作階段 (也就是只涉及兩位參與者的工作階段) 之通話診斷摘要報告所提供的資訊。

### 對等工作階段的計量

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
<td><p><strong>工作階段總數</strong></p></td>
<td><p>否</p></td>
<td><p>進行過的對等工作階段總數</p></td>
</tr>
<tr class="even">
<td><p><strong>失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>對等工作階段失敗的百分比。當您按一下此項目，就會顯示對等活動診斷報告，其中含有更多對等工作階段失敗的詳細資訊。</p></td>
</tr>
</tbody>
</table>


## 會議工作階段的計量

下表列出會議工作階段 (也就是涉及三位以上參與者的工作階段) 之通話診斷摘要報告所提供的資訊。

### 會議工作階段的計量

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
<td><p><strong>會議總數</strong></p></td>
<td><p>否</p></td>
<td><p>進行過的會議總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>會議工作階段總數</strong></p></td>
<td><p>否</p></td>
<td><p>進行過的會議工作階段總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>整體工作階段失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>失敗會議工作階段佔全體的百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>Focus 工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>基於 Focus 的會議工作階段失敗總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Focus 失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>基於 Focus 的會議工作階段失敗百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>MCU 工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>基於會議伺服器 (過去稱為 Multipoint Control Unit 或 MCU) 的失敗會議總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MCU 失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>基於會議伺服器 (過去稱為 Multipoint Control Unit 或 MCU) 的會議失敗百分比。</p></td>
</tr>
</tbody>
</table>


---
title: 會議摘要子報表
TOCTitle: 會議摘要子報表
ms:assetid: 2fc1d2bf-34f5-4093-a6e2-250ec1f1b004
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204779(v=OCS.15)
ms:contentKeyID: 49290482
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 會議摘要子報表

 

_**上次修改主題的時間：** 2015-03-09_

會議摘要子報告提供了失敗會議工作階段的整體檢視。這些失敗的工作階段可藉由工作階段類型加以細分為：焦點工作階段及 MCU 工作階段。

## 篩選器

篩選器可供您用於傳回更加精確的一組資料，或是使用其他方式檢視傳回的資料。下表列出可搭配會議摘要子報告使用的篩選器。

### 會議摘要子報告篩選器

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
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入結束日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>登錄器集區或 Edge Server 的完整網域名稱 (FQDN)。您可以選取個別的集區，或是按一下 [全部] 檢視所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出會議摘要子報告中提供的資訊。

### 會議摘要子報告計量

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
<td><p>保留的會議總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>會議工作階段總數</strong></p></td>
<td><p>否</p></td>
<td><p>會議工作階段總數。單一會議可能會有多個工作階段；例如，會議可能包含焦點工作階段及 MCU 工作階段。</p></td>
</tr>
<tr class="odd">
<td><p><strong>整體工作階段失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>所有失敗工作階段的百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>焦點工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>焦點工作階段總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>焦點失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>失敗之焦點工作階段的百分比。</p></td>
</tr>
<tr class="even">
<td><p>MCU 工作階段</p></td>
<td><p>否</p></td>
<td><p>MCU 工作階段總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MCU 失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>失敗之 MCU 工作階段的百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>依形式區分的 MCU 工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>依形式分組 (例如，IM 會議) 的 MCU 工作階段總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>依形式區分的失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>依形式分組 (例如，IM 會議) 的 MCU 工作階段百分比。</p></td>
</tr>
</tbody>
</table>


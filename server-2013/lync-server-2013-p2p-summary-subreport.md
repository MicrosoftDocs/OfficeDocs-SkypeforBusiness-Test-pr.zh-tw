---
title: P2P 摘要子報表
TOCTitle: P2P 摘要子報表
ms:assetid: fc36185a-3cc5-4167-8c93-8a755fa75ac7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205416(v=OCS.15)
ms:contentKeyID: 49292900
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# P2P 摘要子報表

 

_**上次修改主題的時間：** 2015-03-09_

「P2P 摘要子報表」提供失敗對等通訊工作階段的整體概觀。

## 篩選

篩選可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。下表列出您可以搭配「P2P 摘要子報表」的篩選。

### P2P 摘要子報表 篩選

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>從</strong></p></td>
<td><p>時間範圍的開始日期與時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期與時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>登錄器集區 或 Edge Server 的完整網域名稱 (FQDN)。您可選取個別集區，或按一下 [全部] 以檢查所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。UNRESOLVED_TOKEN_VAL()</p></td>
</tr>
</tbody>
</table>


## 計量

下表 P2P 摘要子報表中所提供的資訊。

### P2P 摘要子報表計量

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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>工作階段總數</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段的總數，包括成功的工作階段、失敗的工作階段 (預期失敗與未預期失敗) 以及未分類的工作階段。</p></td>
</tr>
<tr class="even">
<td><p><strong>失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>對等工作階段失敗的百分比。</p></td>
</tr>
<tr class="odd">
<td><p><strong>依形式區分的工作階段</strong></p></td>
<td><p>否</p></td>
<td><p>依形式區分的工作階段 (例如即時訊息) 總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>依形式區分的失敗率</strong></p></td>
<td><p>否</p></td>
<td><p>依形式區分的工作階段 (例如即時訊息) 失敗總數。</p></td>
</tr>
</tbody>
</table>


---
title: 會議加入時間報表
TOCTitle: 會議加入時間報表
ms:assetid: e64dc89a-25e4-4cb8-bcb1-51712e69ba5a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205344(v=OCS.15)
ms:contentKeyID: 49292634
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 會議加入時間報表

 

_**上次修改主題的時間：** 2015-03-09_

會議加入時間摘要能幫助您判斷使用者加入會議需要多長時間。報表顯示平均加入時間 (以毫秒為單位)，也提供明細，讓您了解有多少使用者能夠在 2 秒以內加入會議，有多少使用者需要 2 ~ 5 秒才能加入會議等等。

## 存取會議加入時間報表

您可從監視報告首頁存取會議加入時間報表。

## 篩選器

篩選可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。下表列出您可以搭配會議加入時間報告的篩選。

### 會議加入時間報表篩選條件

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
<p>2012/7/7 下午 1:00</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>2012/7/7</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>2012/7/3</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>20127/7 下午 1:00</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>2012/7/7</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>2012/7/3</p>
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
<p>若開始與結束日期超出所選間隔允許的上限值，將只會顯示上限值 (從開始日期開始顯示)。例如，若您選取 [每日] 間隔，並將開始與結束日期分別設為 2012/7/7 及 2012/2/28，將只會顯示 2012/8/7 上午 12:00 至 2012/9/7 上午 12:00 這段期間的資料 (亦即只會顯示 31 天的資料)。</p></td>
</tr>
<tr class="even">
<td><p><strong>[集區]</strong></p></td>
<td><p>登錄器集區或 Edge Server 的完整網域名稱 (FQDN)。您可以選取個別的集區，或是按一下 [全部] 檢視所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[會議]</strong></p></td>
<td><p>工作階段類型。允許的值為：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>Focus 工作階段</p></li>
<li><p>應用程式共用</p></li>
<li><p>A/V 會議</p></li>
</ul>
<p>若選擇 [全部]，總會議加入時間會顯示在報表上方。請注意，總會議時間僅包含以 Microsoft Exchange 或 Microsoft Outlook 安排的會議時間。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出會議加入時間報表提供的資訊。

### 會議加入時間報表評量

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
<td><p><strong>[日期]</strong></p>
<p>此評量的實際標題將視選取的間隔而異。</p></td>
<td><p>否</p></td>
<td><p>會議的執行日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>工作階段總數</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段的總數，包括成功的工作階段、失敗的工作階段 (預期失敗與未預期失敗) 以及未分類的工作階段。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[平均 (毫秒)]</strong></p></td>
<td><p>否</p></td>
<td><p>與會者加入會議的平均時間長度 (以毫秒為單位)。</p></td>
</tr>
<tr class="even">
<td><p><strong>[工作階段 &lt; 2 秒，音量]</strong></p></td>
<td><p>否</p></td>
<td><p>能夠在 2 秒內加入會議的與會者人數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[工作階段 &lt; 2 秒，百分比]</strong></p></td>
<td><p>否</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>[工作階段 2-5 秒，音量]</strong></p></td>
<td><p>否</p></td>
<td><p>能夠在 2-5 秒內加入會議的與會者人數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[工作階段 2-5 秒，百分比]</strong></p></td>
<td><p>否</p></td>
<td><p>能夠在 2-5 秒內加入會議的總通話與會者百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>[工作階段 5-10 秒，音量]</strong></p></td>
<td><p>否</p></td>
<td><p>能夠在 5-10 秒內加入會議的與會者人數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[工作階段 5-10 秒，百分比]</strong></p></td>
<td><p>否</p></td>
<td><p>能夠在 5-10 秒內加入會議的總通話與會者百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>[工作階段 &gt; 10 秒，音量]</strong></p></td>
<td><p>否</p></td>
<td><p>需要超過 10 秒才能加入會議的與會者人數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[工作階段 &gt; 10 秒，百分比]</strong></p></td>
<td><p>否</p></td>
<td><p>需要超過 10 秒才能加入會議的總通話與會者百分比。</p></td>
</tr>
</tbody>
</table>


---
title: Lync Server 2013：對等 IM 報告
TOCTitle: 對等 IM 報告
ms:assetid: 19ec0145-2398-437b-8989-f780c179b798
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558620(v=OCS.15)
ms:contentKeyID: 49290249
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的對等 IM 報告

 

_**上次修改主題的時間：** 2015-03-09_

對等 IM 報告會提供對等立即訊息 (IM) 工作階段的趨勢資訊 (依集區和驗證類型細分)。此報告可以顯示指定時段內 (例如，每天或每小時) 主控的工作階段總數，或者可以顯示該時段內傳送的立即訊息總數。

## 存取對等 IM 報告

您只要開啟＜ [Lync Server 2013 中的對等活動摘要報告](lync-server-2013-peer-to-peer-activity-summary-report.md)＞，然後按一下下列任一計量，即可存取對等 IM 報告：

  - 對等 IM 工作階段總數

  - 對等 IM 訊息總數

## 善加利用對等 IM 報告

依預設，對等 IM 報告會顯示每小時 (或每天，視您的設定而定) 的訊息計數。不過，您也可以選擇依每小時的工作階段來檢視那一天。若要執行這項作業，請按一下報告視窗右上角的 \[隱藏/顯示參數\] ，然後從 \[報告者\] 清單按一下 \[工作階段計數\] 。

## 篩選器

篩選器可以讓您傳回更精確的資料集，或者以不同方法檢視傳回的資料。下表列出您可以搭配對等 IM 報告的篩選器。

### 對等 IM 報告篩選器

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
<td><p>時間範圍的開始日期與時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月內的日期 (您不必輸入當週或該月的第一天)：</p>
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
<td><p><strong>間隔</strong></p></td>
<td><p>時間間隔。請選取下列其中一項：</p>
<ul>
<li><p>每小時 (最多可以顯示 25 個小時)</p></li>
<li><p>每日 (最多可以顯示 31 天)</p></li>
<li><p>每週 (最多可以顯示 12 週)</p></li>
<li><p>每月 (最多可以顯示 12 個月)</p></li>
</ul>
<p>若開始與結束日期超出所選間隔允許的上限值，將只會顯示上限值 (從開始日期開始顯示)。例如，若您選取 [每日] 間隔，並將開始與結束日期分別設為 2012 年 7 月 7 日及 2012 年 2 月 28 日，將只會顯示 2012 年 8 月 7 日凌晨 12 點到 2012 年 9 月 7 日凌晨 12 點這段期間的資料 (亦即只會顯示 31 天的資料)。</p></td>
</tr>
<tr class="even">
<td><p><strong>報告依據</strong></p></td>
<td><p>指定報告中所要使用的值。請選取下列其中一項：</p>
<ul>
<li><p>工作階段計數</p></li>
<li><p>訊息計數</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 對等 IM 工作階段計量 (依集區)

下表列出對等 IM 報告提供的資訊。

### 對等 IM 工作階段計量 (依集區)

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
<td><p><strong>集區</strong></p></td>
<td><p>否</p></td>
<td><p>登錄器集區或 Edge Server 的名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>日期/時間</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段的執行日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>總計</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段總數或訊息總數。</p></td>
</tr>
</tbody>
</table>


## 對等 IM 工作階段計量 (依驗證類型)

下表列出對等 IM 報告針對參與者在對等工作階段中使用之每項驗證類型所提供的資訊。

### 對等 IM 工作階段計量 (依驗證類型)

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
<td><p><strong>驗證類型</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段參與者所使用的驗證類型。一般來說，值都是下列其中之一：</p>
<ul>
<li><p>Enterprise</p></li>
<li><p>同盟</p></li>
<li><p>PIC</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>日期/時間</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段的執行日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>總計</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段總數或訊息總數。</p></td>
</tr>
</tbody>
</table>


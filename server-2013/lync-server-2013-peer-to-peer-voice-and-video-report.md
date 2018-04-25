---
title: Lync Server 2013：對等語音和視訊報告
TOCTitle: 對等語音和視訊報告
ms:assetid: e17c36b5-5a2f-4673-9696-3b2d31c2bb2f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615040(v=OCS.15)
ms:contentKeyID: 49292591
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的對等語音和視訊報告

 

_**上次修改主題的時間：** 2015-03-09_

對等語音和視訊報告會提供指定時間期間的語音與視訊電話的詳細散佈情形 (例如，每小時的通話數或每天的通話數)。該報告也提供選項，讓您檢視曾撥打的所有音訊與視訊電話，或是只檢視撥打成功或失敗的電話。報告會將顯示的通話資訊分成以下群組：

  - 每個集區的通話數

  - 每種通話類型的通話數 (例如， Lync 對 Lync 的通話與撥打給 PSTN 網路上人員的 Lync 通話)

  - 每種存取類型的通話數 (登入內部網路的使用者與登入外部網路的使用者)

  - 每個 中繼伺服器的通話數

## 存取對等語音和視訊報告

您只能透過開啟對等活動摘要報告，然後按下列的任一項計量，才能存取對等語音和視訊報告：

  - 對等音訊工作階段總數

  - 對等音訊工作階段總數

  - 對等視訊工作階段總數

  - 對等視訊分鐘總數

## 充分運用對等語音和視訊報告

有許多方式可用來篩選對等語音和視訊報告。不過，預設會隱藏檢視中的這些篩選選項。若要檢視可用的篩選選項，請按一下 \[報告\] 視窗右上角的 \[顯示/隱藏參數\] 按鈕。

## 篩選器

篩選器可以讓您傳回更精確的資料集，或是以不同方法檢視資料。下表列出可用於「對等語音和視訊報告」的篩選器。

### 對等語音和視訊報告篩選器

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
<tr class="even">
<td><p><strong>媒體類型</strong></p></td>
<td><p>指出工作階段所使用的媒體類型。請選取下列其中一項：</p>
<ul>
<li><p>兩者</p></li>
<li><p>音訊</p></li>
<li><p>視訊</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>通話處理</strong></p></td>
<td><p>指出工作階段成功與否。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>通話成功</p></li>
<li><p>通話失敗</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>報告依據</strong></p></td>
<td><p>指定報告中所要使用的值。請選取下列其中一項：</p>
<ul>
<li><p>工作階段計數</p></li>
<li><p>通話分鐘數</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 對等語音及視訊活動計量 (依集區)

下表列出每個集區「對等語音和視訊報告」中所提供的資訊。

### 對等語音及視訊活動計量 (依集區)

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
<td><p>通話所使用 登錄器集區或 Edge Server 的名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>日期/時間</strong></p></td>
<td><p>否</p></td>
<td><p>撥話的日期與時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><strong>總計</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段總數或訊息總數。</p></td>
</tr>
</tbody>
</table>


## 對等語音及視訊活動計量 (依通話類型)

下表列出每個所進行之通話類型「對等語音和視訊報告」中所提供的資訊。

### 對等語音及視訊活動計量 (依通話類型)

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
<td><p><strong>通話類型</strong></p></td>
<td><p>否</p></td>
<td><p>指出所進行的通話類型。值為下列任一項：</p>
<ul>
<li><p>UC 至 UC</p></li>
<li><p>UC 至 PSTN</p></li>
<li><p>PSTN 至 UC</p></li>
<li><p>PSTN 至 PSTN</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>日期/時間</strong></p></td>
<td><p>否</p></td>
<td><p>撥話的日期與時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><strong>總計</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段總數或訊息總數。</p></td>
</tr>
</tbody>
</table>


## 對等語音及視訊活動計量 (依存取類型)

下表列出每個網路存取類型之「對等語音和視訊報告」中所提供的資訊。

### 對等語音及視訊活動計量 (依存取類型)

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
<td><p><strong>活動類型</strong></p></td>
<td><p>否</p></td>
<td><p>指出通話時，用戶端是否登入內部網路或是外部網路。值通常為下列其中一項：</p>
<ul>
<li><p>內部</p></li>
<li><p>外部</p></li>
<li><p>混合</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>日期/時間</strong></p></td>
<td><p>否</p></td>
<td><p>撥話的日期與時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><strong>總計</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段總數或訊息總數。</p></td>
</tr>
</tbody>
</table>


## 對等語音及視訊活動計量 (依中繼伺服器)

下表列出每個 中繼伺服器「對等語音和視訊報告」中所提供的資訊。

### 對等語音及視訊活動計量 (依中繼伺服器)

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
<td><p><strong>中繼伺服器</strong></p></td>
<td><p>否</p></td>
<td><p>中繼伺服器的名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>日期/時間</strong></p></td>
<td><p>否</p></td>
<td><p>撥話的日期與時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><strong>總計</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段總數或訊息總數。</p></td>
</tr>
</tbody>
</table>


---
title: 在 Lync Server 2013 中指派每個使用者的顯示狀態原則
TOCTitle: 在 Lync Server 2013 中指派每個使用者的顯示狀態原則
ms:assetid: fd1097b7-248d-4b78-8c43-456b03257c18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182614(v=OCS.15)
ms:contentKeyID: 49292903
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中指派每個使用者的顯示狀態原則

 

_**上次修改主題的時間：** 2015-03-09_

目前狀態原則是一組會影響目前狀態的限制。下表描述 Lync Server 2013 中提供的目前狀態原則設定。

### 顯示狀態原則設定

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>XML 名稱</th>
<th>顯示名稱</th>
<th>描述</th>
<th>類型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CategorySubscriptions</p></td>
<td><p>訂閱者類別目錄訂閱數目上限</p></td>
<td><p>限制訂閱者類別目錄訂閱的數目。例如，當 Communicator 訂閱使用者的目前狀態時，它會取得各個連絡人卡片、行事曆資料、個人記事、服務和狀態類別目錄的類別目錄訂閱。</p>
<p>設定為 0 時，表示其他人無法訂閱使用者或連絡人物件。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果此設定設為較大數目，可能對效能產生相當大的影響，而且一般使用者會有大量使用者訂閱其目前狀態。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>整數</p></td>
<td><p>0-3000</p></td>
</tr>
<tr class="even">
<td><p>PromptedSubscribers</p></td>
<td><p>佇列的目前狀態訂閱警示數目上限</p></td>
<td><p>限制提示的訂閱者資料表中的項目數。此設定決定可針對特定使用者佇列的提示數目上限。例如，當使用者 A 訂閱使用者 B 的目前狀態時，使用者 B 會收到使用者 A 現已訂閱使用者 B 的提示，而且使用者 B 的提示訂閱者資料表中會建立一則確認提示。在使用者 B 接受 (或確認) 訂閱後，確認提示就會從使用者 B 的提示訂閱者資料表中移除。</p>
<p>設定為 0 時，表示不會在某人訂閱使用者的目前狀態時提示該使用者。</p></td>
<td><p>整數或 Token</p></td>
<td><p>0-500</p></td>
</tr>
</tbody>
</table>


根據預設，\[預設原則\] 和 \[服務:中\] 目前狀態原則會在您部署 Lync Server 時安裝。下表描述這兩項目前狀態原則的特殊設定。

### 目前狀態原則

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>原則名稱</th>
<th>描述</th>
<th>CategorySubscriptions</th>
<th>PromptedSubscribers</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設原則</p></td>
<td><p>一般使用者的原則。這是預設的目前狀態原則。</p></td>
<td><p>1000</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>服務:中</p></td>
<td><p>應用程式的原則，需要更多使用者訂閱物件的目前狀態。</p></td>
<td><p>1000</p></td>
<td><p>0</p></td>
</tr>
</tbody>
</table>


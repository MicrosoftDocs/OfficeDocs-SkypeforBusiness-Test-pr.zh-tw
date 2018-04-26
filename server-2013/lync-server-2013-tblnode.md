---
title: Lync Server 2013：tblNode
TOCTitle: tblNode
ms:assetid: a31d2961-aa83-4286-a12e-15d279c95f19
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615024(v=OCS.15)
ms:contentKeyID: 49291864
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblNode

 

_**上次修改主題的時間：** 2015-03-09_

在 Lync Server 2013 控制台和系統管理 Cmdlet 中管理 tblNode 時，其會包含主控台樹狀目錄 (含有類別或聊天室節點)。

### 欄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>nodeID</p></td>
<td><p>int，非 null</p></td>
<td><p>節點識別碼 (唯一號碼)。</p></td>
</tr>
<tr class="even">
<td><p>nodeGuid</p></td>
<td><p>GUID，非 null</p></td>
<td><p>節點 GUID。</p></td>
</tr>
<tr class="odd">
<td><p>parentID</p></td>
<td><p>int</p></td>
<td><p>父系的節點識別碼。根節點 (識別碼為 1) 也會包含本身做為父系。</p></td>
</tr>
<tr class="even">
<td><p>nodeType</p></td>
<td><p>位元，非 null</p></td>
<td><p>若節點是類別，則為 True。</p>
<p>若節點是聊天室，則為 False。</p></td>
</tr>
<tr class="odd">
<td><p>nodeName</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>節點名稱。</p></td>
</tr>
<tr class="even">
<td><p>nodeDesc</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>節點描述。</p></td>
</tr>
<tr class="odd">
<td><p>invite</p></td>
<td><p>bit</p></td>
<td><p>對於類別：</p>
<ul>
<li><p>若啟用 invite，則為 True。</p></li>
<li><p>若關閉 invite，則為 False。</p></li>
</ul>
<p>對於會議室：</p>
<ul>
<li><p>若關閉 invite，則為 False (覆寫父系類別)。</p></li>
<li><p>若 invite 設定是從父系類別繼承而來，則為 Null。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>logged</p></td>
<td><p>bit</p></td>
<td><p>對於類別：</p>
<ul>
<li><p>若啟用聊天記錄，則為 True。</p></li>
<li><p>若關閉聊天記錄，則為 False。</p></li>
</ul>
<p>對於會議室：</p>
<ul>
<li><p>Null。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>filePost</p></td>
<td><p>bit</p></td>
<td><p>對於類別：</p>
<ul>
<li><p>若允許檔案上傳，則為 True。</p></li>
<li><p>若不允許檔案上傳，則為 False。</p></li>
</ul>
<p>對於會議室：</p>
<ul>
<li><p>Null。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>disabled</p></td>
<td><p>位元，非 null</p></td>
<td><p>若停用聊天室，則為 True。僅適用於聊天室。(若是類別，則為 False。)</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>行為</p></td>
<td><p>smallint，非 null</p></td>
<td><p>行為 (在 EnumValue 表格中查閱)：</p>
<ul>
<li><p>4：一般 (一般聊天室)。</p></li>
<li><p>5：視聽中心 (視聽中心聊天室，只有報告者能張貼訊息)。</p></li>
</ul>
<p>僅套用至聊天室。</p></td>
</tr>
<tr class="odd">
<td><p>可見度</p></td>
<td><p>smallint，非 null</p></td>
<td><p>可見度 (在 EnumValue 表格中查閱)：</p>
<ul>
<li><p>2：私人</p></li>
<li><p>3：範圍內</p></li>
<li><p>6：開放</p></li>
</ul>
<p>僅套用至聊天室。</p></td>
</tr>
<tr class="even">
<td><p>siopID</p></td>
<td><p>GUID</p></td>
<td><p>增益集 GUID，若有增益集與聊天室相關連的話 (類別沒有增益集)。</p>
<p>系統會在 SiopWhiteList 表格中尋找增益集資訊。</p></td>
</tr>
<tr class="odd">
<td><p>nodeAddedBy</p></td>
<td><p>int，非 null</p></td>
<td><p>建立此節點之主體的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>nodeAddedOn</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>節點建立的時間戳記。</p></td>
</tr>
<tr class="odd">
<td><p>nodeUpdatedBy</p></td>
<td><p>int，非 null</p></td>
<td><p>最近一次更新節點之主體的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>nodeUpdatedOn</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>最近一次節點更新的時間戳記。</p></td>
</tr>
<tr class="odd">
<td><p>purgedOn</p></td>
<td><p>datetime</p></td>
<td><p>最近一次影響此節點之清除作業 (從 tblScopedPrincipal 表格移除範圍，從 tblPrincipalRole 表格移除角色) 的時間。為聊天服務的內部快取更新機制所用。</p></td>
</tr>
</tbody>
</table>


### 索引鍵

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>nodeID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>行為</p></td>
<td><p>在 tblEnumValue.valueID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="odd">
<td><p>可見度</p></td>
<td><p>在 tblEnumValue.valueID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>parentID</p></td>
<td><p>在 tblNode.nodeID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="odd">
<td><p>siopID</p></td>
<td><p>在 tblSiopWhiteList.siopId 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>


---
title: Lync Server 2013：tblPrincipal
TOCTitle: tblPrincipal
ms:assetid: 79a24502-b4ce-41f0-8979-8caddf535338
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558667(v=OCS.15)
ms:contentKeyID: 49291396
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipal

 

_**上次修改主題的時間：** 2015-03-09_

tblPrincipal 包含所有主體，包括使用者、資料夾及群組。

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
<td><p>prinID</p></td>
<td><p>int，非 null</p></td>
<td><p>主體識別碼。</p></td>
</tr>
<tr class="even">
<td><p>prinGuid</p></td>
<td><p>GUID，非 null</p></td>
<td><p>主體 GUID。因為它的意義橫跨 Active Directory 網域服務 空間，因此會廣泛做為替代的主索引鍵。(快取主體的 GUID 相等於對應之 Active Directory 物件的 GUID。)</p></td>
</tr>
<tr class="odd">
<td><p>prinUri</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>主體 URI。SIP 配置可用於使用者，而 ma-grp 幾乎可用於其他所有項目。</p></td>
</tr>
<tr class="even">
<td><p>prinName</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>一般名稱。僅可用於使用者類型。</p></td>
</tr>
<tr class="odd">
<td><p>prinDisplayName</p></td>
<td><p>Nvarchar (256)</p></td>
<td><p>顯示名稱。僅可用於使用者類型。</p></td>
</tr>
<tr class="even">
<td><p>prinCompanyName</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>公司名稱。僅可用於使用者類型。</p></td>
</tr>
<tr class="odd">
<td><p>prinEmail</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>電子郵件。僅可用於使用者類型。</p></td>
</tr>
<tr class="even">
<td><p>prinADPath</p></td>
<td><p>nvarchar(384)</p></td>
<td><p>Active Directory 物件 (主體為快取版本) 的網域名稱。非 Active Directory 物件的類型可以是 Null (例如系統使用者)。</p></td>
</tr>
<tr class="odd">
<td><p>prinADUserPrincipalName</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>使用者的使用者主體名稱 (UPN)。僅可用於一般使用者類型。</p></td>
</tr>
<tr class="even">
<td><p>prinDisabled</p></td>
<td><p>smallint，非 null</p></td>
<td><ul>
<li><p>0：主體為作用中狀態。</p></li>
<li><p>1：主體已停用，因為使用者的 SIP 功能已停用。</p></li>
<li><p>2：主體已刪除，因為相關聯的 AD 物件已刪除。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>prinTypeID</p></td>
<td><p>smallint，非 null</p></td>
<td><p>主體類型 (參照 tblPrincipalType 表格)。</p></td>
</tr>
<tr class="even">
<td><p>prinPoolID</p></td>
<td><p>Int</p></td>
<td><p>適用於主體的 Lync 集區指派。</p></td>
</tr>
<tr class="odd">
<td><p>prinPolicyID</p></td>
<td><p>Int</p></td>
<td><p>如果出現標記類型原則，即為適用於使用者的 常設聊天室伺服器 原則值。</p></td>
</tr>
<tr class="even">
<td><p>prinAddedBy</p></td>
<td><p>int</p></td>
<td><p>建立者的主體識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>prinAddedOn</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>建立時間的時間戳記。</p></td>
</tr>
<tr class="even">
<td><p>prinUpdatedBy</p></td>
<td><p>int</p></td>
<td><p>最近一次進行更新之主體的識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>prinUpdatedOn</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>最近一次更新的時間戳記。</p></td>
</tr>
<tr class="even">
<td><p>prinVerifiedOn</p></td>
<td><p>日期時間，非 null</p></td>
<td><p>最近一次主體之 Active Directory Sync 重新整理的日期與時間。</p></td>
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
<td><p>prinID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>prinTypeID</p></td>
<td><p>在 tblPrincipalType.ptypeID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>


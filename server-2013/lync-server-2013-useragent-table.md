---
title: Lync Server 2013：UserAgent 表格
TOCTitle: UserAgent 表格
ms:assetid: d6bda1c0-b053-457a-9ffa-2ae859788775
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398939(v=OCS.15)
ms:contentKeyID: 49292478
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 UserAgent 表格

 

_**上次修改主題的時間：** 2015-03-09_

UserAgent 表格是一種支援表格，其中儲存資料庫中已參與工作階段記錄的各個使用者代理程式清單。表格中的每筆記錄都代表一個使用者代理程式。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UserAgentKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別此使用者代理程式且不重複的號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserAgent</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>使用者代理程式字串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UAType</strong></p></td>
<td><p>smallint</p></td>
<td><p> </p></td>
<td><p>1 是中繼伺服器。</p>
<p>2 是 A/V 會議伺服器。</p>
<p>4 是 Lync。</p>
<p>8 是 IP 電話。</p>
<p>16 是 Live Meeting 主控台。</p>
<p>32 是部署驗證工具 (Deployment Validation Tool, DVT)。</p>
<p>64 是 Macintosh 電腦上的 Lync。</p>
<p>128 是 Office Communications Server 2007 R2 Attendant。</p>
<p>256 是會議宣告服務。</p>
<p>512 是會議自動語音應答。</p>
<p>1024 是回應群組應用程式。</p>
<p>2048 是外部語音控制。</p></td>
</tr>
</tbody>
</table>


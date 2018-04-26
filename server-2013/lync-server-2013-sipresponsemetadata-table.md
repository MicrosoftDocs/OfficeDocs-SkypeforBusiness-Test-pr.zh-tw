---
title: Lync Server 2013 中的 SIPResponseMetaData 表
TOCTitle: Lync Server 2013 中的 SIPResponseMetaData 表
ms:assetid: cf723737-4a75-4352-829b-f4954aa59716
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205294(v=OCS.15)
ms:contentKeyID: 49292368
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SIPResponseMetaData 表

 

_**上次修改主題的時間：** 2015-03-09_

SIPResponseMetaDataTable 包含 SIP 回應碼清單及各個代碼的分類與定義。這些代碼是為了回應影響 SIP 裝置與 SIP 通訊工作階段的事件而產生；例如，當 SIP 裝置發出要求，但伺服器拒絕執行該要求，就會產生回應碼 403。

本表在 Microsoft Lync Server 2013 中介紹過。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>索引鍵/索引</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>回應碼</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>代表 IP 回應碼的數值。</p></td>
</tr>
<tr class="even">
<td><p><strong>類別</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>回應碼的一般分類。分類包括：</p>
<ul>
<li><p>1 – 資訊回應</p></li>
<li><p>2 – 成功回應</p></li>
<li><p>3 – 重新導向回應</p></li>
<li><p>4 – 用戶端失敗回應</p></li>
<li><p>5 – 伺服器失敗回應</p></li>
<li><p>6 – 全域失敗回應</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>描述</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>描述 SIP 回應碼。例如，回應碼 181 的描述如下：</p>
<p>已轉接通話</p></td>
</tr>
</tbody>
</table>


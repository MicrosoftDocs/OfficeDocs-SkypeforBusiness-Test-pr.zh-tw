---
title: Lync Server 2013：常設聊天室伺服器規範表的清單
TOCTitle: 常設聊天室伺服器規範表的清單
ms:assetid: 8563446e-90cc-47cc-8a8e-4883decfe195
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215878(v=OCS.15)
ms:contentKeyID: 49291538
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中常設聊天室伺服器規範表的清單

 

_**上次修改主題的時間：** 2015-03-09_

常設聊天室規範資料庫結構描述由下列表格所組成。

## 常設聊天室伺服器 規範表格清單


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblcompliancedata.md">Lync Server 2013 中的 tblComplianceData</a></p></td>
<td><p>包含所有設定的介面卡尚未處理的規範事件。</p>
<p>此表格包含 常設聊天室 的事件，例如聊天訊息及檔案下載。(tblComplianceParticipant 表格會追蹤參與者事件。)</p>
<p>(將此表格中的事件加以處理的伺服器會列在 tblComplianceFanout 表格中。)</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblcompliancefanout.md">Lync Server 2013 中的 tblComplianceFanout</a></p></td>
<td><p>包含已處理規範事件的伺服器。此表格必須緊密搭配 tblComplianceData 表格。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblcomplianceparticipant.md">Lync Server 2013 中的 tblComplianceParticipant</a></p></td>
<td><p>包含每個交談服務和每部伺服器的目前參與者。其會依據從 常設聊天室服務所接收的加入與離開規範事件進行維護。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblcompliancestate.md">Lync Server 2013 中的 tblComplianceState</a></p></td>
<td><p>包含整個集區的規範狀態資訊。</p></td>
</tr>
</tbody>
</table>


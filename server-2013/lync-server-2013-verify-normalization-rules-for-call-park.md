---
title: Lync Server 2013：驗證通話駐留的正規化規則
TOCTitle: 驗證通話駐留的正規化規則
ms:assetid: deaa170f-041e-45cb-8eab-f02931ab541e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398981(v=OCS.15)
ms:contentKeyID: 49292545
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中驗證通話駐留的正規化規則

 

_**上次修改主題的時間：** 2012-09-11_

通話駐留軌道不可正規化。檢查撥號對應表以確認軌道號碼沒有正規化。如果您必須建立其他正規化規則以防止將軌道正規化，請依照[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)中的程序，定義新的正規化規則，以便 \[要比對的模式\] 識別軌道範圍，且 \[轉譯模式\] 為 **$1**。例如，如果您的通話駐留軌道範圍是 7000 – 7999，則 \[要比對的模式\] 為 **^(7\\d{3})$**，且 \[轉譯模式\] 為 **$1**。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>確認撥號對應表中的預設正規化規則未包含 <strong>^(\d*)</strong>。否則，您的 通話駐留正規化規則將永遠不會執行。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)


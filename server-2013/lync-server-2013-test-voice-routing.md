---
title: Lync Server 2013：測試語音路由
TOCTitle: 測試語音路由
ms:assetid: d3aae909-fef6-440f-b144-0b62dc82bf5d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398915(v=OCS.15)
ms:contentKeyID: 49292412
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中測試語音路由

 

_**上次修改主題的時間：** 2013-02-24_

您可以使用 Lync Server 控制台**\[測試語音路由\]** 索引標籤來設定測試案例。若要定義測試案例，需要指定要對其測試指定之電話號碼的撥號對應表、語音原則、PSTN 使用方式和語音路由。

在實際部署語音路由設定之前，建議您先使用不同的電話號碼測試，以確認可達成您所預期的結果。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用 <strong>[匯出測試案例]</strong> 和 <strong>[匯入測試案例]</strong> 命令來儲存語音路由測試案例，並將它們匯入其他電腦上使用。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您刪除任一部分的語音路由設定 (例如撥號對應表、語音原則、語音路由或電話使用方式)，則應該檢閱並更新您的語音路由測試案例。如果測試案例由於設定變更而不再有效， Lync Server 控制台將不會通知您。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中建立語音路由測試案例](lync-server-2013-create-a-voice-routing-test-case.md)

  - [在 Lync Server 2013 中匯出語音路由測試案例](lync-server-2013-export-voice-routing-test-cases.md)

  - [在 Lync Server 2013 中改善語音路由測試案例](lync-server-2013-import-voice-routing-test-cases.md)

  - [在 Lync Server 2013 中執行語音路由測試](lync-server-2013-running-voice-routing-tests.md)


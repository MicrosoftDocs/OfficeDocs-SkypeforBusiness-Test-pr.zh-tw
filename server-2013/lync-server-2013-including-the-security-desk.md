---
title: Lync Server 2013：加入安全性桌面
TOCTitle: 加入安全性桌面
ms:assetid: 4b1d9125-7488-419b-85dd-a8dd3ab5add3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398299(v=OCS.15)
ms:contentKeyID: 49290840
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中加入安全性桌面

 

_**上次修改主題的時間：** 2012-10-02_

您的公司可能需要警衛室介入處理緊急通話。為了協助決定如何將警衛室整合至 E9-1-1 部署，您應該回答下列問題。

  - **您是否希望在有人撥打緊急通話時通知警衛室？**  
    您可以設定位置原則，讓 Lync Server 傳送立即訊息 (IM) 通知給一或多位安全人員的 Lync SIP 位址。這些通知包含撥打緊急電話的人員名稱、號碼及位置，以加速安全人員協助處理緊急狀況。

<!-- end list -->

  - **您想要針對每一通緊急通話都邀請警衛室參加會議嗎？**  
    只要緊急服務服務提供者有支援，您可以設定位置原則，以隨每通緊急通話附上回撥號碼。然後提供者就會針對緊急電話，使用此號碼來召集您組織的安全人員開會。此會議可在位置原則中設定為單向 (只能聆聽) 或雙向。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必要時，您可以為每個位置原則設定不同的緊急人員。這樣可讓您針對公司內的不同區域自訂回應，或針對來自網路內部和外部的緊急電話分別建立不同的行為。您可以使用通訊群組來指定想要通知的人員。</td>
</tr>
</tbody>
</table>


---
title: 移轉封存和監控伺服器
TOCTitle: 移轉封存和監控伺服器
ms:assetid: 77831579-df45-4697-b8c5-207b74a07a40
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205015(v=OCS.15)
ms:contentKeyID: 49291370
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉封存和監控伺服器

 

_**上次修改主題的時間：** 2012-10-02_

如果您已在 Lync Server 2010 環境中部署存封伺服器和監控伺服器，當您移轉前端集區後，可以在 Lync Server 2013 環境中部署這些伺服器。然而，如果存封和監控功能對您的組織而言十分重要，在移轉之前，您應將存封和監控新增至 Lync Server 2013 試驗集區，以確保在移轉過程期間能夠使用該功。

移轉過程中，如果您需要存封和監控功能，請記住以下注意事項：

  - 存封資料和監控資料不會移動至 Lync Server 2013 部署。您解除委任舊版環境之前所備份的資料，將會是您在 Lync Server 2010 環境中的活動歷程記錄。

  - 存封伺服器和監控伺服器的 Lync Server 2010 版本僅能與 Lync Server 2010 前端集區相關聯。在 Lync Server 2013 中，存封和監控不再扮演伺服器的角色，而是成為與 Lync Server 2013 前端集區整合的服務。

  - 在舊版與 Lync Server 2013 部署並存期間， Lync Server 2010 版本的存封伺服器和監控伺服器會收集位於 Lync Server 2010 集區之使用者的資料。 Lync Server 2013 中的存封和監控收集位於 Lync Server 2013 集區之使用者的資料。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>移轉階段期間，如果您仍使用具有新 Lync Server 2013 試驗集區的舊版 Edge Server， Lync Server 2010 版本的存封伺服器將持續收集位於 Lync Server 2010 集區之使用者的資料，而 Lync Server 2013 中的存封將收集位於 Lync Server 2013 集區中之使用者的資料。</td>
    </tr>
    </tbody>
    </table>


  - 如果您在 Lync Server 2013 中搭配存封和監控使用協力廠商的存封與監控解決方案；請諮詢您的廠商，以了解您整合 Lync Server 2013 協力廠商解決方案的時機和方法。


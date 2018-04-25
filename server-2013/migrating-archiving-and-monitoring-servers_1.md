---
title: 移轉封存和監控伺服器
TOCTitle: 移轉封存和監控伺服器
ms:assetid: 8d879253-ad76-42b7-8386-e44b110239cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688124(v=OCS.15)
ms:contentKeyID: 49890199
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉封存和監控伺服器

 

_**上次修改主題的時間：** 2012-10-02_

您的 Office Communications Server 2007 R2 中如有部署封存伺服器及監控伺服器，可以在移轉前端集區之後，於 Lync Server 2013 環境中部署這兩部伺服器。倘若封存及監控功能對於貴組織極為重要，您應在移轉之前，先將封存及監控加入您的試驗集區，讓這兩項功能在移轉期間仍能如常運作。

若希望在移轉共存階段期間繼續提供封存及監控功能，請牢記下列注意事項：

  - 封存資料與監控資料不會移至 Lync Server 2013 部署。在解除委任舊版環境之前所備份的資料，將會是 Office Communications Server 2007 R2 中的活動記錄。

  - 存封伺服器和監控伺服器的 Office Communications Server 2007 R2 版本僅能與 Office Communications Server 2007 R2 前端集區相關聯。在 Lync Server 2013 中，存封和監控不再扮演伺服器的角色，而是成為與 Lync Server 2013 前端集區整合的服務。

  - 在舊版部署與 Lync Server 2013 部署共存期間， Office Communications Server 2007 R2 版的封存伺服器與監控伺服器會收集位於 Office Communications Server 2007 R2 集區上之使用者的資料。 Lync Server 2013 版的封存伺服器與監控伺服器則會收集位於 Lync Server 2013 集區上之使用者的資料。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您在移轉階段使用舊版 Edge Server 搭配新的 Lync Server 2013 試驗集區使用， Office Communications Server 2007 R2 版的封存伺服器將會繼續收集位於 Office Communications Server 2007 R2 集區上之使用者的資料，而 Lync Server 2013 版的封存取伺服器則會收集位於 Lync Server 2013 集區上之使用者的資料。</td>
    </tr>
    </tbody>
    </table>


  - 若要將第三方封存與監控解決方案，和封存伺服器及監控伺服器搭配使用，請洽詢相關廠商，了解整合第三方解決方案與 Lync Server 2013 的方法及時機。


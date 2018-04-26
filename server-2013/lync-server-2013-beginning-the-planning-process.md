---
title: Lync Server 2013：開始規劃程序
TOCTitle: 開始規劃程序
ms:assetid: df3722b3-f859-49e1-b3ff-ee6863483731
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398986(v=OCS.15)
ms:contentKeyID: 49292561
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 開始 Lync Server 2013 的規劃程序

 

_**上次修改主題的時間：** 2014-11-07_

儘管規劃內部部署整合通訊部署可能有些聲勢浩大，但是 Lync Server 提供了兩種非常有用的工具來協助您：

  - **規劃工具**是一個精靈，提供一系列與組織相關的問題、要啟用的 Lync Server 功能以及容量規劃需求。接著，它會根據您的回答來建立建議的部署拓撲，並產生此一部署的 Microsoft Visio 圖表。

  - **拓撲產生器**是 Lync Server 的安裝元件。您可以使用 拓撲產生器 建立、調整和發佈規劃的拓撲。它也能在開始安裝伺服器之前驗證您的拓撲。在個別伺服器上安裝 Lync Server 時，這些伺服器會在安裝過程中讀取發佈的拓撲，而且安裝程式會依照拓撲的指示來部署伺服器。

## Lync Server 規劃工具

規劃工具在工具中採取您對問題的回答，並基於 Lync Server 準則和最佳實作方案產生一個拓撲，還根據答案提供多個部署檢視。同時，顯示一個所有網站的全局檢視 (即包括中央網站和分支網站) 和顯示各網站中伺服器和其他元件的詳細檢視。

執行 規劃工具時，不會認可任何特定部署或啟動任何程序。事實上，在制定明確規劃之前執行 規劃工具，對瞭解需要在規劃程序期間考量的問題類型具有指導性。

您可以多次執行 規劃工具，採用不同的方式回答問題，並比較成果。如果您對某個設計基本滿意，但是需要進行一些變更，則可以回到 規劃工具，載入設計，然後進行變更。完成 規劃工具一次，大約需要 15 分鐘。

滿意之後，您可以使用 規劃工具來建立規劃部署的圖表。在以 拓撲產生器建立部署時，您可以使用此圖表。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這個 Lync Server 2013 版本隨附的規劃工具是發行前版本。請注意，規劃工具中的容量規劃數字是初步數字，不受最終版本支援。</td>
</tr>
</tbody>
</table>


## Lync Server 拓撲產生器

在您的部署計劃定案之後，您可以使用 拓撲產生器開始進行部署。感到滿意之後，可以使用 拓撲產生器驗證拓撲，然後在拓撲通過驗證之後將其發佈出來。發佈拓撲時， Lync Server 會將拓撲置於 中央管理存放區中，如果拓撲尚不存在，就會在此時建立。部署期間在各伺服器上安裝 Lync Server 時，伺服器會從 中央管理存放區 讀取拓撲，並自行進行安裝為部署中適合自己的角色。

或者，如果您對 Lync Server 非常熟悉，並且不需要規定性準則，則可以跳過 規劃工具，然後使用 拓撲產生器中的精靈開始設計部署、進行驗證和發佈。

使用 拓撲產生器規劃和發佈拓撲是一個必要步驟。在部署期間，您不能略過 拓撲產生器並在伺服器上單獨安裝 Lync Server。每部伺服器都必須從 中央管理存放區中已驗證、已發佈的拓撲讀取該拓撲。

## 高階規劃程序

我們建議在以下一般程序中同時使用文件和 規劃工具，規劃 Lync Server 部署。

1.  如果您非常熟悉舊版的 Lync Server，請閱讀＜ [Lync Server 2013 中的新功能](lync-server-2013-new-features.md)＞，以瞭解 Lync Server 2013 的新功能和需求。

2.  閱讀本節中的其他主題：＜ [規劃 Lync Server 2013 前必須知道的拓撲基本知識](lync-server-2013-topology-basics-you-must-know-before-planning.md)＞、＜ [Lync Server 2013 中的參考拓撲](lync-server-2013-reference-topologies.md)＞、＜ [Lync Server 2013 的初始規劃決策](lync-server-2013-initial-planning-decisions.md)＞以及＜ [Lync Server 2013 的用戶端](lync-server-2013-clients.md)＞。記下＜ [Lync Server 2013 中的參考拓撲](lync-server-2013-reference-topologies.md)＞中呈現的規劃決策。

3.  既然您對 Lync Server 功能和必須回答的問題類型有了更加深入的瞭解，請執行 規劃工具，並檢視產生的拓撲和詳細資訊。確定該拓撲符合組織的獨特需求。

4.  如果您需要瞭解特定的工作負載或功能，或對其感興趣，請閱讀[規劃 Lync Server 2013](lync-server-2013-planning.md)中的相應章節。

5.  再次執行 規劃工具。您可以開始在步驟 3 中建立的部署，並修改結果，或從頭開始。
    
    若有必要，請再次執行 規劃工具，不斷重複，直到您對輸出滿意為止。

6.  當您完成拓撲規劃時，請使用 規劃工具來建立和列印拓撲的 Visio 圖表。您可以在使用 拓撲產生器輸入拓撲時使用此列印成品。

7.  開始部署之前，請閱讀＜ [判定 Lync Server 2013 的系統需求](lync-server-2013-determining-your-system-requirements.md)＞及＜ [判斷 Lync Server 2013 的基礎結構需求](lync-server-2013-determining-your-infrastructure-requirements.md)＞，瞭解 Lync Server 的先決條件和必要基礎結構。此外，請務必閱讀《 [規劃 Lync Server 2013](lync-server-2013-planning.md)》中適用於規劃部署的工作量和功能的所有章節。

## 從舊版移轉

如果您從舊版移轉至 Lync Server，請參閱＜ [移轉](migration.md)＞文件中用於移轉和部署的特定指示。


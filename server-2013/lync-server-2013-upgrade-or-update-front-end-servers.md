---
title: 在 Lync Server 2013 中升級或更新前端伺服器
TOCTitle: 在 Lync Server 2013 中升級或更新前端伺服器
ms:assetid: 20fa39ae-ecfb-4c72-9cc4-8e183d3c752f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204736(v=OCS.15)
ms:contentKeyID: 49290315
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中升級或更新前端伺服器

 

_**上次修改主題的時間：** 2013-06-28_

Enterprise Edition Pool 中的前端伺服器會組織成*升級網域*。這些升級網域都是集區中前端伺服器的子集，且 拓撲產生器會自動建立升級網域。

在升級伺服器時，請務必一次僅進行單一升級網域的作業。先關閉升級網域的某部伺服器、加以升級，然後重新啟動，再繼續進行其他升級網域的作業。同時也必須記錄清楚哪些升級網域和伺服器已經升級過了。升級每部伺服器時，請使用以下的流程圖圖表。

![升級伺服器流程圖](images/JJ204736.42ed59a4-1c26-49f7-ade4-a5a788457ab9(OCS.15).jpg "升級伺服器流程圖")

## 套用升級至集區中的前端伺服器

1.  在集區中的前端伺服器上，執行下列 Cmdlet：
    
    **Get-CsPoolUpgradeReadinessState**
    
    若 *PoolUpgradeState* 的值為 **Busy**，請等候 10 分鐘，然後再重新嘗試 **Get-CsPoolUpgradeReadinessState**。若您至少連續三次都看到 **Busy**，請在每次嘗試之間都等候 10 分鐘，或者，若您看到 **PoolUpgradeState,** 的結果是 **InsufficientActiveFrontEnds**，就表示集區發生問題。若集區是與災害復原拓撲中的前端集區搭配運作，您就應該將集區容錯移轉至備用集區，然後再更新此集區中的伺服器。如需詳細資訊，請參閱＜[在 Lync Server 2013 中容錯移轉集區](lync-server-2013-failing-over-a-pool.md)＞。
    
    若 *PoolUpgradeState* 的值是 **Ready**，請前往步驟 2。

2.  **Get-CsPoolUpgradeReadinessState** Cmdlet 也會傳回集區中每個升級網域以及每個升級網域中有哪些前端伺服器的相關資訊。若包含您欲升級之伺服器的升級網域的 **ReadyforUpgrade** 值為 **True**，您就可以放心升級這些伺服器。若要執行這項作業，請執行下列動作：
    
    1.  使用 `Stop-CsWindowsService -Graceful -Verbose` Cmdlet 停止要升級之前端伺服器的新連線。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您要在排定的伺服器停機時間進行這些伺服器的升級，可以執行此 Cmdlet 但不加上 ‘-<strong>Graceful</strong>‘ 參數，如下所示：<strong>Stop-CsWindowsService</strong>。如此將會立即關閉服務，而不會等候全部現有服務要求完成。</td>
        </tr>
        </tbody>
        </table>
    
    2.  為與此升級網域關聯的伺服器進行升級。
    
    3.  重新啟動伺服器，並確保伺服器接受新的連線。

3.  為集區中每個其他升級網域重複步驟 1 和 2，直到所有 前端伺服器 都已升級為止。


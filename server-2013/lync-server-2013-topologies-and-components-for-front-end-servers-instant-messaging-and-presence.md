---
title: Lync Server 2013：前端伺服器、立即訊息及顯示狀態的拓撲和元件
TOCTitle: 前端伺服器、立即訊息及顯示狀態的拓撲和元件
ms:assetid: f08ce7a1-d14e-4a54-9771-a82c870658bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412996(v=OCS.15)
ms:contentKeyID: 49292766
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的拓撲和元件

 

_**上次修改主題的時間：** 2015-05-04_

立即訊息 (IM) 和目前狀態需要的元件只有：

  - 您組織的前端伺服器或 Standard Edition Server。IM 和目前狀態功能一定會在這些伺服器上啟用。

  - 負載平衡器，如果您有 Enterprise Edition前端集區。如需詳細資訊，請參閱 [Lync Server 2013 中的負載平衡需求](lync-server-2013-load-balancing-requirements.md)。

## 前端集區的部署規劃

在 Lync Server 2013 中， 前端集區 架構已變更，這些變更會影響規劃及維護 前端集區 的方式。

我們建議所有的 Enterprise Edition前端集區 至少要包含三個前端伺服器。在 Lync Server 中， 前端集區 的架構使用分散式系統模型，集區中三部前端伺服器都有每個使用者的資料。如需此新架構的詳細資訊，請參閱 [Lync Server 2013 中的拓撲變更](lync-server-2013-topology-changes.md)。

如果您不想不部署三個 Enterprise Edition前端伺服器 而想要災難復原，我們建議使用 Lync ServerStandard Edition 並建立兩個有配對備份關係的集區。如此，僅有兩個伺服器時，也可提供災難復原解決方案。如需高可用性與災難復原之拓撲與功能的詳細資訊，請參閱 [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)。

## 前端集區的管理規劃

若是 前端集區，請遵守本節中的指導方針。

## 確認該集區可運作

使用 前端集區 新的分散式模型，必須執行特定數量的集區伺服器才能使集區正常運作。一個集區有兩個遺失模式

  - 因特定路由群組的複本伺服器不足所導致的路由群組層級仲裁遺失。路由群組是一組位於集區之使用者的彙總。每個路由群組在集區中皆有三個複本：一個主要複本和兩個次要複本。

  - 因集區中執行的種子伺服器不足所導致的集區層級仲裁遺失。

## 路由群組層級仲裁遺失

第一次啟動新的 前端集區 時，基本上必須要有 85% 的伺服器執行運作，如下表所示。若僅有少數伺服器執行，服務可能會停滯在啟動狀態，集區也可能不會啟動。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>集區伺服器的總數</th>
<th>第一次啟動集區時必須執行的伺服器數目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>3</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>5</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>5</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>6</p></td>
</tr>
<tr class="even">
<td><p>9</p></td>
<td><p>7</p></td>
</tr>
<tr class="odd">
<td><p>10</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>11</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>12</p></td>
<td><p>10</p></td>
</tr>
</tbody>
</table>


集區啟動後的後續時間，必須要有 85% 的伺服器啟動 (如先前表格所示)。若無法啟動此數目的伺服器 (但有足夠的伺服器可啟動，讓您不至於面臨仲裁遺失的狀態)，您可以使用 **Reset-CsPoolRegistrarState –ResetType QuorumLossRecovery** cmdlet，讓集區從此路由群組層級仲裁遺失中復原並有所進展。若需更多如何使用 cmdlet 的相關資訊，請參閱[Reset-CsPoolRegistrarState](reset-cspoolregistrarstate.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於 Lync Server 使用主要 SQL 資料庫作為見證，因此如果您關閉主要資料庫並切換至鏡像複本，然後關閉足夠的 前端伺服器，則根據先前的表格，執行的伺服器會不足，而整個集區將會關閉。如需詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/?linkid=393672">資料庫鏡像見證</a>。</td>
</tr>
</tbody>
</table>


## 集區層級仲裁遺失

若要 前端集區 正常運作，則其不能處於集區層級仲裁遺失。如果執行的伺服器數低於此表格顯示的最低正常運作層級，則集區中其餘伺服器將會停止所有 Lync Server 服務。請注意，下表中的數字是假設集區中的後端伺服器皆在執行中。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>集區中的前端伺服器總數</th>
<th>集區正常運作所需的伺服器數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>3-4</p></td>
<td><p>任 2</p></td>
</tr>
<tr class="odd">
<td><p>5-6</p></td>
<td><p>任 3</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>任 4</p></td>
</tr>
<tr class="odd">
<td><p>8-9</p></td>
<td><p>前 7 部伺服器中的任 4 部</p></td>
</tr>
<tr class="even">
<td><p>10-12</p></td>
<td><p>前 9 部伺服器中的任 5 部</p></td>
</tr>
</tbody>
</table>


在先前的表格中，「最先的伺服器」是當集區第一次啟動時按時間先後順序最先啟動的伺服器。若要判斷這些伺服器，您可以使用 **Get-CsComputer** cmdlet 與 **–PoolFqdn** 選項。這個 Cmdlet 會依伺服器在拓樸中顯現的順序來顯示伺服器，而在清單頂端的伺服器就是最先的伺服器。

## 有兩個前端伺服器的前端集區

我們不建議部署僅包含兩個前端伺服器的前端集區。如果您還是需要部署這樣的集區，請遵循下列指南：

  - 如果兩個前端伺服器其中一部停機，應盡快重新開啟當機的伺服器。同理，如果需要升級兩部伺服器的其中一部，必須在完成升級後盡快使這部伺服器復原上線。

  - 如果您基於某些理由，必須同時讓兩部伺服器停機，請在集區停機完成後進行下列步驟：
    
      - 最佳做法是同時重新啟動兩部前端伺服器。
    
      - 如果無法同時重新啟動兩部伺服器，應依照停機時的相反順序重新開機。
    
      - 如果無法以相反順序重新開機，請先使用下列 Cmdlet 再重新將集區開機。
        
            Reset-CsPoolRegistrarState -ResetType QuorumLossRecovery -PoolFQDN <FQDN>

## 確保集區正常運作的其他步驟

您應查看其他幾個因素來確保您的 前端集區 維持正常運作。

  - 第一次將使用者移至集區時，請確定至少正在執行三部前端伺服器。

  - 如果基於災難復原目的而建立此集區與另一個集區的配對關係，則建立關係後，必須確認此集區正同時執行三部前端伺服器，以便與備份集區同步處理資料。如需集區配對與災難復原功能的詳細資訊，請參閱 [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)＞。

## 改善集區升級的可靠性

當您需要在 前端集區 升級或修補伺服器時，請按照[在 Lync Server 2013 中升級或更新前端伺服器](lync-server-2013-upgrade-or-update-front-end-servers.md)中的工作流程，與以下指南進行：

  - 當您按照[在 Lync Server 2013 中升級或更新前端伺服器](lync-server-2013-upgrade-or-update-front-end-servers.md)中的工作流程，在升級網域間移動以升級時，您會用到**Get-CsPoolUpgradeReadinessState** cmdlet 並查看是否為 \[就緒\] 狀態。當顯示為 \[就緒\] 狀態後，等待 20 分鐘再進行下次更新，能使更新更具可靠性。如果在這 20 分鐘內，狀態變成 \[未就緒\]，請重新啟動 20 分鐘計時器。此外，您也可以在 20 分鐘間隔前或後執行 **Get-CsPoolFabricState** cmdlet，確定主要與次要路由群組沒有變更。

  - 如果上個修補升級網域停滯或沒有重新啟動，請不要前往下一個升級網域。如果升級中有任何伺服器無法啟動，也請這樣處理。執行 **Get-CsPoolFabricState** 以確保所有路由群組都擁有主要路由群組，及至少一個次要路由群組；這能確認是否所有使用者都擁有服務。

  - 如果只有部分使用者擁有服務，請搭配 –Verbose 選項執行 **Get-CsPoolFabricState**，檢查出缺少複本的路由群組。請勿將重新啟動整個集區做為疑難排解的第一個步驟。如需更多關於此 cmdlet 的資訊，請參閱[Get-CsPoolFabricState](get-cspoolfabricstate.md)。

  - 請確定 \[事件檢視器 \] 或 \[效能監視器\] 視窗的所有執行個體都已關閉，以進行 Windows Fabric 安裝/解除安裝。

## 變更前端集區的設定

每當將前端伺服器新增至集區或從集區中移除，並發佈新拓撲時，請遵循下列指南：

  - 發佈新拓撲時，必須重新啟動集區中每個 前端伺服器。一次重新啟動一部。

  - 如果變更設定時，整個集區停機，請在發佈新拓撲後執行下列 Cmdlet：
    
        Reset-CsPoolRegistrarState -PoolFQDN <PoolFQDN> -ResetType ServiceReset

如果前端伺服器當機，也不太可能在幾天內更換，請從拓撲中移除此伺服器。可再次使用新前端伺服器時，請將它新增至拓撲。


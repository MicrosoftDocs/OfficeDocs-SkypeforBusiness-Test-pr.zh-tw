---
title: Lync Server 2013：IP 位址類型概觀
TOCTitle: Lync Server 2013 的 IP 位址類型概觀
ms:assetid: ee9a695f-5cf5-441e-94fb-6adeca50e8d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205363(v=OCS.15)
ms:contentKeyID: 49292728
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 IP 位址類型概觀

 

_**上次修改主題的時間：** 2015-03-09_

在 Lync Server 2013 中設定 IP 位址時，您有三種作法。您可設定 Lync Server 2013 只支援 IP 版本 4 (IPv4)、只支援 IP 版本 6 (IPv6)，或是兩種組合 (稱為 *「雙重堆疊」* (dual stack))。每種組態都有幾個問題需要考量：

  - **僅限 IPv4**   IPv6 會產生，是因為全球已快用盡 IPv4 位址。IPv6 最終將會完全獲得全球支援，但目前必須與貴企業通訊的多數公司與裝置尚未支援 IPv6，短時間內也不會有所進展。僅限 IPv4 組態將有助於確保 Lync Server 實作可與多數現有裝置通訊。

  - **僅限 IPv6**   反之，完整的 IPv6 實作在這個階段將排除與許多現有裝置的通訊。

  - **雙重堆疊**   雙重堆疊是同時啟用 IPv4 與 IPv6 位置的網路。 Lync Server 2013 支援此組態，因為在多數情況下，從完整 IPv4 到完整 IPv6 的轉換需要好幾年的時間。

下節說明這三種組態的相容性，以便使用各種 Lync Server 功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有實驗室或驗證用途的僅限 IPv6 的用戶端或伺服器組態，才能獲得支援。生產部署不支援僅限 IPv6 組態。</td>
</tr>
</tbody>
</table>


## 用戶端登錄


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端端點網路</th>
<th>伺服器網路</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>雙重堆疊</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>IPv6</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## 對等用戶端

對等通訊包含音訊、音訊/視訊、應用程式共用，以及檔案傳輸。這兩個用戶端登錄成功後，即可支援下列組合。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端端點 1</th>
<th>用戶端端點 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## 會議

會議包含音訊/視訊、應用程式共用，以及資料共同作業 (白板與檔案共用)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端端點網路</th>
<th>伺服器網路</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>雙重堆疊</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>IPv6</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## 中繼伺服器/PSTN

若流量通過 IPv6 介面，則 Lync Server 2013 不支援公用交換電話網路 (PSTN) 通話的媒體旁路。若需要媒體旁路，建議將 PSTN 閘道設為 IPv4。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>主要介面*</th>
<th>PSTN 介面 (中繼伺服器)</th>
<th>PSTN 閘道設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>雙重堆疊</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>雙重堆疊</p></td>
<td><p>雙重堆疊</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>雙重堆疊</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


\* 主要介面是與 Lync Server 元件通訊的介面。

## 遠端使用者對等通訊

與遠端使用者的對等通訊包含立即訊息、音訊/視訊、應用程式共用，以及檔案傳輸。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>遠端使用者網路</th>
<th>Edge Server (外部 Edge)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>雙重堆疊</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="odd">
<td><p>雙重堆疊</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>雙重堆疊</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## 前端集區與 Edge 集區組態

下表顯示 前端伺服器 集區與內部 Edge Server 集區的支援矩陣。

### 前端集區與 Edge 集區 (內部 Edge) 矩陣

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Edge 集區：IPv4</strong></p></td>
<td><p><strong>Edge 集區：雙重堆疊</strong></p></td>
<td><p><strong>Edge 集區：IPv6</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>前端集區：IPv4</strong></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><strong>前端集區：雙重堆疊</strong></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><strong>前端集區：IPv6</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是*</p></td>
</tr>
</tbody>
</table>


\* 此組合僅適用於實驗室環境。

下表是內部與外部邊緣介面的支援組合矩陣。

### Edge 集區 (內部 Edge) 與 Edge 集區 (外部 Edge) 矩陣

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Edge 集區 (外部 Edge)：IPv4</strong></p></td>
<td><p><strong>Edge 集區 (外部 Edge)：雙重堆疊</strong></p></td>
<td><p><strong>Edge 集區 (外部 Edge)：IPv6</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Edge 集區 (內部 Edge)：IPv4</strong></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><strong>Edge 集區 (內部 Edge)：雙重堆疊</strong></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><strong>Edge 集區 (內部 Edge)：IPv6</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是*</p></td>
</tr>
</tbody>
</table>


\* 此組合僅適用於實驗室環境。

## IPv6 進階 Enterprise Voice 支援

包含所有通話許可控制 (CAC)、增強型 911 (E9-1-1) 或媒體旁路的部署必須設為僅限 IPv4 或雙重堆疊實作。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在雙重堆疊部署中，即使 Lync 用戶端使用 IPv6 連線到 Lync Server， Lync 將盡可能對應到適當的 IPv4 位置，以支援 E9-1-1。</td>
</tr>
</tbody>
</table>


有 IPv6 位址的 位置資訊服務 不受支援。

Exchange 整合通訊 (UM) 不支援 IPv6。若使用 Exchange UM，請確認 DNS 解析不是傳回到 IPv6 位址。若來電會傳送到語音信箱，使用 IPv6 可能導致失敗。

## 其他 Lync Server 2013支援的 IPv6 功能

除了上述提及的功能與元件， Lync Server 2013 還支援下列 IPv6 功能：

  - **永續性交談**
    
    您可使用 拓撲產生器 設定 常設聊天室 的 IPv6。如需設定 常設聊天室 的詳細資訊，請參閱部署永續性交談的伺服器文件。

  - **經驗品質 (QoE) 與詳細通話記錄 (CDR) 報告**
    
    監控報告包含監控伺服器資料庫儲存的 IP 位址，不論是 IPv4 或 IPv6。


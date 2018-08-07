---
title: Lync Server 2013：選擇拓撲
TOCTitle: 選擇拓撲
ms:assetid: 23f2aeb6-fed9-4349-8fba-dcbf18ee4b04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425716(v=OCS.15)
ms:contentKeyID: 49290346
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中選擇拓撲

 

_**上次修改主題的時間：** 2015-03-09_

選擇拓撲後，可以使用下列其中一個支援的拓撲選項：

> [!NOTE]  
> 若您已經使用過 Microsoft Lync Server 2010，您會發現此處的指導方針除了少數特別註明之處，大部分都沒有變更。



  - [Lync Server 2013 中的單一合併 Edge (利用私人 IP 位址及 NAT)](lync-server-2013-single-consolidated-edge-with-private-ip-addresses-and-nat.md)

  - [Lync Server 2013 中的單一合併 Edge (利用公用 IP 位址)](lync-server-2013-single-consolidated-edge-with-public-ip-addresses.md)

  - [Lync Server 2013 中的調整式合併 Edge (使用 NAT 透過私人 IP 位址進行 DNS 負載平衡)](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md)

  - [Lync Server 2013 中的調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)

  - [Lync Server 2013 中含硬體負載平衡器的調整式合併 Edge](lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md)

> [!IMPORTANT]  
> 內部 Edge 介面和外部 Edge 介面必須使用相同類型的負載平衡。您不能在一個 Edge 介面上使用 DNS 負載平衡，而在另一個 Edge 介面上使用硬體負載平衡。



下表摘要列出受支援 Microsoft Lync Server 2013 拓撲可用的功能。欄標題表示某特定 Edge 設定選項可用的功能。以調整式 Edge (DNS 負載平衡) 選項為例，您可以看到它支援高可用性，可使用指派給 Edge 外部介面之無法經路由傳送的私人 IP 位址 (搭配 NAT) 或可路由公用 IP 位址，由於不需要硬體負載平衡器因此可以降低成本。

DNS 負載平衡支援的 Edge 容錯移轉案例為 Lync 至 Lync 點對點工作階段、 Lync 會議工作階段、 Lync 至 PSTN 工作階段以及 Office 365。不適用於 DNS 負載平衡支援的 Edge 容錯移轉案例為針對遠端使用者 Exchange 整合通訊 (UM) ( Exchange 2010 SP1 之前)、公用立即訊息 (IM) 連線和執行 Office Communications Server之伺服器同盟的容錯移轉。

### Edge Server 拓撲選項摘要

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>拓撲</th>
<th>高可用性</th>
<th>Edge 集區中的外部 Edge Server 都需要額外的 DNS A 記錄</th>
<th>Lync 至 Lync 工作階段的 Edge 容錯移轉</th>
<th>Lync 至 Lync EUM/PIC/OCS 同盟工作階段的 Edge 容錯移轉</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 NAT 的單一 Edge</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>使用公用 IP 的單一 Edge</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>使用 NAT 的調整式 Edge (DNS 負載平衡)</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>*</p></td>
</tr>
<tr class="even">
<td><p>使用公用 IP 的調整式 Edge (DNS 負載平衡)</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>*</p></td>
</tr>
<tr class="odd">
<td><p>調整式 Edge 硬體 (負載平衡)</p></td>
<td><p>是</p></td>
<td><p>否 (每個 VIP 各一個 DNS A 記錄)</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


**\*** 公用立即訊息 (IM) 連線和執行 Office Communications Server 伺服器同盟的容錯移轉不適用於 DNS 負載平衡。使用 DNS 負載平衡的 Exchange UM (遠端使用者) 容錯移轉必須具備 Exchange Server 2010 SP1 或更新版本。

> [!NOTE]  
> 單一 Edge 和調整式的 Edge (DNS 負載平衡) 拓撲可以使用：  
> <ul><li>可路由公用 IP 位址</li>
> <li>無法經路由傳送的私人 IP 位址 (如果使用對稱式網路位址轉譯 (NAT))</li>  
    > [!NOTE]  
    > 若您使用公用 IP 位址或私人 IP 位址且搭配 NAT，則仍會根據您在 拓撲產生器中所做的設定選擇，使用相同的 IP 位址數目。您可設定 Edge Server 讓每項服務使用單一 IP 位址搭配明確的連接埠，或者讓每項服務使用明確的 IP 位址，但使用相同的連接埠 (預設為 TCP 443)。
> </li></ul>
> 若您決定使用無法經路由傳送的私人 IP 位址且搭配 NAT：
> <ul><li><p>您必須在三個外部介面上都使用可路由的私人 IP 位址</p></li>
> <li><p>您必須為輸入和輸出流量設定對稱的 NAT</p></li></ul>
> 調整式 Edge (硬體負載平衡) 拓撲必須使用公用 IP 位址


Lync Server 2013 支援將 Access、Web 會議和 A/V Edge 外部介面放在路由器或防火牆後面，該路由器或防火牆會為單一及調整式合併 Edge Server 拓撲執行網路位址解析 (NAT)。

若要將 NAT 用於所有 Edge 外部介面，需要使用 DNS 負載平衡。和使用硬體負載平衡相比，透過使用 DNS 負載平衡而不使用 NAT，可讓您減少 Edge 集區中每個 Edge Server 的公用 IP 位址數目，如下列清單中所述：

  - Lync Server 2013 調整式合併 Edge (DNS 負載平衡) 要求 Edge 集區中的每個 Edge Server 需要三個公用 IP 位址。

  - Lync Server 2013 調整式合併 Edge (硬體負載平衡) 需要有三個公用 IP 位址用於負載平衡器虛擬 IP 位址 (僅一次的需求，不會在更多 Edge Server 新增至集區時遞增)，以及集區中每一 Edge Server 各需要三個公用 IP 位址。

### 調整式合併 Edge 的 IP 位址需求 (每個角色一個 IP 位址)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>每個集區的 Edge Server 數目</th>
<th>需要的 IP 位址 Lync Server 2013 數目 (DNS 負載平衡)</th>
<th>需要的 IP 位址 Lync Server 2013 數目 (硬體負載平衡)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>6</p></td>
<td><p>3 (每個 VIP 各 1 個) + 6</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>9</p></td>
<td><p>3 (每個 VIP 各 1 個) + 9</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>3 (每個 VIP 各 1 個) + 12</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>15</p></td>
<td><p>3 (每個 VIP 各 1 個) + 15</p></td>
</tr>
</tbody>
</table>


### 調整式合併 Edge 的 IP 位址需求 (所有角色都使用單一 IP 位址)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>每個集區的 Edge Server 數目</th>
<th>需要的 IP 位址 Lync Server 2013 數目 (DNS 負載平衡)</th>
<th>需要的 IP 位址 Lync Server 2013 數目 (硬體負載平衡)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>1 (每個 VIP 各 1 個) + 2</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>3</p></td>
<td><p>1 (每個 VIP 各 1 個) + 3</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>1 (每個 VIP 各 1 個) + 4</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>5</p></td>
<td><p>1 (每個 VIP 各 1 個) + 5</p></td>
</tr>
</tbody>
</table>


拓撲選項的主要決策點是高可用性和負載平衡。高可用性的需求條件會影響負載平衡的決策。

  - **高可用性**   如果您需要高可用性，請在單一集區中至少部署兩部 Edge Server。單一 Edge 集區可支援最多 12 部 Edge Server。如果您需要更多容量，則可部署多個 Edge 集區。一般而言，10% 的使用者人數需要外部存取。
    
    > [!IMPORTANT]  
    > 拓撲產生器可讓您在單一 Edge 集區中設定最多 12 部 Edge Server。單一集區中 Edge Server 的最大數量為 12 ，這數字是經過測試且受支援的。因此， 拓撲產生器允許大於 12 的數字不應構成暗示在單一 Edge 集區中可支援超過 12 部 Edge Server。
    


  - **硬體負載平衡**   在 Edge 外部介面使用可公開路由的 IP 位址時，即可支援在對 Lync Server 2013Edge Server 進行負載平衡時使用硬體負載平衡。例如，此方法會用於下列任一應用程式需要容錯移轉的情況時：
    
      - 公用 IM 連線
    
      - 與執行 Microsoft Office Communications Server 2007 或 Microsoft Office Communications Server 2007 R2 的公司建立同盟
    
      - 外部存取至 Exchange 2007 Unified Messaging (UM) 或 Exchange 2010 UM
        
        > [!IMPORTANT]  
        > Exchange UM 可支援 Exchange 2010 SP1 和更新版本的 DNS 負載平衡。
        
    
    這三種應用程式都能繼續運作，但不會感知 DNS 負載平衡，只會連接至集區中第一個 Edge Server。如果該伺服器無法使用，連線就會失敗。例如，如果在集區中部署多個 Edge Server 用來處理同盟流量負載，實際上只有一個 Access Proxy 會收到流量，而其他伺服器都閒置中。

> [!IMPORTANT]  
> 如果您要與使用 Lync Server 2010 和 Microsoft Office 365 的公司建立同盟，建議使用 DNS 負載平衡。需注意，如果同盟協力廠商大多使用 Office Communications Server 2007 或 Office Communications Server 2007 R2，則會嚴重影響效能。



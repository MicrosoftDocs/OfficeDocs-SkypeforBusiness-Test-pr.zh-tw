---
title: Lync Server 2013：決定外部 A/V 防火牆和連接埠需求
TOCTitle: 決定外部 A/V 防火牆和連接埠需求
ms:assetid: 3b849dc7-175d-40d1-820d-80e6ade6d332
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425882(v=OCS.15)
ms:contentKeyID: 49290647
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求

 

_**上次修改主題的時間：** 2015-03-09_

音訊/視訊 (A/V) 通訊有可能非常複雜。因為 A/V 中所使用之通訊協定的本質以及用戶端和伺服器使用通訊協定的方式，所以特別以本節說明用戶端和伺服器版本的差異。

請使用下列 A/V 防火牆和連接埠表格，判斷防火牆需求以及應開放的連接埠。接著檢閱網路位址轉譯 (NAT) 術語，因為 NAT 可透過許多方式實作。如需防火牆連接埠設定的詳細範例，請參閱＜ [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞中的參考架構。

### 音訊/視訊和媒體流量中 UDP 和 TCP 的一般通訊協定使用方式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>音訊/視訊 (A/V) 傳輸</th>
<th>使用狀況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UDP</p></td>
<td><p>音訊和視訊的慣用傳輸層通訊協定</p></td>
</tr>
<tr class="even">
<td><p>TCP</p></td>
<td><p>音訊和視訊的容錯移轉傳輸層通訊協定</p>
<p>應用程式共用至 Office Communications Server 2007 R2、 Lync Server 2010 及 Lync Server 2013 的必要傳輸層通訊協定</p>
<p>檔案傳輸至 Lync Server 2010 及 Lync Server 2013 的必要傳輸層通訊協定</p></td>
</tr>
</tbody>
</table>


## 外部使用者存取的外部 A/V 防火牆連接埠需求

不論用戶端的版本或同盟協力廠商的版本為何，外部 (及內部) SIP 和會議介面的防火牆連接埠需求是一致的。

A/V Edge 外部介面則不同。對於使用 Office Communications Server 2007 的同盟而言，A/V Edge Service 需要外部防火牆規則允許 RTP/TCP 和 RTP/UDP 流量在 50,000 至 59,999 連接埠範圍雙向流動。前表中假設 Lync Server 2013 是主要同盟協力廠商，且您要設定它來與其他所列同盟協力廠商類型之一進行通訊。

在設定音訊/視訊連接埠範圍 50,000-59,999 時，必須考慮到該連接埠範圍會包含與同盟協力廠商通訊所用的來源連接埠。設想從同盟協力廠商起始通訊時的詳細情況。從 50,000-59,999 範圍中 A/V Edge 服務 連接埠的通訊會連線至協力廠商之 A/V Edge 服務 的預期連接埠 TCP 443。相反地，至 A/V Edge 服務 連接埠 TCP 443 的輸入流量會有 50,000-59,999 範圍中的來源連接埠。

其他的防火牆與防火牆管理原則可能只要求設定目的地規則，也可能要求設定來源和目的地。如果您的需求是只針對目的地連接埠，則音訊/視訊需求如下︰


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源 IP</th>
<th>目的地 IP</th>
<th>目的地連接埠</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A/V Edge 服務 介面</p></td>
<td><p>任何一個</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>A/V Edge 服務 介面</p></td>
<td><p>任何一個</p></td>
<td><p>UDP 3478</p></td>
</tr>
<tr class="odd">
<td><p>任何一個</p></td>
<td><p>A/V Edge 服務 介面</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>任何一個</p></td>
<td><p>A/V Edge 服務 介面</p></td>
<td><p>UDP 3478</p></td>
</tr>
</tbody>
</table>


如果您的原則是要求輸入和輸出防火牆規則定義，則音訊/視訊需求如下︰


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>來源 IP</th>
<th>目的地 IP</th>
<th>來源連接埠</th>
<th>目的地連接埠</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A/V Edge 服務 介面</p></td>
<td><p>任何一個</p></td>
<td><p>TCP 50,000-59,999</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>A/V Edge 服務 介面</p></td>
<td><p>任何一個</p></td>
<td><p>UDP 3478</p></td>
<td><p>UDP 3478</p></td>
</tr>
<tr class="odd">
<td><p>任何一個</p></td>
<td><p>A/V Edge 服務 介面</p></td>
<td><p>任何一個</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>任何一個</p></td>
<td><p>A/V Edge 服務 介面</p></td>
<td><p>任何一個</p></td>
<td><p>UDP 3478</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft Office Communications Server 2007 需要稍微不同的設定。TCP 和 UDP 連接埠範圍 50,000-59,999 必須開放輸入和輸出。此需求僅針對 Office Communicator 2007。 Office Communications Server 2007 R2、 Lync Server 2010 及 Lync Server 2013 只要求 TCP 範圍 50,000-59,999 開放輸出。</td>
</tr>
</tbody>
</table>


## 外部使用者存取的 NAT 需求

NAT 通常是一種路由功能，但如防火牆甚至是硬體負載平衡器之類的較新裝置都可以設定 NAT。因此本主題並不注重在執行 NAT 的裝置，而是說明必要的 NAT 行為。

Lync Server 2013通訊軟體不支援對進出 Edge 內部介面的流量使用 NAT，但對於 Edge 外部介面，下列 NAT 行為是必要的。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須針對連入和連出流量設定對稱的 NAT。對稱的 NAT 為此主題中說明的 NAT 技術。</td>
</tr>
</tbody>
</table>


本文件在表格和繪圖中使用縮寫 ChangeDST 和 ChangeSRC，以定義下列必要行為：

  - **ChangeDST**   指在預定送往使用 NAT 的網路的封包上變更目的 IP 位址的過程。也稱為透明度、連接埠轉送、目的地 NAT 模式或半 NAT 模式。

  - **ChangeSRC**   指在離開使用 NAT 的網路的封包上變更來源 IP 位址的過程。也稱為 Proxy、安全 NAT、可設定狀態的 NAT、來源 NAT 或全 NAT 模式。

無論所使用的命名慣例為何，Edge Server 的外部介面所需的 NAT 行為如下：

  - 從網際網路到 Edge 外部介面的流量：
    
      - 將傳入封包的目的地 IP 位址，從 Edge 外部介面公用 IP 位址變更為轉譯後的 Edge 外部介面 IP 位址。
    
      - 保持來源 IP 位址不變，讓流量保有傳回路由。

  - 從 Edge 外部介面到網際網路的流量：
    
      - 將離開 Edge 外部介面的封包的來源 IP 位址，從轉譯後的 Edge 外部介面 IP 位址變更為公用 IP 位址，以免暴露內部 Edge IP 位址，而且因為這是無法路由的 IP 位址。
    
      - 保持傳出封包上的目的地 IP 位址不變。

下圖以 A/V Edge 為例，顯示變更輸入流量的目的地 IP 位址 (ChangeDST) 跟變更輸出流量的來源 IP 位址 (ChangeSRC) 有何不同。

**變更輸入流量的目的地 IP 位址 (ChangeDST) 和變更來源 IP 位址 (ChangeSRC)**

![變更目的地/來源 IP 位址](images/Gg425882.0fee7ec5-4cb8-4aff-9164-e7fbab73336d(OCS.15).jpg "變更目的地/來源 IP 位址")

重點為：

  - 對於輸入至執行 A/V Edge 服務 之伺服器的流量，來源 IP 位址不變，但目的地 IP 位址從 131.107.155.30 變更為轉譯後的 IP 位址 10.45.16.10。

  - 對於從執行 A/V Edge 服務 之伺服器輸出回到工作站的流量，來源 IP 位址從伺服器的公用 IP 位址變更為執行 A/V Edge 服務 之伺服器的公用 IP 位址。目的地 IP 仍為工作站的公用 IP 位址。封包從第一個 NAT 裝置輸出後，NAT 裝置上的規則會將來源 IP 位址從執行 A/V Edge 服務 之伺服器的外部介面 IP 位址 (10.45.16.10) 變更為其公用 IP 位址 (131.107.155.30)。


---
title: Lync Server 2013：E9-1-1 概觀
TOCTitle: E9-1-1 概觀
ms:assetid: c01e6774-bc9f-4c5b-a60b-478b7317b2b7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412936(v=OCS.15)
ms:contentKeyID: 49292200
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 E9-1-1 概觀

 

_**上次修改主題的時間：** 2012-10-29_

Microsoft Lync Server 2013 可支援從 Lync 用戶端和 Lync Phone Edition 裝置進行增強型 9-1-1 (E9-1-1) 通話。當您為 E9-1-1 設定 Lync Server 時，從 Lync 2013 或 Lync Phone Edition 進行的緊急通話會包含 位置資訊服務資料庫中的緊急回應位置 (ERL)。ERL 包含市民地址 (也就是街道地址)，以及其他可更精確指出辦公大樓內與其他多租用戶設施內之位置的資訊。使用者撥打緊急電話時， Lync Server 會透過 中繼伺服器，將通話音訊連同位置和回撥資訊路由傳送至 E9-1-1 服務提供者。E9-1-1 服務提供者再使用來電者的市民地址，將通話路由傳送至來電者當地的公共安全勤務中心 (PSAP)，並附上緊急服務查詢碼 (ESQK) 供 PSAP 查詢來電者的 ERL。

Lync Server 可支援使用兩種方法將緊急通話路由傳送給 E9-1-1 服務提供者：

  - 對合格 E9-1-1 服務提供者的工作階段初始通訊協定 (SIP) 主幹連線

  - 通往公用交換電話 (PSTN) 型 E9-1-1 服務提供者的緊急定位識別碼 (ELIN) 閘道

使用 SIP 主幹 E9-1-1 服務提供者時，需新增 ERL 至 位置資訊服務資料庫，然後根據 E9-1-1 服務提供者所維護的主要街道地址指南 (MSAG) 來驗證該位置。如果 E9-1-1 服務提供者收到的來電沒有位置資訊或是位置未經 MSAG 驗證，則 E9-1-1 服務提供者會將來電路由傳送至全國/地區緊急電話回應中心 (ECRC)，由受過專門訓練的人員盡量口頭詢問來電者的所在位置，再將來電手動路由傳送至適當的 PSAP (有些 SIP 主幹 E9-1-1 服務提供者也會提供 ECRC 的 PSTN 直接向內撥號 (DID) 號碼給客戶，以防萬一 SIP 主幹因故不通，還是可以路由傳送 9-1-1 通話)。

與有固定位置的分時多工 (TDM) 及 IP 型專用交換機 (PBX) 電話不同， Lync 端點可以保持機動性。當您部署 E9-1-1 功能時， Lync Server 可協助確保無論來電者所在位置為何，緊急電話都能路由傳送至來電者當地的 PSAP。例如，如果使用者的主要辦公室位於 Redmond, Washington，但使用者是從 Wichita, Kansas 分公司的電話撥出緊急電話，則 SIP 主幹或 PSTN 型 E9-1-1 服務提供者會將來電路由傳送至 Wichita 的 PSAP，而非 Redmond 的 PSAP。

使用 ELIN 閘道時，也需將 ERL 新增至 位置資訊服務資料庫，但還需包含每個位置的 ELIN 號碼。ELIN 號碼會成為緊急通話期間的緊急撥打號碼。接著您必須要確定 PSTN 業者會將 ELIN 上傳至自動位置識別 (ALI) 資料庫。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>與 Lync 連線的類比裝置無法接收來自 位置資訊服務的位置資訊或是將位置傳輸給 E9-1-1 服務提供者。如果您使用 SIP 主幹 E9-1-1 服務提供者選項，並需要支援讓類比電話撥打 E9-1-1，您有兩個選項：
<ul>
<li><p><strong>傳統 PS-ALI 選項</strong>   如果每個部署了類比電話的網站中都有本機 PSTN 閘道，且每部類比電話都有 DID，則可直接向專用交換機/自動位置識別 (PS-ALI) 服務提供者佈建類比裝置的位置。在這種情況下，請設定特製的 Lync 語音原則，並將其指派給類比裝置連絡人物件，使得這些電話的 E9-1-1 來電會直接路經本機閘道傳送到服務該網站的 PSTN 提供者 (而不是將來電路由傳送到 E9-1-1 服務提供者 SIP 主幹)。撥打緊急電話時，PS-ALI 提供者那邊與 PSTN 主幹相關聯的資料庫會將每部類比電話的 DID 對應至實體位置，並將該位置提供給 PSAP。每次將電話移動至不同的 ERL 時，都必須向 PS-ALI 服務提供者更新這些記錄。</p></li>
<li><p><strong>E9-1-1 服務提供者選項</strong>   您可以向 E9-1-1 服務提供者註冊類比電話 DID 及其對應的 ERL (如果 E9-1-1 服務提供者支援此選項)。提供者如果從 Lync Server 收到不含 PIDF-LO 資料的來電，可能會查看資料庫中是否有符合來電方 DID 號碼的項目。提供者可以使用從資料庫擷取的 ERL，自動將緊急電話路由傳送給正確的 PSAP，而 PSAP 會收到類比裝置的 DID 以及 ESQK 記錄，供調度員查閱來電者位置。</p></li>
</ul>
如果您使用 ELIN 閘道選項且需要支援讓類比電話撥打 E9-1-1，可以直接向 PS-ALI 服務提供者佈建類比裝置的位置，如前文第一個選項所述。</td>
</tr>
</tbody>
</table>


從 Lync Server 的觀點來看，E9-1-1 處理程序可分為兩個階段：

  - 階段 1：取得位置

  - 階段 2：將緊急電話路由傳送至 E9-1-1 服務提供者

本節說明這些階段的運作方式。

如果您打算將基礎結構設定為自動偵測用戶端位置，首先需要決定要使用哪些網路元素對應出來電者的位置。如需可行選項的詳細資訊，請參閱 [在 Lync Server 2013 中定義用於判斷位置的網路元素](lync-server-2013-defining-the-network-elements-used-to-determine-location.md)。

## 本節內容

  - [在 Lync Server 2013 中擷取位置](lync-server-2013-acquiring-a-location.md)

  - [在 Lync Server 2013 中使用 SIP 主幹路由 E9-1-1 來電](lync-server-2013-routing-e9-1-1-calls-by-using-a-sip-trunk.md)

  - [在 Lync Server 2013 中使用 ELIN 閘道路由 E9-1-1 來電](lync-server-2013-routing-e9-1-1-calls-by-using-an-elin-gateway.md)


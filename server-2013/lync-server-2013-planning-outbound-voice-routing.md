---
title: Lync Server 2013：規劃撥出語音路由
TOCTitle: 規劃撥出語音路由
ms:assetid: 37c55fa4-175a-4190-b9e4-c2e5ac7b9261
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425853(v=OCS.15)
ms:contentKeyID: 49290597
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃撥出語音路由

 

_**上次修改主題的時間：** 2015-03-09_

撥出電話路由適用於以公用交換電話網路 (PSTN) 閘道、主幹或專用交換機 (PBX) 為目的地的電話。當使用者撥打電話時，伺服器就會在必要時將電話號碼正規化成 E.164 格式，並嘗試比對電話號碼與 SIP URI。如果伺服器無法成功進行比對，就會根據提供的撥號字串套用撥出電話的路由邏輯。您可以依下表所述進行伺服器設定，以便定義該邏輯。

### Lync Server 撥出電話路由設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>物件</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>撥號對應表</p></td>
<td><p>撥號對應表是一個具名的正規化規則集，可將具名位置、個別使用者或連絡人物件的電話號碼轉譯成單一標準 (E.164) 格式，以便進行電話授權和電話路由傳送。</p></td>
</tr>
<tr class="even">
<td><p>正規化規則</p></td>
<td><p>正規化規則會針對每個指定位置、使用者或連絡人物件，定義要如何路由傳送以各種格式表達的電話號碼。相同的撥號字串可能會因撥號地點的位置，以及撥打電話的人員或連絡人物件而有不同的解譯和轉譯。撥號對應表即是一組與特定位置相關的正規化規則。</p></td>
</tr>
<tr class="odd">
<td><p>語音原則</p></td>
<td><p>語音原則會讓一個或多個 PSTN 使用方式記錄與一個使用者或使用者群組產生關聯。語音原則也會提供您可啟用或停用之撥號功能的清單。</p></td>
</tr>
<tr class="even">
<td><p>PSTN 使用方式記錄</p></td>
<td><p>PSTN 使用方式記錄會指定組織內的各個使用者或使用者群組可以進行的通話等級 (例如內線、當地或長途電話)。</p></td>
</tr>
<tr class="odd">
<td><p>電話路由</p></td>
<td><p>電話路由會讓目的地電話號碼與特定主幹和 PSTN 使用方式記錄產生關聯。</p></td>
</tr>
</tbody>
</table>


## 本章節內容

本節提供設定下列撥出電話路由伺服器設定的指導方針：

  -   
    [Lync Server 2013 中的撥號對應表和正規化規則](lync-server-2013-dial-plans-and-normalization-rules.md)

  -   
    [Lync Server 2013 中的語音原則](lync-server-2013-voice-policies.md)

  -   
    [Lync Server 2013 中的 PSTN 使用方式記錄](lync-server-2013-pstn-usage-records.md)

  -   
    [Lync Server 2013 中的語音路由](lync-server-2013-voice-routes.md)

## 請參閱

#### 概念

[Lync Server 2013 中的 SIP 主幹連線](lync-server-2013-sip-trunking.md)  
[Lync Server 2013 中的 SIP 直接連線](lync-server-2013-direct-sip-connections.md)


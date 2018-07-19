---
title: Lync Server 2013：E9-1-1 的部署檢查清單
TOCTitle: E9-1-1 的部署檢查清單
ms:assetid: cc6a656a-6043-4b9b-85c2-5708b9bb1c06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398864(v=OCS.15)
ms:contentKeyID: 49292340
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 E9-1-1 的部署檢查清單

 

_**上次修改主題的時間：** 2015-03-09_

若要有效規劃增強型 9-1-1 (E9-1-1)，請務必包含下列部署需求：

  - 部署 E9-1-1 的先決條件。

  - 部署 E9-1-1 所需的步驟。

## E9-1-1 的部署先決條件

在部署 E9-1-1 之前，您必須已部署 Lync Server 內部伺服器，包括 中央管理存放區、 前端集區或 Standard Edition Server、一或多部 中繼伺服器或 中繼伺服器集區，以及 Lync Server 用戶端。此外，E9-1-1 部署需要有 SIP 主幹連到合格的緊急服務提供者，或有公用交換電話網路 (PSTN) 的緊急定位識別碼 (ELIN)。 Lync Server 僅支援使用美國境內的 E9-1-1 服務提供者。

## 部署程序

下表提供 E9-1-1 部署程序的概觀。如需部署步驟的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中設定增強型 9-1-1](lync-server-2013-configure-enhanced-9-1-1.md)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>角色</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>設定語音使用方式、路由和主幹組態</p></td>
<td><ol>
<li><p>建立新的 PSTN 使用方式記錄。這個名稱與位置原則中用於 [PSTN 使用方式] 設定的名稱相同。</p></li>
<li><p>建立或指派語音路由給在上一個步驟建立的 PSTN 使用方式記錄，然後使閘道屬性指向 E9-1-1 SIP 主幹或 ELIN 閘道。</p></li>
<li><p>若為 SIP 主幹 E9-1-1 服務提供者，請使用 <strong>set-cstrunkconfiguration –EnablePIDFLOSupport</strong> Cmdlet 設定主幹來處理透過 SIP 傳遞 PIDF-LO 資料的 E9-1-1 通話。</p></li>
<li><p>(選用) 若為 SIP 主幹 E9-1-1 服務提供者，請為 E9-1-1 服務提供者 SIP 主幹所未處理的通話，建立或指派本機 PSTN 路由。如果與 E9-1-1 服務提供者的連線無法使用，則會使用此路由。如果 E9-1-1 服務提供者支援的話，請指派主幹組態規則給會將 911 撥號字串轉譯成全國/地區緊急電話回應中心 (ECRC) 直接向內撥號 (DID) 號碼的閘道。</p></li>
</ol></td>
<td><p>CSVoiceAdmin</p></td>
<td><p><a href="lync-server-2013-configure-an-e9-1-1-voice-route.md">在 Lync Server 2013 中設定 E9-1-1 語音路由</a></p></td>
</tr>
<tr class="even">
<td><p>建立位置原則並且指派給使用者和子網路</p></td>
<td><ol>
<li><p>檢閱全域位置原則。</p></li>
<li><p>建立使用者層級範圍的位置原則；如果組織具有一個以上擁有不同緊急使用方式的網站，則建立網路層級範圍的位置原則。</p></li>
<li><p>將位置原則指派給網站。</p></li>
<li><p>將適當的子網路加入至網站。</p></li>
<li><p>(選用) 將位置原則指派給使用者原則。</p></li>
</ol>
<p></p></td>
<td><p>CSVoiceAdmin</p>
<p>CSLocationAdmin (建立位置原則除外)</p></td>
<td><p><a href="lync-server-2013-create-location-policies.md">在 Lync Server 2013 中建立位置原則</a></p>
<p><a href="lync-server-2013-add-a-location-policy-to-a-network-site.md">在 Lync Server 2013 中將位置原則新增到網站</a></p>
<p><a href="lync-server-2013-associate-subnets-with-network-sites-for-e9-1-1.md">在 Lync Server 2013 中將子網路與 E9-1-1 上的網站關聯</a></p></td>
</tr>
<tr class="odd">
<td><p>設定位置資料庫</p></td>
<td><ol>
<li><p>將網路元素與位置的對應填入資料庫。</p></li>
<li><p>若為 ELIN 閘道，請新增 ELIN 至 &lt;CompanyName&gt; 欄。</p></li>
<li><p>設定與 E9-1-1- 服務提供者的連線以便驗證位址。</p></li>
<li><p>向 E9-1-1 服務提供者驗證位址。</p></li>
<li><p>發行更新過的資料庫。</p></li>
<li><p>若為 ELIN 閘道，請上傳 ELIN 到您 PSTN 業者的自動位置識別 (ALI) 資料庫。</p></li>
</ol></td>
<td><p>CSVoiceAdmin</p>
<p>CSLocationAdmin</p></td>
<td><p><a href="lync-server-2013-configure-the-location-database.md">在 Lync Server 2013 中設定位置資料庫</a></p></td>
</tr>
<tr class="even">
<td><p>設定進階功能 (選用)</p></td>
<td><ol>
<li><p>設定 SNMP 應用程式的 URL。</p></li>
<li><p>設定次要 位置資訊服務的位置 URL。</p></li>
</ol></td>
<td><p>CSVoiceAdmin</p></td>
<td><p><a href="lync-server-2013-configure-an-snmp-application.md">在 Lync Server 2013 中設定 SNMP 應用程式</a></p>
<p><a href="lync-server-2013-configure-a-secondary-location-information-service.md">在 Lync Server 2013 中設定次要位置資訊服務</a></p></td>
</tr>
</tbody>
</table>


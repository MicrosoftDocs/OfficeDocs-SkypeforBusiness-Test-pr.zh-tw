---
title: 會議位置基礎路由需求
TOCTitle: 會議位置基礎路由需求
ms:assetid: 766d9286-2c34-4faf-bb3e-f0ca478a70cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362806(v=OCS.15)
ms:contentKeyID: 56269109
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 會議位置基礎路由需求

 

_**上次修改主題的時間：** 2015-03-09_

以下為安裝與設定位置基礎路由會議應用程式的必要需求：

  - 拓撲中的所有伺服器或集區均需部署 Lync Server 2013 累計更新 2。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是拓撲中的 Lync Server 或集區並未安裝 Lync Server 2013 累計更新 2 或更高版本，則無法保證能成功執行 Lync 會議的位置基礎路由。</td>
</tr>
</tbody>
</table>


  - Lync Server 2013 位置基礎路由是位置基礎路由會議應用程式的必要條件。如需設定 Lync Server 2013 位置基礎路由的進一步資訊，請參閱＜[設定位置基礎路由](lync-server-2013-configuring-location-based-routing.md)＞。

  - 位置基礎路由會議應用程式的需求與 Lync Server 2013 位置基礎路由相同。如需詳細資訊，請參閱＜[規劃位置基礎路由](lync-server-2013-planning-for-location-based-routing.md)＞。

## 支援的伺服器

位置基礎路由會議應用程式要求拓撲中的所有前端集區與 Standard Edition Server 均需部署 Lync Server 2013 累計更新 2。若是拓撲中的部分 Lync Server 未安裝 Lync Server 2013 累計更新 2，則 Lync 會議與諮詢通話轉接將無法完整執行位置基礎路由限制。

下表說明支援位置基礎路由的伺服器角色與版本的組合。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>前端集區版本</p></td>
<td><p>中繼伺服器版本</p></td>
<td><p>受支援</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 累計更新 2</p></td>
<td><p>Lync Server 2013 累計更新 2</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013 累計更新 2</p></td>
<td><p>Lync Server 2013 累計更新 1</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 累計更新 2</p></td>
<td><p>Lync Server 2010</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013 累計更新 2</p></td>
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 累計更新 1</p></td>
<td><p>任何一個</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2010</p></td>
<td><p>任何一個</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>任何一個</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 支援的用戶端

支援 Lync 會議之位置基礎路由的 Lync 用戶端同時也是支援 Lync Server 2013 位置基礎路由的用戶端。如需詳細資訊，請參閱＜[位置基礎路由的用戶端和伺服器支援](lync-server-2013-client-and-server-support-for-location-based-routing.md)＞。

## 諮詢通話轉接的中繼伺服器需求

位置基礎路由會議應用程式要求部署獨立式中繼伺服器以在諮詢通話轉接中執行位置基礎路由限制。

若要執行諮詢通話轉接的位置基礎路由，中繼伺服器必須僅與要求位置基礎路由之網路區域中的單一中繼伺服器對等端 (即 PBX 或 SIP 閘道等) 相關聯。若是在相同的網路區域中部署額外的中繼伺服器對等端，則該中繼伺服器對等端必須與其他中繼伺服器相關聯。此需求詳述如下：

  - 單一中繼伺服器相對於多個中繼伺服器對等端 當諮詢通話轉接透過設有多個 SIP 主幹連結至多個對等端 (即 PBX 與閘道) 的中繼伺服器路由至中繼伺服器對等端時，若是允許透過部分 SIP 主幹進行諮詢通話轉接但不允許透過其他 SIP 主幹進行諮詢通話轉接，則諮詢通話轉接將遭到封鎖以防止 PSTN 電話旁路作業。
    
    例如，在單一中繼伺服器處理單一 PSTN 閘道中繼伺服器對等端與單一 PBX 中繼伺服器對等端的情況下，將採取下列行為：
    
      - 當來自指定網站 (即網站 1) 的 Lync 使用者嘗試透過諮詢轉接以 PSTN 端點將通話轉接至不同網站 (即網站 2) 的 Lync 使用者時，該通話將不受允許以防止 PSTN 電話旁路作業。
    
      - 當來自指定網站 (即網站 1) 的 Lync 使用者嘗試透過諮詢轉接以相同網站 (網站 1) 的 PBX 端點將通話轉接至不同網站 (即網站 2) 的 Lync 使用者時，即使不會發生 PSTN 電話旁路作業，該通話亦不受允許。

  - 個別中繼伺服器相對於個別中繼伺服器對等端
    
    當諮詢轉接以中繼伺服器對等端為目標時，系統將針對中繼伺服器所處理的單一中繼伺服器對等端評估諮詢轉接。系統將根據通話是否可能發生 PSTN 電話旁路作業而允許/不允許該通話，而網站中的所有其他中繼伺服器對等端因為是由不同的中繼伺服器處理，所以並不會造成任何影響。
    
    舉例來說，在個別中繼伺服器處理單一 PSTN 閘道中繼伺服器對等端與單一 PBX 中繼伺服器對等端的情況下，將採取下列行為：
    
      - 當來自指定網站 (即網站 1) 的 Lync 使用者嘗試透過諮詢轉接以 PSTN 端點將通話轉接至不同網站 (即網站 2) 的 Lync 使用者時，該通話將不受允許以防止 PSTN 電話旁路作業。
    
      - 當來自指定網站 (即網站 1) 的 Lync 使用者嘗試透過諮詢轉接以相同網站 (網站 1) 的 PBX 端點將通話轉接至不同網站 (即網站 2) 的 Lync 使用者時，該通話將因為不會發生 PSTN 電話旁路作業而受到允許。

## 位置基礎路由會議應用程式不支援的功能

位置基礎路由會議應用程式不支援下列功能：

  - 撥入式會議：撥入式會議無法執行位置基礎路由。任何撥入至特定會議的要求將不受位置基礎路由的限制，即使會議召集人為啟用位置基礎路由的 Lync 使用者亦是如此。

  - 建議不要在需要執行位置基礎路由限制的區域中佈建會議存取號碼。


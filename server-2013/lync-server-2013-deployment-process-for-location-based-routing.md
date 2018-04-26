---
title: Lync Server 2013：位置基礎路由的部署程序
TOCTitle: 位置基礎路由的部署程序
ms:assetid: 9e923e72-83fc-4a4f-8937-28a55739ed3e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994055(v=OCS.15)
ms:contentKeyID: 52056199
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的位置基礎路由的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

此主題提供與設定位置基礎路由有關的程序概觀。您必須已部署具有 企業語音 的 Lync ServerEnterprise Edition 或 Standard Edition，才能設定位置基礎路由。位置基礎路由需要的元件在您部署 企業語音 時就會加以安裝和啟用。

### 位置基礎路由部署程序

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
<th>所需群組和角色</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>部署 Enterprise Voice</p></td>
<td><ul>
<li><p>設定主幹</p></li>
<li><p>建立語音原則</p></li>
<li><p>定義語音路由</p></li>
</ul></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td><p>部署 Enterprise Voice</p></td>
</tr>
<tr class="even">
<td><p>驗證您的 Enterprise Voice 部署</p></td>
<td><p></p></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>設定網路區域、網站和子網路</p></td>
<td><ul>
<li><p>建立網路區域</p></li>
<li><p>建立網站</p></li>
<li><p>建立子網路與網站的關聯</p></li>
</ul></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td><p>關於網路區域、網站和子網路<br />
建立或修改網路區域<br />
建立或修改網站<br />
建立子網路與網站的關聯</p></td>
</tr>
<tr class="even">
<td><p>設定位置基礎路由</p></td>
<td><ul>
<li><p>建立語音路由原則</p></li>
<li><p>為每個主幹定義個別主幹組態</p></li>
<li><p>修改語音原則</p></li>
<li><p>啟用位置基礎路由組態</p></li>
</ul></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 範例部署

下列部署是用以進一步說明位置基礎路由所啟用的機制。

![以位置為基礎的路由拓撲](images/JJ994055.e1bd2230-44da-4784-b359-24572b6ce02d(OCS.15).png "以位置為基礎的路由拓撲")

## 傳入 PSTN 通話

系統管理員可以啟用定義的主幹以將通話路由傳送到「網站 1 閘道」以達到位置基礎路由的目的，並將「網站 1 閘道」與網站 1 建立關聯。啟用後，透過「網站 1 閘道」路由傳送的通話，將只會路由傳送給位於網站 1 的使用者。所有透過「網站 1 閘道」主幹路由傳送給位於其他網站 (例如網站 2) 使用者的通話將會受到封鎖，以禁止 PSTN 免話費機制。

所有透過「網站 1 閘道」傳入的 PSTN 通話將只能路由傳送到位於網站 1 的端點。例如，當「Lync 使用者 1」前往網站 2 時，所有透過「網站 1 閘道」傳入的 PSTN 通話將不會路由傳送到位於網站 2 的「Lync 使用者 1」端點。當「Lync 使用者 1」前往無法判斷使用者位置的未知網站時，也適用相同的路由規則。

下表說明此環境中「Lync 使用者 1」的使用者體驗。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>位於網站 1 的 Lync 使用者 1 端點</th>
<th>位於網站 2 的 Lync 使用者 1 端點</th>
<th>位於未知網站的 Lync 使用者 1 端點</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>傳送給 Lync 使用者 1 的輸入 PSTN 通話</p></td>
<td><p>通話會路由傳送到此位置的端點</p></td>
<td><p>通話不會路由傳送到此位置的端點</p></td>
<td><p>通話不會路由傳送到此位置的端點</p></td>
</tr>
</tbody>
</table>


## 傳出 PSTN 通話

語音路由可以同時在直接指派給使用者的語音原則，以及指派給網站的語音路由原則中參照。兩種原則都包含對路由的參照，可用來以不同方式路由傳送通話。例如，系統管理員可以為所有位於網站 1 的使用者定義語音路由原則，將所有輸出通話透過「網站 1 閘道」路由傳送，而讓部分使用者的語音原則可為所有透過「網站 2 閘道」輸出的通話定義路由。雖然這些使用者位於網站 1，但他們的輸出通話將會透過「網站 1 閘道」路由傳送。

當使用者位於已針對位置基礎路由設定的網站時，網站的語音路由原則路由會覆寫使用者的語音原則路由。此規則對於暫時移至不同網站的使用者而言特別有用。在此特定個案中，使用者將會固定使用其所在位置的本機閘道；如果「Lync 使用者 3」位於「網站 2」，所有該使用者的輸出通話都將會透過「網站 2 閘道」路由傳送，但如果該使用者前往網站 1，則所有他於網站 1 撥打的輸出通話都將會透過「網站 1 閘道」路由傳送。

下表說明 Lync 使用者 1 從下列網站撥打輸出通話時的使用者體驗。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>網站 1</th>
<th>網站 2</th>
<th>未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>輸出通話授權</p></td>
<td><p>Lync 使用者 1 語音原則</p></td>
<td><p>Lync 使用者 1 語音原則</p></td>
<td><p>Lync 使用者 1 語音原則</p></td>
</tr>
<tr class="even">
<td><p>輸出通話路由</p></td>
<td><p>網站 1 語音路由原則</p></td>
<td><p>網站 2 語音路由原則</p></td>
<td><p>使用者的語音原則，且僅適用於未啟用位置基礎路由的系統</p></td>
</tr>
</tbody>
</table>


## 通話轉接和來電轉接

當轉接通話或來電時，通話的路由會受到位置基礎路由的影響。

下表說明 Lync 使用者 1 轉接 PSTN 通話或來電給其他使用者的情況。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>使用者起始通話轉接或來電轉接</th>
<th>Lync 使用者 2</th>
<th>Lync 使用者 4</th>
<th>位於未啟用位置基礎路由網站的 Lync 使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 使用者 1</p></td>
<td><p>允許來電轉接或通話轉接</p></td>
<td><p>不允許來電轉接或通話轉接</p></td>
<td><p>不允許來電轉接或通話轉接</p></td>
</tr>
</tbody>
</table>

  
下表說明位置基礎路由如何影響通話路由傳送到 PSTN 端點的方式。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>要轉接通話或來電的目標端點</th>
<th>Lync 使用者 2</th>
<th>Lync 使用者 4</th>
<th>位於未啟用位置基礎路由網站的 Lync 使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PSTN 端點</p></td>
<td><p>通話或來電轉接會經網站 1 語音路由原則路由傳送並透過網站 1 閘道輸出</p></td>
<td><p>通話或來電轉接會經網站 2 語音路由原則路由傳送並透過網站 2 閘道輸出</p></td>
<td><p>通話或來電轉接會經 Lync 使用者語音原則路由傳送並透過未啟用位置基礎路由的閘道輸出 (如果有的話)</p></td>
</tr>
</tbody>
</table>


## 同時響鈴

在範例拓撲中設定位置基礎路由後，會執行下列互動。

下表說明位置基礎路由是否允許針對不同的 Lync 使用者 (亦即 Lync 使用者 2、Lync 使用者 4 等) 同時響鈴。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>匯入 PSTN 通話目標</th>
<th>Lync 使用者 2</th>
<th>Lync 使用者 4</th>
<th>位於未啟用位置基礎路由網站的 Lync 使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 使用者 1</p></td>
<td><p>允許同時響鈴</p></td>
<td><p>不允許同時響鈴</p></td>
<td><p>不允許同時響鈴</p></td>
</tr>
</tbody>
</table>

  
下表說明位置基礎路由是否允許從不同的 Lync 使用者 (亦即 Lync 使用者 2、Lync 使用者 4 等) 同時向 PSTN 端點響鈴。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>同步響鈴目標</th>
<th>Lync 使用者 2</th>
<th>Lync 使用者 4</th>
<th>位於未啟用位置基礎路由網站的 Lync 使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 使用者 1 行動電話 (PSTN 端點)</p></td>
<td><p>通話會經網站 1 的語音路由原則路由傳送並透過網站 1 閘道輸出</p></td>
<td><p>通話會經網站 2 的語音路由原則路由傳送並透過網站 2 閘道輸出</p></td>
<td><p>來電者語音原則路由傳送並將透過未啟用位置基礎路由的 PSTN 閘道輸出</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃位置基礎路由](lync-server-2013-planning-for-location-based-routing.md)


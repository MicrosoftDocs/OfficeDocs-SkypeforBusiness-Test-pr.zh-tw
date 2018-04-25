---
title: Lync Server 2013：規劃簡單 URL
TOCTitle: 規劃簡單 URL
ms:assetid: 20e4f4b6-b7ff-4297-b00d-d1211ee800ac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398287(v=OCS.15)
ms:contentKeyID: 49290314
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃簡單 URL

 

_**上次修改主題的時間：** 2015-03-09_

簡單 URL 可讓您的使用者更容易加入會議中，讓系統管理員更易於存取 Lync Server 系統管理工具。

Lync Server 支援 3 個簡單 URL：

  - Meet 可作為網站或組織中所有會議的基底 URL。舉例來說，https://meet.contoso.com 即為 Meet 簡單 URL。特定的會議 URL 可如 https://meet.contoso.com/*username*/7322994。
    
    透過 Meet 簡單 URL，加入會議的連結可更容易理解，且更容易溝通與分送。

  - **Dial-in** 可讓使用者存取 \[電話撥入式會議設定\] 網頁。此頁面會顯示會議撥入號碼及其可用語言、指派的會議資訊 (即針對不需排程的會議所提供的資訊) 與會議中 DTMF 控制項，並可讓使用者管理其個人識別碼 (PIN) 與指派的會議資訊。Dial-in 簡單 URL 會包含在所有的會議邀請中，讓想要撥號參加會議的使用者能夠存取所需的電話號碼與 PIN 資訊。舉例來說，https://dialin.contoso.com 即為 Dial-in 簡單 URL。

  - **Admin** 可讓使用者快速存取 Lync Server 控制台。在位於組織防火牆內的任何電腦上，系統管理員均可在瀏覽器中輸入 Admin 簡單 URL 藉以開啟 Lync Server 控制台。Admin 簡單 URL 是您組織內部的 URL。舉例來說，https://admin.contoso.com 即為 Admin 簡單 URL。

## 簡單 URL 範圍

您可以設定全域範圍的簡單 URL，或為您組織中的每個中央網站指定不同的簡單 URL。如果您同時指定了全域簡單 URL 與網站簡單 URL，將會優先使用網站簡單 URL。

一般情況下，建議您在全域層級設定簡單 URL 即可，因為在此設定下，即便使用者在網站間移動，其 Meet 簡單 URL 也不會變更。不同網站上的撥入使用者需要使用不同電話號碼的組織，則屬例外。請注意，如果您在網站上將某個簡單 URL (如 Dial-in 簡單 URL) 設定為網站層級簡單 URL，則必須將該網站上的其他簡單 URL 也設定為網站層級。

您可以在 拓撲產生器中設定全域簡單 URL。若要在網站層級上設定簡單 URL，您必須使用 Set-CsSimpleURLConfiguration Cmdlet。

## 為簡單 URL 命名

我們提供了三種建議選項讓您為簡單 URL 命名。您所選擇的選項，將會影響您對支援簡單 URL 的 DNS A 記錄與憑證進行設定的方式。在每個選項中，您都必須為組織中的每個 SIP 網域設定一個 Meet 簡單 URL。

但無論您有多少個 SIP 網域，您的整個組織中都只需要一個 Dial-in 簡單 URL 與一個 Admin 簡單 URL。

如需有關所需 DNS A 記錄與憑證的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中簡單 URL 的 DNS 需求](lync-server-2013-dns-requirements-for-simple-urls.md)＞與＜ [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)＞。

在「選項 1」中，您會為每個簡單 URL 建立一個新的 SIP 網域名稱。

如果您使用此選項，您的每個簡單 URL 都必須要有個別的 DNS A 記錄，且每個 Meet 簡單 URL 都必須在憑證中命名。

### 簡單 URL 命名選項 1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>簡單 URL</strong></p></td>
<td><p><strong>範例</strong></p></td>
</tr>
<tr class="even">
<td><p>會議 (Meet)</p></td>
<td><p>https://meet.contoso.com、https://meet.fabrikam.com 等等 (組織中的每個 SIP 網域各一個)</p></td>
</tr>
<tr class="odd">
<td><p>撥入</p></td>
<td><p>https://dialin.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Admin</p></td>
<td><p>https://admin.contoso.com</p></td>
</tr>
</tbody>
</table>


使用「選項 2」時，簡單 URL 會以網域名稱 lync.contoso.com 為基礎。因此，您只需要一個 DNS A 記錄即可啟用這三種簡單 URL。此 DNS A 記錄會參考 lync.contoso.com。此外，您的組織中其他的 SIP 網域仍需要個別的 DNS A 記錄。

### 簡單 URL 命名選項 2

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>簡單 URL</strong></p></td>
<td><p><strong>範例</strong></p></td>
</tr>
<tr class="even">
<td><p>會議 (Meet)</p></td>
<td><p>https://lync.contoso.com/Meet、https://lync.fabrikam.com/Meet 等等 (組織中的每個 SIP 網域各一個)</p></td>
</tr>
<tr class="odd">
<td><p>撥入</p></td>
<td><p>https://lync.contoso.com/Dialin</p></td>
</tr>
<tr class="even">
<td><p>Admin</p></td>
<td><p>https://lync.contoso.com/Admin</p></td>
</tr>
</tbody>
</table>


如果您有許多 SIP 網域，並且想讓它們有個別的 Meet 簡單 URL，但也想盡可能降低這些簡單 URL 的 DNS 記錄與憑證需求，「選項 3」將可發揮最佳功效。

### 簡單 URL 命名選項 3

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>簡單 URL</strong></p></td>
<td><p><strong>範例</strong></p></td>
</tr>
<tr class="even">
<td><p>會議 (Meet)</p></td>
<td><p>https://lync.contoso.com/contosoSIPdomain/Meet</p>
<p>https://lync.contoso.com/fabrikamSIPdomain/Meet</p></td>
</tr>
<tr class="odd">
<td><p>撥入</p></td>
<td><p>https://lync.contoso.com/Dialin</p></td>
</tr>
<tr class="even">
<td><p>Admin</p></td>
<td><p>https://lync.contoso.com/Admin</p></td>
</tr>
</tbody>
</table>


## 簡單 URL 命名與驗證規則

拓撲產生器與 Lync Server 管理命令介面Cmdlet 會對您的簡單 URL 施加數個驗證規則。您必須設定 Meet 與 Dialin 的簡單 URL，但可選擇是否為 Admin 設定。每個 SIP 網域都必須有個別的 Meet 簡單 URL，但您整個組織只需要一個 Dialin 簡單 URL 與一個 Admin 簡單 URL。

組織中的每個簡單 URL 都必須要有唯一名稱，且不可以是其他簡單 URL 的首碼 (例如，將 lync.contoso.com/Meet 設定為 Meet 簡單 URL，lync.contoso.com/Meet/Dialin 設定為 Dialin 簡單 URL，是不被允許的)。簡單 URL 名稱不可包含您任何集區的 FQDN，或是任何連接埠資訊 (例如，https://FQDN:88/meet 是不被允許的)。所有簡單 URL 都必須以 https:// 開頭。

簡單 URL 只能包含英數字元，即 a-z、A-Z、0-9 與點 (.)。如果您使用其他字元，簡單 URL 可能無法如預期般運作。

## 在部署後變更簡單 URL

如果您在初始部署後變更了簡單 URL，您必須注意變更會對簡單 URL 的 DNS 記錄與憑證造成何種影響。如果簡單 URL 的基底有所變更，您也必須變更 DNS 記錄和憑證。例如，從 https://lync.contoso.com/Meet 變更為 https://meet.contoso.com 會使基底 URL 從 lync.contoso.com 變更為 meet.contoso.com，所以您需要將 DNS 記錄和憑證變更成指向 meet.contoso.com。如果您將簡單 URL 從 https://lync.contoso.com/Meet 變更為 https://lync.contoso.com/Meetings，則基底 URL lync.contoso.com 維持不變，所以不需要變更 DNS 或憑證。

但只要您變更了簡單 URL 名稱，您就必須在每個 Director 與前端伺服器上執行 **Enable-CsComputer**，以登錄變更。

## 請參閱

#### 概念

[Lync Server 2013 中簡單 URL 的 DNS 需求](lync-server-2013-dns-requirements-for-simple-urls.md)


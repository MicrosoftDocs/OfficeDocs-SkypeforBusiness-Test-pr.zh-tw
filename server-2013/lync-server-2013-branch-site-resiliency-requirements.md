---
title: Lync Server 2013：分支網站復原需求
TOCTitle: 分支網站復原需求
ms:assetid: a570922c-52bd-42d7-bd64-226578b3d110
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412772(v=OCS.15)
ms:contentKeyID: 49291895
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的分支網站復原需求

 

_**上次修改主題的時間：** 2015-03-09_

本主題有助於讓使用者做好分支網站恢復和語音信箱生存能力的準備，同時還詳述相關的硬體與軟體需求。

## 讓分公司使用者做好分支網站恢復的準備

若要讓使用者做好分支網站恢復的準備，請將其登錄器集區設為 Survivable Branch Appliance (SBA) 或 Survivable Branch 伺服器。

## 分公司使用者的登錄器指派

無論您選擇哪個分支網站恢復解決方案，都需要為每個使用者指派主要登錄器。分支網站使用者應一律向分支網站的登錄器註冊，無論該登錄器位在 Survivable Branch Appliance、 Survivable Branch 伺服器 或獨立的 Lync Server 2013 Standard 或 Enterprise Edition Server 中，都是如此。需要有網域名稱系統 (DNS) 服務 (SRV) 記錄，如此用戶端才可探索其登錄器集區。如果 Survivable Branch Appliance 變成無法使用，這是分支網站用戶端將用來自動探索備份登錄器的方法。

如果分支網站沒有 DNS 伺服器，有兩個替代方式可設定 Survivable Branch Appliance 或 Survivable Branch 伺服器 的探索：

  - 在分支網站的動態主機設定通訊協定 (DHCP) 伺服器上設定 DHCP 選項 120，以指向 Survivable Branch Appliance 或 Survivable Branch 伺服器 的完整網域名稱 (FQDN)。

  - 設定 Survivable Branch Appliance 或 Survivable Branch 伺服器 以回應 DHCP 120 查詢。

## 分公司使用者的語音路由

建議您為分支網站中的使用者建立不同的使用者層級 VoIP 原則。此原則應包含一個使用 Survivable Branch Appliance 或分支伺服器閘道的主要路由，以及一或多個使用中央網站上具有公用交換電話網路 (PSTN) 閘道之主幹的備份路由。如果主要路由無法使用，則會改用使用一或多個中央網站閘道的備份路由。如此一來，無論使用者在何處註冊 (在分支網站登錄器或中央網站的備份登錄器集區)，使用者的 VoIP 原則永遠有效。這是容錯移轉案例的重要考量。比如，如果您需要重命名 Survivable Branch Appliance 或重新設定 Survivable Branch Appliance，以連接至中央網站的備份登錄器集區，那麼在此期間您必須將分支網站使用者移動至中央網站 (如需重新命名或重新設定Survivable Branch Appliance 的詳細資訊，請參閱部署文件中的[Lync Server 2013 中的附錄 B：管理 Survivable Branch Appliance](lync-server-2013-appendix-b-managing-a-survivable-branch-appliance.md))。如果這些使用者沒有使用者層級 VoIP 原則或使用者層級撥號對應表，則將使用者移動至其他網站時，預設會對使用者套用中央網站的網站層級 VoIP 原則和網站層級撥號對應表，而不是套用分支網站的網站層級 VoIP 原則和撥號對應表。在此例中，除非備份登錄器集區使用的網站層級 VoIP 原則與網站層級撥號對應表也能套用至分支網站使用者，否則其通話將會失敗。例如，日本分支網站的使用者被移動至 Redmond 中央網站，那麼在所有的 7 位數電話前面加上 +1425 的正規化規則撥號對應表，就無法正確地為這些使用者轉譯電話。

> [!IMPORTANT]  
> 當您建立分公司備份路由時，建議您將兩個 PSTN 電話使用方式記錄新增至分公司使用者原則，並將不同的路由指派給每個記錄。第一個 (或主要) 路由會將通話導向至與 Survivable Branch Appliance (SBA) 或分公司伺服器相關聯的閘道；第二個 (或備份) 路由會將通話導向至中央網站的閘道。在導向通話時，SBA 或分公司伺服器會先嘗試指派給第一個 PSTN 使用方式記錄的所有路由，然後再嘗試第二個使用方式記錄。



若要確保在分支閘道或 Survivable Branch Appliance 網站的 Windows 元件無法使用時 (例如， Survivable Branch Appliance 或分支閘道關機進行維護時會發生此情況)，對分支網站使用者的來電會路由傳送給這些使用者，請在閘道上建立容錯移轉路由 (或與您的直接內部撥號 (DID) 提供者合作)，以將來電重新導向至中央網站的備份登錄器集區。在這裡，會透過 WAN 連結將來電路由傳送給分公司使用者。請確定路由會轉譯號碼以符合 PSTN 閘道或其他對等主幹接受的電話號碼格式。如需關於建立容錯移轉路由的詳細資訊，請參閱＜ [在 Lync Server 2013 中設定容錯移轉路由](lync-server-2013-configuring-a-failover-route.md)＞。另外，請為與分支網站上的閘道相關聯的主幹建立服務層級撥號對應表，以正規化來電。如果您在分支網站有兩個 Survivable Branch Appliance，除非需要個別的服務層級對應表，否則可以建立兩者共用的網站層級撥號對應表。

> [!NOTE]  
> 為了針對任何一個分支網站裡倚賴中央網站以獲得顯示狀態、會議或容錯移轉功能的使用者，記錄其對中央網站資源的使用情況，建議您將每位分支網站使用者視為向中央網站註冊的使用者。對於分支網站使用者的數量，包括向 Survivable Branch Appliance註冊的使用者，目前並沒有限制。



我們也建議您建立使用者層級撥號對應表和語音原則，然後將它指派給分支網站使用者。如需詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞及＜ [在 Lync Server 2013 中為分支使用者建立 VoIP 路由原則](lync-server-2013-create-the-voip-routing-policy-for-branch-users.md)＞。

## 路由傳送分機號碼

為分支網站使用者準備撥號對應表和語音原則時，請確定其中包含了正規化規則和轉譯規則，而且這些規則必須符合 msRTCSIP-line (或線路 URI) 屬性中使用的字串和數字格式，如此一來，分支網站使用者與中央網站使用者之間的 Lync 2013 電話，才能正確地路由傳送；特別是，如果 WAN 連結無法使用，而必須透過 PSTN 重新路由傳送電話的情形。此外，對於包含分機號碼而不僅是電話號碼的撥號號碼而言，還有其他的特殊考量。

符合包含分機號碼之線路 URI 的正規化規則和轉譯規則，無論是單獨使用或與完整的 E.164 電話號碼一起使用，都還有其他的要求。本節提供數個範例案例，說明如何路由傳送包含分機號碼之線路 URI 的電話。

如果組織沒有為個別使用者設定直接向內撥號 (DID) 電話號碼，並且每位使用者的線路 URI 已設定為「只是」 分機號碼，則內部使用者只要撥打分機號碼，就能與對方通話。但是，您必須設定正規化規則，可以套用至從分支網站使用者打給符合分機號碼之中央網站使用者的電話。

在分支網站和中央網站之間的 WAN 連結可用時，從分支網站使用者撥給中央網站使用者的電話不需要符合正規化規則即可轉譯號碼，因為電話不是透過 PSTN 路由傳送的。例如：


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
<th>規則名稱</th>
<th>說明</th>
<th>號碼模式</th>
<th>轉譯</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5digitExtensions</p></td>
<td><p>不轉譯 5 位數號碼</p></td>
<td><p>^(\d{5})$</p></td>
<td><p>$1</p></td>
<td><p>10001 不會被轉譯</p></td>
</tr>
</tbody>
</table>


您也必須考慮特定情況的分機號碼；例如，當分支網站和中央網站之間的 WAN 連結無法使用，而來自分支網站的電話必須經由 PSTN 路由傳送時。在 WAN 中斷期間，如果分支網站使用者僅透過撥打分機號碼來打電話給中央網站使用者時，您的輸出轉譯規則中必須新增中央網站使用者的完整電話號碼。如果使用者的線路 URI 包含組織的完整電話號碼，也包含使用者的唯一分機號碼 (而不是其唯一的完整電話號碼)，那麼您的輸出轉譯規則中必須新增組織的完整電話號碼。例如：


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>比對模式</th>
<th>轉譯</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>將 5 位數號碼轉譯為使用者的電話號碼和分機號碼</p></td>
<td><p>^(\d{5})$</p></td>
<td><p>+14255550123;ext=$1</p></td>
<td><p>10001 會轉譯為 +14255550123;ext=10001</p></td>
</tr>
<tr class="even">
<td><p>將 5 位數號碼轉譯為組織的電話號碼和使用者的分機號碼</p></td>
<td><p>^(\d{5})$</p></td>
<td><p>+14255550100;ext=$1</p></td>
<td><p>10001 會轉譯為 +14255550100;ext=10001</p></td>
</tr>
</tbody>
</table>


在此情況下，如果處理重新路由傳送至 PSTN 的主幹對等不支援分機號碼，那麼輸出轉譯規則也必須移除分機號碼。例如：


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>比對模式</th>
<th>轉譯</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>移除包含分機號碼之電話號碼中的分機號碼</p></td>
<td><p>^\+(\d*);ext=(\d*)$</p></td>
<td><p>+$1</p></td>
<td><p>+14255550123;ext=10001 會轉譯為 +14255550123</p></td>
</tr>
</tbody>
</table>


無論 WAN 連結是否可用，如果組織沒有為個別使用者設定 DID 號碼，而且使用者的線路 URI 包含組織電話號碼和使用者唯一的分機號碼，則您必須將組織的電話號碼線路 URI，設定為一個分支網站上主幹對等或 PSTN 閘道可以接通的號碼。此外，也必須將組織的電話號碼線路 URI，設定成包含其本身的唯一分機號碼，才能將電話路由傳送至該號碼。

如需關於中央網站和分支網站之間的 WAN 連結無法使用時，中央網站使用者撥打電話給分支網站使用者的詳細資訊，請參閱本主題稍後的＜準備語音信箱生存能力＞。如需撥號對應表和正規化規則的詳細資訊 (包含其他範例規則)，請參閱規劃文件中的＜ [Lync Server 2013 中的撥號對應表和正規化規則](lync-server-2013-dial-plans-and-normalization-rules.md)＞及部署文件中的＜ [在 Lync Server 2013 中設定撥號對應表](lync-server-2013-configuring-dial-plans.md)＞。如需輸出轉譯規則的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的轉譯規則](lync-server-2013-translation-rules.md)＞及部署文件中的＜ [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)＞。

## 準備語音信箱生存能力

Exchange 整合通訊 (UM) 通常只會在中央網站安裝，不會在分支網站安裝。即使分支網站與中央網站之間的 WAN 連結無法使用，來電者應該仍可保留語音信箱訊息。因此，為 Exchange UM 自動語音應答電話號碼設定線路 URI，以便為分支網站使用者提供語音信箱，除了適用於該語音信箱號碼的語音原則、撥號對應表和正規化規則外，還需要特別考量。

Survivable Branch Appliance (SBA) 和 Survivable Branch 伺服器 可在 WAN 中斷期間，為分支網站使用者提供語音信箱生存能力。具體而言，如果您使用 Survivable Branch Appliance 或 Survivable Branch 伺服器，當 WAN 無法使用時，SBA 或 Survivable Branch 伺服器會將未接來電透過 PSTN 重新路由傳送至中央網站的 Exchange UM。SBA 或 Survivable Branch 伺服器也可讓使用者在 WAN 中斷期間，透過 PSTN 擷取語音信箱訊息。最後，在 WAN 中斷期間， Survivable Branch Appliance 或 Survivable Branch 伺服器會佇列未接來電通知，然後在 WAN 還原時，將這些通知上傳至 Exchange UM 伺服器。為了確保語音信箱重新路由傳送的靈活性，請確定在 Survivable Branch 伺服器上的主機檔案中，新增一個中央網站集區的 FQDN 項目，以及一個 Edge Server FQDN 項目。否則，如果您的分支網站上沒有 DNS 伺服器，DNS 解析將會逾時。

若要為分支網站使用者設定語音信箱生存能力，建議使用下列設定：

  - Microsoft Exchange 系統管理員應該將 Exchange UM 自動語音應答 (AA) 設定為只接受訊息。此設定會停用所有其他一般功能 (例如轉接給使用者或轉接給接線員)，並限制 AA 只能接受訊息。或者，Exchange 系統管理員可以使用一般 AA，或自訂為將來電路由傳送至接線員的 AA。

  - Lync Server 系統管理員應取得 AA 電話號碼，並使用該號碼做為 Survivable Branch Appliance 或分公司伺服器之語音信箱重新路由傳送設定中的 \[Exchange UM 自動語音應答\] 號碼。

  - Lync Server 系統管理員應取得 Exchange UM 使用者存取號碼，並使用該號碼做為 Survivable Branch Appliance 或 Survivable Branch 伺服器之語音信箱重新路由傳送設定中的 \[訂閱者存取\] 號碼。

  - Lync Server 系統管理員應設定 Exchange UM，以便只有一個撥號對應表與需要在 WAN 中斷期間存取語音信箱的所有分公司使用者相關聯。

  - 當 WAN 連結無法使用時，撥給分支網站使用者的電話將被路由傳送至使用者的 Exchange Unified Messaging (UM) 語音信箱，但僅限於如果套用至電話的語音原則，指定了唯一的語音信箱電話號碼，且不包含分機號碼時才會成立。

## 分支網站恢復的硬體和軟體需求

硬體和軟體需求會因您的恢復解決方案而異。

## Survivable Branch Appliance 的需求

必要的硬體和軟體已內建到 Survivable Branch Appliance 中。不過，建議每個分支網站都部署 DHCP 伺服器以取得用戶端 IP 位址；否則，當 DHCP 租用到期時，用戶端將沒有 IP 連線能力。

如果企業 DNS 伺服器只位在中央網站，則分支網站使用者在 WAN 中斷期間將無法連線至這些伺服器；因此，使用 DNS SRV (服務 (SRV) 資源記錄) 的 Lync Server 探索將會失敗。為了確保在 WAN 中斷期間立即重新路由傳送，分支網站必須快取 DNS 記錄。如果分支路由器支援 DNS 快取，請開啟 DNS 快取功能。或者，您可在分支網站部署 DNS 伺服器。這可以是獨立的伺服器，或支援 DNS 功能的 Survivable Branch Appliance 版本。如需詳細資訊，請連絡您的 Survivable Branch Appliance 提供者。

> [!NOTE]  
> 分支網站不需要有網域控制站。 Survivable Branch Appliance 會使用特殊的憑證來驗證用戶端，該憑證是它在登入時為回應用戶端的憑證要求傳送給用戶端的憑證。



Lync 用戶端可使用 DHCP 選項 120 (SIP 登錄器選項) 來探索 Lync Server。這可使用下列兩種方式之一來設定：

  - 設定分支網站的 DHCP 伺服器以回覆 DHCP 120 查詢，這些查詢會傳回 Survivable Branch Appliance 或 Survivable Branch 伺服器 上之登錄器的 FQDN。

  - 開啟 Lync Server DHCP。開啟此功能時， Lync Server 登錄器會回應 DHCP 選項 120 查詢。請注意，登錄器不會回應 DHCP 選項 120 以外的任何 DHCP 查詢。

此外，針對具有多個子網路的較大型分支網站，應該啟用 DHCP 轉接代理，以將 DHCP 選項 120 查詢轉送到 DHCP 伺服器 (設定 1) 或登錄器 (設定 2)。

最後，必須為分支網站使用者設定 企業語音，並以適當的整合通訊端點來佈建。

## Survivable Branch 伺服器的需求

Survivable Branch 伺服器的需求與 前端伺服器的需求相同。如需詳細資訊，請參閱規劃文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。

## 完整規模 Lync Server 分支網站部署的需求

如需詳細資訊，請參閱規劃文件中的＜ [判斷 Lync Server 2013 的基礎結構需求](lync-server-2013-determining-your-infrastructure-requirements.md)＞。


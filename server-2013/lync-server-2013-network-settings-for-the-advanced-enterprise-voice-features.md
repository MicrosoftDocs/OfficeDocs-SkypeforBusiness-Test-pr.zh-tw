---
title: Lync Server 2013：進階企業語音功能的網路設定
TOCTitle: 進階企業語音功能的網路設定
ms:assetid: 7f6de9e4-c8a4-44e4-8d14-21fe8c45283a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398637(v=OCS.15)
ms:contentKeyID: 49291467
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的進階企業語音功能的網路設定

 

_**上次修改主題的時間：** 2012-10-10_

Lync Server 具有三項進階的 企業語音功能：通話許可控制 (CAC)、緊急服務 (E9-1-1) 以及媒體旁路。這些功能對於網路地區、網路網站以及 Lync Server 拓撲中的每個子網路的網路網站關聯等方面，具有某些共同的組態需求。如需這些功能之部署規劃的詳細資訊，請參閱：

  - [在 Lync Server 2013 中規劃通話許可控制](lync-server-2013-planning-for-call-admission-control.md)

  - [在 Lync Server 2013 中規劃緊急服務 (E9-1-1)](lync-server-2013-planning-for-emergency-services-e9-1-1.md)

  - [在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)

如需部署這每項功能的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中部署進階 Enterprise Voice 功能](lync-server-2013-deploying-advanced-enterprise-voice-features.md)＞。

本主題將概略說明這三項進階 企業語音功能共同的組態需求。

## 網路地區

網路地區是一種網路中樞或網路骨幹，只有在通話許可控制 (CAC)、E9-1-1 和媒體旁路的組態中才會使用。

> [!NOTE]  
> 網路地區與 Lync Server 電話撥入式會議地區不同，後者是將電話撥入式會議存取號碼與一或多個 Lync Server 撥號對應表建立關聯時所需要的項目。如需電話撥入式會議地區的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-dial-in-conferencing-requirements.md">Lync Server 2013 中的電話撥入式會議需求</a>＞。



若要使用 CAC，每個網路地區都必須有一個相關聯的 Lync Server 中央網站，用以管理該地區內的媒體流量 (亦即，此網站會根據您所設定關於可否建立即時音訊或視訊工作階段的原則，來進行決策)。 Lync Server 中央網站並不代表地理位置，而是以一個或多個集區的形式設定的伺服器邏輯群組。如需中央網站的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的參考拓撲](lync-server-2013-reference-topologies.md)＞。另請參閱支援文件中的＜ [Lync Server 2013 中支援的拓撲](lync-server-2013-supported-topologies.md)＞。

若要設定網路地區，您可以使用 Lync Server 控制台的 \[網路設定\] 區段中的 \[地區\] 索引標籤，或執行 **New-CsNetworkRegion** 或 **Set-CsNetworkRegion**Lync Server 管理命令介面 Cmdlet。如需相關指示，請參閱部署文件中的＜ [在 Lync Server 2013 中建立或修改網路地區](lync-server-2013-create-or-modify-a-network-region.md)＞，或參閱 Lync Server 管理命令介面文件。

這三項進階 企業語音功能都共用同一組網路地區定義。如果您已為其中一項功能建立網路地區，即無須再為其他功能建立新的網路地區。但您可能需要修改現有的網路地區定義，以套用功能特有的設定。例如，如果您為 E9-1-1 (不需要有相關聯的中央網站) 建立網路地區後，又部署了通話許可控制，則必須修改每個網路地區定義以指定中央網站。

若要將 Lync Server 中央網站與網路地區建立關聯，您可以使用 Lync Server 控制台的 \[網路設定\] 區段或是執行 **New-CsNetworkRegion** 或 **Set-CsNetworkRegion**Lync Server 管理命令介面 Cmdlet，以指定中央網站名稱。如需相關指示，請參閱部署文件中的＜ [在 Lync Server 2013 中建立或修改網路地區](lync-server-2013-create-or-modify-a-network-region.md)＞，或參閱 Lync Server 管理命令介面文件。

## 網路網站

網路網站代表地理位置，例如分公司、地區辦事處或總公司。每個網路網站都必須與某個網路地區相關聯。

> [!NOTE]  
> 只有進階 企業語音功能才會使用網路網站。網路網站與您在 Lync Server 拓撲中設定的分支網站並不相同。如需分支網站的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-reference-topologies.md">Lync Server 2013 中的參考拓撲</a>＞。另請參閱支援文件中的＜ <a href="lync-server-2013-supported-topologies.md">Lync Server 2013 中支援的拓撲</a>＞。



若要設定網路網站並指定其相關聯的網路地區，您可以使用 Lync Server 控制台的 \[網路設定\] 區段，或執行 Lync Server 管理命令介面**New-CsNetworkSite** 或 **Set-CsNetworkSite** Cmdlet。如需相關指示，請參閱部署文件中的＜ [在 Lync Server 2013 中建立或修改網站](lync-server-2013-create-or-modify-a-network-site.md)＞，或參閱 Lync Server 管理命令介面文件。

## 識別 IP 子網路

對於每一個網站，您需要和網路管理員一同決定要指派給每一個網站的 IP 子網路。如果您的網路管理員已經整理好各個網路地區與網站的 IP 子網路，您的工作將會大幅簡化。

例如，可以將指派以下 IP 子網路給北美洲區域內的紐約網站：172.29.80.0/23, 157.57.216.0/25, 172.29.91.0/23, 172.29.81.0/24. 假設平常在 Detroit 工作的 Bob 要到 New York 分公司受訓。當他開啟自己的電腦並連線至網路時，他的電腦會取得分配給紐約的四個範圍內的其中一個 IP 位址，例如，172.29.80.103。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在伺服器網路組態期間所指定的 IP 子網路，必須符合用戶端電腦所提供的格式，以便正確運用在媒體旁路上。 Lync 用戶端會接受本地 IP 位址並以關聯的子網路遮罩來遮蔽該 IP 位址。在決定每個用戶端所關聯的旁路 ID 時，登錄器會將每個網站所關聯的 IP 子網路清單與用戶端所提供的子網路進行比較，確定兩者完全相符。因此，在伺服器網路組態期間所輸入的子網路必須是實際的子網路，而非虛擬子網路，這點請務必注意(如果您部署了通話許可控制，但缺少媒體旁路，即便您設定了虛擬子網路，通話許可控制還是可以正常運作)。<br />
例如，當 Lync 用戶端以 172.29.81.57 的 IP 位址及 255.255.255.0 的 IP 子網路登入電腦，會要求提供與子網路 172.29.81.0 關聯的旁路 ID。如果子網路定義為 172.29.0.0/16，則儘管用戶端屬於虛擬子網路，登錄器仍舊不會將其視為完全相符，因為登錄器所尋找的是真正的子網路 172.29.81.0。因此，系統管理員必須一字不差地輸入 Lync 用戶端所提供的子網路 (此位址是在網路組態期間靜態提供，或由動態主機設定通訊協定 (DHCP) 服務動態提供)。</td>
</tr>
</tbody>
</table>


## 建立子網路與網路網站的關聯

企業網路中的每個子網路都必須與某個網路網站相關聯 (亦即，每個子網路都必須與某個地理位置相關聯)。子網路的這項關聯可讓進階 企業語音功能找出端點的地理位置。例如，找出端點位置後，CAC 可以調節進出該網路網站的即時音訊與視訊資料流量。

若要建立子網路與網路網站的關聯，您可以使用 Lync Server 控制台的 \[網路設定\] 區段，也可以使用 Lync Server 管理命令介面。如需相關指示，請參閱部署文件中的 [在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)，或參閱 Lync Server 管理命令介面文件。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃通話許可控制](lync-server-2013-planning-for-call-admission-control.md)  
[在 Lync Server 2013 中規劃緊急服務 (E9-1-1)](lync-server-2013-planning-for-emergency-services-e9-1-1.md)  
[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)


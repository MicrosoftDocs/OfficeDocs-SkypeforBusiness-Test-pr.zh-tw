---
title: Lync Server 2013 網站
TOCTitle: 網站
ms:assetid: 022cb6dd-37e2-4882-a53e-5ddfdbc6f53a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398076(v=OCS.15)
ms:contentKeyID: 49289904
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 Lync Server 網站

 

_**上次修改主題的時間：** 2012-10-16_

在 Lync Server 中，您可以定義網路上含有 Lync Server 元件的「網站」 。網站是以高速、低延遲網路來妥善連線的一組電腦，例如單一區域網路 (LAN) 或以高速光纖網路連接的兩個網路。請注意， Lync Server 網站的概念不同於 Active Directory 網域服務 網站和 Microsoft Exchange Server 網站。 Lync Server 網站不必對應至 Active Directory 網站。

## 網站類型

每一個網站可以是「中央網站」 (至少包含一個 前端集區或 Standard Edition 伺服器) 或 「分支網站」 。每一個分支網站都剛好與一個中央網站相關聯，而分支網站的使用者會從相關聯中央網站的伺服器取得大多數的 Lync Server 功能。

每一個分支網站都包含下列其中一項：

  - 「Survivable Branch Appliance (SBA)」 ，這是符合工業標準的刀鋒伺服器，並有在 Windows Server 上執行的 Lync Server 登錄器和中繼伺服器。 Survivable Branch Appliance 也包含公用交換電話網路 (PSTN) 閘道。 Survivable Branch Appliance 是特別針對具有 25 至 1000 位使用者的分支網站所設計。

  - 「Survivable Branch 伺服器 (SBS)」 ，這是執行 Windows Server 的伺服器，其符合指定的硬體需求，並已安裝 Lync Server 登錄器和中繼伺服器軟體。該伺服器必須將 PSTN 閘道或 SIP 主幹連線至電話服務提供者。Survivable Branch 伺服器特別針對具有 1000 至 5000 位用者的分支網站所設計。

  - PSTN 閘道和「中繼伺服器」 (選用)。如需此伺服器角色及其他伺服器角色的詳細資訊，請參閱＜ [Lync Server 2013 中的伺服器角色](lync-server-2013-server-roles.md)＞。

具有中央網站的可恢復廣域網路 (WAN) 連結的分公司可以使用第三個選項，也就是 PSTN 閘道和中繼伺服器 (選用)。具有較難恢復連結的分公司網站應使用 Survivable Branch Appliance 或 Survivable Branch 伺服器，以便在廣域網路故障期間具有恢復能力。例如，在已部署 Survivable Branch Appliance 或 Survivable Branch 伺服器的網站中，如果從分支網站連接至中央網站的 WAN 網路故障，使用者仍然可以撥打和接聽企業語音電話。如需 Survivable Branch Appliance、Survivable Branch 伺服器及恢復功能的詳細資訊，請參閱規劃文件中的＜[在 Lync Server 2013 中規劃企業語音復原](lync-server-2013-planning-for-enterprise-voice-resiliency.md)＞。

## 網站拓撲

您的部署必須包含至少一個中央網站，並可以包含零到多個分支網站。每一個分支網站均隸屬於一個中央網站。中央網站會將不在分支網站本機的 Lync Server 服務 (例如，目前狀態和會議) 提供給分支網站。

如果您有多個網站，您可以將不同網站的前端集區配對在一起，以啟用嚴重損壞修復功能。如需詳細資訊，請參閱＜ [Lync Server 2013 中的高可用性和災害復原支援](lync-server-2013-high-availability-and-disaster-recovery-support.md)＞。

## 請參閱

#### 概念

[Lync Server 2013 中的伺服器角色](lync-server-2013-server-roles.md)  
[Lync Server 2013 中的高可用性和災害復原支援](lync-server-2013-high-availability-and-disaster-recovery-support.md)  

#### 其他資源

[在 Lync Server 2013 中規劃企業語音復原](lync-server-2013-planning-for-enterprise-voice-resiliency.md)


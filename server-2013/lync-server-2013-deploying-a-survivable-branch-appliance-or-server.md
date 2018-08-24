---
title: Lync Server 2013：部署 Survivable Branch Appliance 或 Survivable Branch Server
TOCTitle: 部署 Survivable Branch Appliance 或 Survivable Branch Server
ms:assetid: cb780c14-dc5f-41ba-8092-f20ae905bd16
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398849(v=OCS.15)
ms:contentKeyID: 49292336
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server

 

_**上次修改主題的時間：** 2014-12-10_

可恢復的 企業語音指的是分支網站恢復能力，也就是與中央網站的連結發生無法使用的情況時，可繼續為分支網站使用者提供 企業語音服務的能力。

針對中小型分支網站 (擁有 25 到 1,000 位使用者的分支網站)，我們建議部署 Survivable Branch Appliance，它會使用其內建的 PSTN 閘道或 SIP 主幹 (連至電話服務提供者) 來終止公用交換電話網路 (PSTN) 通話。 Survivable Branch Appliance 是協力廠商裝置，它包含執行 Windows Server 2008 R2 作業系統、 Lync Server 2013 登錄器、 中繼伺服器軟體和 PSTN 閘道的刀鋒伺服器，且全部位在單一設備底座中。

針對擁有 1,000 到 5,000 個使用者且沒有可恢復之 WAN 的分支網站，我們建議使用連線到 PSTN 閘道或 SIP 主幹 (連至電話服務提供者) 的 Survivable Branch 伺服器。 Survivable Branch 伺服器 是 Windows Server 電腦，其中安裝了登錄器和 中繼伺服器軟體。

> [!NOTE]
> 對於擁有超過 5,000 個使用者及專屬 Lync Server 系統管理員的分支網站，我們建議使用完整的 Lync Server 2013 部署，並與中央網站的部署分開。<br />
> 如需關於為貴組織中的分支網站選擇最佳恢復解決方案的詳細資訊，包括先決條件和規劃考量，請參閱規劃文件中的 <a href="lync-server-2013-branch-site-resiliency-requirements.md">Lync Server 2013 的分支網站復原需求</a>。


## 本章節內容

  - [使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server - 中央網站工作](lync-server-2013-deploying-a-survivable-branch-appliance-or-server-central-site-tasks.md)

  - [使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Server - 分支網站工作](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md)

  - [在 Lync Server 2013 中為分支網站恢復設定使用者](lync-server-2013-configuring-users-for-branch-site-resiliency.md)

  - [在 Lync Server 2013 中將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-home-users-on-a-survivable-branch-appliance-or-server.md)

  - [Lync Server 2013 中的附錄：Survivable Branch Appliance 和 Survivable Branch Server](lync-server-2013-appendices-survivable-branch-appliances-and-servers.md)

## 請參閱

#### 其他資源

[部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)


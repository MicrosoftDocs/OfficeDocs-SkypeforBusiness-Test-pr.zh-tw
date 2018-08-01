---
title: Lync Server 2013：部署 Survivable Branch Appliance 或 Survivable Branch Server - 中央網站工作
TOCTitle: 部署 Survivable Branch Appliance 或 Survivable Branch Server - 中央網站工作
ms:assetid: 0f631a36-fc2e-41cd-8a0d-f27e84f4a89e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398189(v=OCS.15)
ms:contentKeyID: 49290109
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server - 中央網站工作

 

_**上次修改主題的時間：** 2012-10-18_

在中央網站完成本節中的工作。如果您正在部署 Survivable Branch 伺服器，請略過第一項工作。

> [!IMPORTANT]  
> 在您執行本節中的工作時，必須符合下列條件：
> <ul>
> <li><p>必須在中央網站設定 Lync Server。</p></li>
> <li><p>必須將分支網站的安裝技術人員加入至 RTCUniversalSBATechnicians 群組。</p></li>
> </ul>
> 此外，我們建議您執行下列作業：
> <ul>
> <li><p>在每個分支網站部署 DHCP 伺服器，讓用戶端能夠取得 IP 位址。</p></li>
> <li><p>在每個分支網站部署 DHCP 伺服器的替代方法，就是使用 Lync Server 管理命令介面 Cmdlet <strong>Set-CsRegistrarConfiguration –EnableDHCPServer $true</strong>，在 Survivable Branch Appliance 或 Survivable Branch 伺服器 上啟用 Lync Server DHCP。如需詳細資訊，請參閱規劃文件中＜<a href="lync-server-2013-branch-site-resiliency-requirements.md">Lync Server 2013 的分支網站復原需求</a>＞的＜硬體和軟體需求＞一節。</p></li>
> </ul>


## 本章節內容

  - [在 Lync Server 2013 中將 Survivable Branch Appliance 新增到 Active Directory](lync-server-2013-add-a-survivable-branch-appliance-to-active-directory.md)

  - [在 Lync Server 2013 中新增分支網站至拓撲](lync-server-2013-add-branch-sites-to-your-topology.md)

  - [在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)


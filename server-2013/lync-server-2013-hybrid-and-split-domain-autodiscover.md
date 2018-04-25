---
title: 混合與分割網域 - 自動探索
TOCTitle: 混合與分割網域 - 自動探索
ms:assetid: c855bcc5-b656-4d2d-92d6-f016f2797d3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945652(v=OCS.15)
ms:contentKeyID: 52056203
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 混合與分割網域 - 自動探索

 

_**上次修改主題的時間：** 2013-02-14_

共用 SIP 位址空間，又稱為「分割網域」部署或「混合式」部署，是一種跨內部部署與線上環境來部署使用者的設定。預期的結果是要讓使用者 (無論其主伺服器是位在內部部署或線上) 登入部署，並重新導向至其主伺服器位置。為完成此作業，會使用 Lync Server 2013 的自動探索功能來將線上使用者重新導向至線上拓撲。執行此作業需使用 Lync Server 管理命令介面、**Get-CsHostingProvider** Cmdlet 和 **Set-CsHostingProvider** Cmdlet 來設定自動探索統一資源定位器 (URL)。

## 分割網域部署的行動性

您需要收集並記錄下列部署的屬性：

  - 從 Lync Server 管理命令介面，輸入
    
        Get-CsHostingProvider

  - 在結果中尋找具有 **ProxyFQDN**屬性的線上提供者。例如，sipfed.online.lync.com。

  - 記錄 ProxyFQDN 的值。

  - 啟用內部部署 Lync Server 控制台中的同盟，允許和線上提供者建立同盟。

  - 為線上提供者啟用同盟。根據預設，所有線上使用者都會啟用網域同盟，並可與所有網域通訊。

  - 如果您將會定義封鎖及允許的網域，請決定您要明確允許或封鎖的網域。

  - 若為線上同盟，您必須規劃防火牆例外、憑證及 DNS 主機 (若使用 IPv6，則為 A 或 AAAA) 記錄。此外，您必須設定同盟原則。如需詳細資訊，請參閱＜[規劃 Lync Server 與 Office Communications Server 同盟](lync-server-2013-planning-for-lync-server-and-office-communications-server-federation.md)＞。


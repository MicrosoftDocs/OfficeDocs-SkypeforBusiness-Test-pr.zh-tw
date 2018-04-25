---
title: 檢視 Lync Server 2013 中個別 SIP 主幹的相關資訊
TOCTitle: 檢視 Lync Server 2013 中個別 SIP 主幹的相關資訊
ms:assetid: adfacb74-7ea5-4c53-934e-ba7ec59879eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721847(v=OCS.15)
ms:contentKeyID: 49890258
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視 Lync Server 2013 中個別 SIP 主幹的相關資訊

 

_**上次修改主題的時間：** 2013-02-21_

SIP 主幹用來連線至 Microsoft Lync Server 2013 Voice over IP 電話網路與公用交換電話網路。在前版產品中，主幹用來將來自中繼伺服器的撥出電話路由至 PSTN 閘道，而每個閘道限用於單一主幹。因此，PSTN 閘道與 SIP 主幹本質上是相同的。對於系統管理員來說，這表示他們只要檢視關聯 PSTN 閘道的資訊，就可檢視有關個別 SIP 主幹的資訊。

然而在 Lync Server 2013 中， 現在可將多個主幹指派給單一 PSTN 閘道；這表示閘道與主幹不再一樣。同理，這表示系統管理員必須使用新的 [Get-CsTrunk](get-cstrunk.md) Cmdlet 才能檢視個別 SIP 主幹的資訊。

可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行 Get-CsTrunk Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視所有 SIP 主幹的資訊

  - 下列命令會傳回您組織中正在使用的所有 SIP 主幹資訊：
    
        Get-CsTrunk

## 檢視特定 SIP 主幹的資訊

  - 此命令只會傳回具有 PstnGateway:192.168.0.240 身分識別的 SIP 主幹的資訊：
    
        Get-CsTrunk -Identity "PstnGateway:192.168.0.240"

## 檢視指派到集區的所有 SIP 主幹資訊

  - 在此範例中，會傳回指派到 atl-cs-001.litwareinc.com 集區的所有 SIP 主幹資訊：
    
        Get-CsTrunk -PoolFqdn "atl-cs-001.litwareinc.com"


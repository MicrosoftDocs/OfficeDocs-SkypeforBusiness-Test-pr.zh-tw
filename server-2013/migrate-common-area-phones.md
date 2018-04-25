---
title: 移轉公共區域電話
TOCTitle: 移轉公共區域電話
ms:assetid: 31bd26fc-861b-45c6-8221-18df16e575de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688015(v=OCS.15)
ms:contentKeyID: 49890008
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉公共區域電話

 

_**上次修改主題的時間：** 2012-09-29_

公共區域電話為最常在共用工作區或公共區域 (例如大廳、廚房或工廠) 的 IP 電話。公共區域電話不需要連線至提供 Lync Server UC 功能的電腦。將 Lync Server 2010 部署移轉至 Lync Server 2013 後，您還必須移轉與舊版公共區域電話相關的連絡人物件。使用 Lync Server 管理命令介面先擷取與 Lync Server 2010 公共區域電話相關的連絡人物件，然後將這些物件移至 Lync Server 2013 集區。

**移轉公共區域電話**

1.  從 Lync Server 2013 前端伺服器開啟 Lync Server 管理命令介面。

2.  從命令列輸入下列命令：
    
        Get-CsCommonAreaPhone -Filter {RegistrarPool -eq "pool01.contoso.net"} | Move-CsCommonAreaPhone -Target pool02.contoso.net

3.  若要確認是否已將所有連絡人物件移至 Lync Server 2013 集區，請從 Lync Server 管理命令介面輸入下列命令：
    
        Get-CsCommonAreaPhone -Filter {RegistrarPool -eq "pool02.contoso.net"}
    
    確認所有連絡人物件現已關聯至 Lync Server 2013 集區。


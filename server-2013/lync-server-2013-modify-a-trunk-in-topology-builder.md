---
title: 在 Lync Server 2013 的拓撲產生器中修改主幹
TOCTitle: 在 Lync Server 2013 的拓撲產生器中修改主幹
ms:assetid: 81055a82-c6f8-47b2-9779-223b1d842f36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688110(v=OCS.15)
ms:contentKeyID: 49890141
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 的拓撲產生器中修改主幹

 

_**上次修改主題的時間：** 2012-09-21_

請依照下列步驟，修改主幹的替代媒體 IP 位址和替代旁路識別碼。

## 修改主幹的替代媒體 IP 位址

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsPstnGateway Cmdlet，並修改 Lync Server 管理命令介面中的 \[AlternateBypassId\] 欄位。
    
        Set-CsPstnGateway -Identity "PstnGateway:<peer FQDN> -RepresentativeMediaIP <IP address>

## 修改主幹的替代 BypassID

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsPstnGateway Cmdlet，並修改 Lync Server 管理命令介面中的 \[AlternateBypassId\] 欄位。
    
        Set-CsPstnGateway -Identity "PstnGateway:<peer FQDN> -AlternateBypassID <identifier>


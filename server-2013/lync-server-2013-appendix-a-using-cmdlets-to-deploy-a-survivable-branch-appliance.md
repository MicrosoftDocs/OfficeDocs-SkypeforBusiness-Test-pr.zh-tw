---
title: Lync Server 2013：附錄 A：使用 Cmdlet 部署 Survivable Branch Appliance
TOCTitle: 附錄 A：使用 Cmdlet 部署 Survivable Branch Appliance
ms:assetid: 796a26cf-7ec9-453b-8757-6153a6dd86c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398598(v=OCS.15)
ms:contentKeyID: 49291400
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的附錄 A：使用 Cmdlet 部署 Survivable Branch Appliance

 

_**上次修改主題的時間：** 2012-10-07_

本主題說明如何使用 Lync Server 管理命令介面來部署 Survivable Branch Appliance。請在中央網站執行此程序。

## 從遠端部署 Survivable Branch Appliance

1.  請遵循 [在 Lync Server 2013 中新增分支網站至拓撲](lync-server-2013-add-branch-sites-to-your-topology.md)中的程序來新增分支網站。

2.  將分支網站加入網域。

3.  將 RTCUniversalSBATechnicians 群組新增至本機 Administrators 群組。

4.  重新啟動伺服器，然後以 RTCUniversalSBATechnicians 群組成員的身分登入。

5.  在 Lync Server 管理命令介面中，輸入下列命令，以正確的組織資訊取代預留位置：
    
        Export-CsConfiguration -FileName C:\CSConfig.zip
        Import-CsConfiguration -LocalStore -FileName C:\CSConfig.zip -Verbose
        Enable-CSReplica -Verbose
        Enable-CsComputer -Verbose
        Request-CsCertificate -New -Type default -CA <YourCA> -Verbose
        Set-CsCertificate -Type Default -Thumbprint <YourCertThumbprint>
        Start-cswindowsservice -verbose


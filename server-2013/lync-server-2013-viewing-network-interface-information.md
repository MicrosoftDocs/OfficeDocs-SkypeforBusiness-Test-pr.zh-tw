---
title: 檢視網路介面資訊
TOCTitle: 檢視網路介面資訊
ms:assetid: e7dbb1ec-62b3-48be-a419-c493df5740e6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721916(v=OCS.15)
ms:contentKeyID: 49890358
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網路介面資訊

 

_**上次修改主題的時間：** 2013-02-23_

## 使用 Lync Server 管理命令介面 Cmdlet 檢視網站介面資訊

您可使用 Lync Server 管理命令介面與 **Get-CsNetworkInterface** Cmdlet，檢視網站介面資訊。您可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視網路介面資訊

  - 要檢視網路介面資訊，請在 Lync Server 管理命令介面輸入下列命令，然後按下 ENTER：
    
        Get-CsNetworkInterface
    
    此命令傳回的資訊，類似下列各網路介面的資訊：
    
        Identity              : dc.vdomain.com/Primary/1
        ComputerFqdn          : dc.vdomain.com
        IPAddress             : 0.0.0.0
        IPv6Address           :
        Interface             : Primary
        InterfaceNumber       : 1
        ConfiguredFqdn        :
        ConfiguredIPAddress   :
        ConfiguredIPv6Address :

如需詳細資訊，請參閱＜[Get-CsNetworkInterface](get-csnetworkinterface.md)＞。


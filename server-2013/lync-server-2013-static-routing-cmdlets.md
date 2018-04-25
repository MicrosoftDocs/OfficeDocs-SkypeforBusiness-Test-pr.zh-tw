---
title: 靜態路由 Cmdlet
TOCTitle: 靜態路由 Cmdlet
ms:assetid: 71d5e0cd-8412-4383-818a-95b851a4da4b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg416492(v=OCS.15)
ms:contentKeyID: 49291290
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 靜態路由 Cmdlet

 

_**上次修改主題的時間：** 2012-06-20_

使用靜態路由，系統管理員可以預先決定 SIP 訊息所採用的網路路由。伺服器在接收到訊息時，會檢查訊息位址，然後將訊息轉送至由系統管理員預先設定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。

## 靜態路由 Cmdlet

除非 Microsoft 支援人員指示，否則應該使用 [New-CsStaticRoute](new-csstaticroute.md) Cmdlet 建立針對 Microsoft Lync Server 2013 所設定的靜態路由。建立路由之後，就可以使用 CsStaticRoutingConfiguration Cmdlet，將該路由新增至靜態路由集合。

**靜態路由**

  -   
    [Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)

  -   
    [New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)

  -   
    [Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

  -   
    [Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

  -   
    [New-CsStaticRoute](new-csstaticroute.md)

  -   
    [Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)

  -   
    [New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)

  -   
    [Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

  -   
    [Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

  -   
    [New-CsSipProxyCustom](new-cssipproxycustom.md)

  -   
    [New-CsSipProxyRealm](new-cssipproxyrealm.md)

  -   
    [New-CsSipProxyTCP](new-cssipproxytcp.md)

  -   
    [New-CsSipProxyTLS](new-cssipproxytls.md)

  -   
    [New-CsSipProxyTransport](new-cssipproxytransport.md)

  -   
    [New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

  -   
    [New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

  -   
    [New-CsIssuedCertId](new-csissuedcertid.md)

## 請參閱

#### 其他資源

[Lync Server PowerShell 部落格](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x404)


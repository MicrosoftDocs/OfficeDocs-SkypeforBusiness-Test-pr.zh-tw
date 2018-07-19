---
title: 不使用範圍或身分識別的 Cmdlet
TOCTitle: 不使用範圍或身分識別的 Cmdlet
ms:assetid: 9c50c732-3c64-4b6a-96fd-8f528eb739ce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362824(v=OCS.15)
ms:contentKeyID: 56269128
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 不使用範圍或身分識別的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

修改允許清單與封鎖清單 (決定您的使用者可與哪些外部組織進行通訊的清單) 時所使用的 Cmdlet 並不會使用範圍或身分識別。事實上，**New-CsEdgeAllowAllKnownDomains** Cmdlet 也沒有任何參數。不使用範圍也不使用身分識別的 Cmdlet 包括：

  - [New-CsEdgeAllowAllKnownDomains](https://docs.microsoft.com/powershell/module/skype/New-CsEdgeAllowAllKnownDomains)

  - [New-CsEdgeAllowList](https://docs.microsoft.com/powershell/module/skype/New-CsEdgeAllowList)

  - [New-CsEdgeDomainPattern](https://docs.microsoft.com/powershell/module/skype/New-CsEdgeDomainPattern)

請注意，使用 **New-CsEdgeAllowList** Cmdlet 與 **New-CsEdgeDomainPattern** Cmdlet 時必須加上 Domain 參數，例如：

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)


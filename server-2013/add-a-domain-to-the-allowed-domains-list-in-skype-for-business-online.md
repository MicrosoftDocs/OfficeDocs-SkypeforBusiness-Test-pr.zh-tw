---
title: Lync Online：新增網域至允許的網域清單
TOCTitle: 新增網域至允許的網域清單
ms:assetid: 7b7f76c8-3047-40be-a938-8ac2868a6bc8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362818(v=OCS.15)
ms:contentKeyID: 56269121
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Online 中新增網域至允許的網域清單

 

_**上次修改主題的時間：** 2015-06-22_

初次為允許網域清單新增網域的程序分為三個步驟。首先，使用 [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) Cmdlet 為所要新增的網域建立網域物件：

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

接著，使用 [New-CsEdgeAllowList](new-csedgeallowlist.md) Cmdlet 建立包含網域物件的新允許清單：

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x

最後，使用 [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) Cmdlet 將新允許清單寫入至 商務用 Skype Online：

    Set-CsTenantFederationConfiguration -AllowedDomains $newAllowList

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


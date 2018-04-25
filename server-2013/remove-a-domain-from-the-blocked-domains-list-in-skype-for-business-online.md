---
title: 從封鎖網域清單中移除網域
TOCTitle: 從封鎖網域清單中移除網域
ms:assetid: a11ea475-bb8b-44be-a5a5-4abb2fed42b8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362830(v=OCS.15)
ms:contentKeyID: 56269135
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從封鎖網域清單中移除網域

 

_**上次修改主題的時間：** 2015-06-22_

從封鎖網域清單中移除網域的所需步驟有二：首先，您必須使用 [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) Cmdlet 建立所要移除之網域的網域物件：

    $x = New-CsEdgeDomainPattern "fabrikam.com"

建立此物件後，請使用下列語法從封鎖網域清單中移除網域 (在此範例中，網域儲存於變數 $x)：

    Set-CsTenantFederationConfiguration -BlockedDomains @{Remove=$x}

若要從封鎖網域清單中移除所有網域，請將 BlockedDomains 屬性值設為 Null ($Null)：

    Set-CsTenantFederationConfiguration -BlockedDomains $Null

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


---
title: Lync Online：新增網域至封鎖網域清單
TOCTitle: 新增網域至封鎖網域清單
ms:assetid: ea6ebeea-3031-4c42-9a2c-88eaab790636
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362853(v=OCS.15)
ms:contentKeyID: 56269164
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Online 中新增網域至封鎖網域清單

 

_**上次修改主題的時間：** 2015-06-22_

若要新增網域至封鎖網域清單，請使用類似下列的語法：

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -BlockedDomains @{Add=$x}

如您所見，此命令要求進行兩個步驟。首先，使用 [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) 建立代表要新增至封鎖清單之網域的網域物件。然後，使用 [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) Cmdlet 搭配 Add 方法將該網域 (在此範例中，網域儲存於變數 $x) 新增至清單中。

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


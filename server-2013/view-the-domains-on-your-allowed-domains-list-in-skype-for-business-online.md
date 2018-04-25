---
title: 檢視允許網域清單中的網域
TOCTitle: 檢視允許網域清單中的網域
ms:assetid: 13bceaba-5c4f-431f-864f-9e374cafa986
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362772(v=OCS.15)
ms:contentKeyID: 56269068
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視允許網域清單中的網域

 

_**上次修改主題的時間：** 2015-06-22_

若要檢視允許網域清單中的所有網域，請使用 [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) 與下列語法：

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty AllowedDomains | Select-Object AllowedDomain

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


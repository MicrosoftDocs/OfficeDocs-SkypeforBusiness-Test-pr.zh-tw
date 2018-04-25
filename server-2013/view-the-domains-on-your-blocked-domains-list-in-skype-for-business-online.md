---
title: 檢視封鎖網域清單中的網域
TOCTitle: 檢視封鎖網域清單中的網域
ms:assetid: 67c65dbf-1a68-4c77-aabd-bed5001b4267
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362797(v=OCS.15)
ms:contentKeyID: 56269100
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視封鎖網域清單中的網域

 

_**上次修改主題的時間：** 2015-06-22_

若要檢視封鎖網域清單中的所有網域，請呼叫 [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) Cmdlet，然後將傳回的資料傳送至 **Select-Object** Cmdlet：

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty BlockedDomains

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


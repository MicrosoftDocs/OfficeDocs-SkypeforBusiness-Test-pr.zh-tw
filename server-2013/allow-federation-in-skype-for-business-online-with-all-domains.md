---
title: 允許與所有網域建立同盟
TOCTitle: 允許與所有網域建立同盟
ms:assetid: d26f1057-a76c-447a-9efe-72efdce4c15e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362855(v=OCS.15)
ms:contentKeyID: 56269166
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 允許與所有網域建立同盟

 

_**上次修改主題的時間：** 2015-06-22_

若要允許您的使用者與來自任何網域的使用者進行通訊，您必須執行兩項操作：首先，使用 [New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md) Cmdlet 建立 AllowAllKnownDomains 物件的執行個體：

    $x = New-CsEdgeAllowAllKnownDomains

再者，呼叫 [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) Cmdlet，並將 AllowedDomains 屬性值設為包含 AllowAllKnownDomains 物件的變數 (在此範例中，即為 $x)：

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


---
title: 從允許網域清單中移除網域
TOCTitle: 從允許網域清單中移除網域
ms:assetid: 04948582-363b-49bd-8305-166c4c1d0dd9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362766(v=OCS.15)
ms:contentKeyID: 56269062
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從允許網域清單中移除網域

 

_**上次修改主題的時間：** 2015-06-22_

要將網域從允許網域清單中移除，需要執行一連串步驟。首先，您必須使用類似下列命令來擷取清單目前的所有網域集合：

    $x = (Get-CsTenantFederationConfiguration).AllowedDomains

接著，執行此命令以檢視這些網域：

``` 
$x
```

請注意所要移除之網域的數字次序。若是該網域為清單中的第一個網域，則該網域的索引值為 0。若是該網域為清單中的第二個網域，則索引值為 1，依此類推。

知道索引號碼後，使用類似下列命令移除指定網域，並確認使用的索引號碼正確。此命令會移除清單中的第一個網域 (索引號碼為 0)：

    $x.AllowedDomain.RemoveAt(0)

最後，呼叫 [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) Cmdlet 以將變更寫入至 商務用 Skype Online：

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


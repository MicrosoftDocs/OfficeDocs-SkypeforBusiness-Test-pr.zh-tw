---
title: 啟用/停用指定公用 IM 提供者
TOCTitle: 啟用/停用指定公用 IM 提供者
ms:assetid: 9d3e2607-01c0-4ae9-accc-39f03ce253bb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362825(v=OCS.15)
ms:contentKeyID: 56269129
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用/停用指定公用 IM 提供者

 

_**上次修改主題的時間：** 2015-06-22_

商務用 Skype Online 可讓您與位於下列一或多個公用立即訊息 (IM) 提供者的使用者建立同盟：

  - Windows Live network of Internet services

  - Yahoo\!

  - AOL

若要允許與上述一或多個提供者建立同盟，請使用 [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) Cmdlet 並將 Provider 屬性值設為下列一或多個值：

  - Windows Live

  - Yahoo

  - AOL

例如，下列命令會建立與 Windows Live 及 AOL 的同盟：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

請注意，每次要新增或移除提供者時，您必須在命令中加入所有相關的同盟提供者。例如，若要新增 Yahoo\!，請執行下列命令：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo"

此命令會將 Yahoo\! 設為唯一同盟提供者，因為其為命令中所呼叫的提供者。若要建立與這三個公用 IM 提供者的同盟，您必須加入這三個提供者：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo", "AOL","WindowsLive"

請注意，您必須在呼叫 Set-CsTenantPublicProvider Cmdlet 時加入 Tenant 參數；如果沒有，系統將提示您輸入租用戶識別碼。您可以使用下列命令傳回 商務用 Skype Online 租用戶的識別碼：

    Get-CsTenant | Select-Object TenantID

或者，使用下列命令將租用戶識別碼儲存於變數中：

    $tenantID = (Get-CsTenant | Select-Object TenantID)

接著在呼叫 Set-CsTenantPublicProvider 時使用該變數 (在此範例中，即為 $tenantID)：

    Set-CsTenantPublicProvider -Tenant $tenantID -Provider "Yahoo", "AOL","WindowsLive"

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


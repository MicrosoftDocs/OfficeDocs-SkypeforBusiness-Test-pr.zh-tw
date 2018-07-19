---
title: 使用 Tenant 參數的 Cmdlet
TOCTitle: 使用 Tenant 參數的 Cmdlet
ms:assetid: e7fe7c12-fbe0-49c1-9e8c-eef6958f27d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362850(v=OCS.15)
ms:contentKeyID: 56269161
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Tenant 參數的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

修改公用提供者設定時，一律需要提供租用戶識別碼；即使您僅有單一租用戶亦是如此。例如，此命令會將 Windows Live 設為您的使用者可與之通訊的唯一公用提供者：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

所幸您無需在每次執行這些 Cmdlet 時都要輸入租用戶識別碼 (例如 bf19b7db-6960-41e5-a139-2aa373474354)；您可以改為執行 [Get-CsTenant](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenant) Cmdlet，將租用戶識別碼儲存為變數，然後在呼叫其他 Cmdlet 時使用該變數。例如：

    $x = (Get-CsTenant).TenantId
    Set-CsTenantPublicProvider -Tenant $x -Provider "WindowsLive"

或者，您可以使用單一命令執行此操作：擷取租用戶識別碼並將該值傳送至 Set-CsTenantPublicProvider Cmdlet：

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider "WindowsLive"}

您無需在呼叫 **Get-CsTenant** Cmdlet 時指定租用戶識別碼。下列命令會傳回租用戶的相關資訊：

    Get-CsTenant

下列 Cmdlet 接受租用戶身分識別。然而，在這些案例中，參數為選用性質；您無需在呼叫 Cmdlet 時輸入參數，而是由 Windows PowerShell 根據您目前所連線的 商務用 Skype Online 以有效率的方式為您輸入租用戶身分識別：

  - [Get-CsTenant](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenant)

  - [Set-CsTenantFederationConfiguration](https://docs.microsoft.com/powershell/module/skype/Set-CsTenantFederationConfiguration)

  - [Set-CsTenantHybridConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsTenantHybridConfiguration)

  - [Get-CsTenantFederationConfiguration](https://docs.microsoft.com/powershell/module/skype/Get-CsTenantFederationConfiguration)

  - [Get-CsTenantHybridConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenantHybridConfiguration)

  - [Get-CsTenantLicensingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenantLicensingConfiguration)

例如，使用下列命令可呼叫 **Get-CsTenantFederationConfiguration** Cmdlet：

    Get-CsTenantFederationConfiguration

雖然並非必要，但在呼叫 Get-CsTenantFederationConfiguration 時可加入 Tenant 參數：

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)


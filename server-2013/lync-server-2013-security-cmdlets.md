---
title: 安全性 Cmdlet
TOCTitle: 安全性 Cmdlet
ms:assetid: 9a6c654d-287d-434e-8d93-409f0d623f5a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398799(v=OCS.15)
ms:contentKeyID: 49291791
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安全性 Cmdlet

 

_**上次修改主題的時間：** 2012-10-09_

Microsoft Lync Server 2013 包含的安全性 Cmdlet 主要用於管理驗證和使用者權限。可用來管理驗證的 Cmdlet 有許多種，包括用來驗證憑證和個人識別碼 (PIN) 的 Cmdlet。此外，另有一些 Cmdlet 可讓您使用新的角色型存取控制 (RBAC) 功能，以便委派 Lync Server 的系統管理控制。

## 安全性 Cmdlet

許多適用於安全性設定的管理工作都能從 Lync Server 控制台 執行。主要的例外是使用者權限 Cmdlet。然而，所有安全性管理工作都能從 Lync Server 管理命令介面或指令碼內部使用 Cmdlet 來執行；使用指令碼可讓您使某些工作自動化。以下是與管理安全性設定直接相關的 Cmdlet 清單：

**[憑證和驗證 Cmdlet](lync-server-2013-certificate-and-authentication-cmdlets.md)**

  -   
    [Get-CsCertificate](get-cscertificate.md)

  -   
    [Import-CsCertificate](import-cscertificate.md)

  -   
    [Remove-CsCertificate](remove-cscertificate.md)

  -   
    [Request-CsCertificate](request-cscertificate.md)

  -   
    [Set-CsCertificate](set-cscertificate.md)

  -   
    [Test-CsCertificateConfiguration](test-cscertificateconfiguration.md)

  -   
    [Get-CsClientCertificate](get-csclientcertificate.md)

  -   
    [Revoke-CsClientCertificate](revoke-csclientcertificate.md)

  -   
    [Lock-CsClientPin](lock-csclientpin.md)

  -   
    [Set-CsClientPin](set-csclientpin.md)

  -   
    [Unlock-CsClientPin](unlock-csclientpin.md)

  -   
    [Get-CsClientPinInfo](get-csclientpininfo.md)

  -   
    [New-CsKerberosAccount](new-cskerberosaccount.md)

  -   
    [Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)

  -   
    [New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

  -   
    [Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

  -   
    [Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

  -   
    [Test-CsKerberosAccountAssignment](test-cskerberosaccountassignment.md)

  -   
    [Set-CsKerberosAccountPassword](set-cskerberosaccountpassword.md)

  -   
    [Get-CsPinPolicy](get-cspinpolicy.md)

  -   
    [Grant-CsPinPolicy](grant-cspinpolicy.md)

  -   
    [New-CsPinPolicy](new-cspinpolicy.md)

  -   
    [Remove-CsPinPolicy](remove-cspinpolicy.md)

  -   
    [Set-CsPinPolicy](set-cspinpolicy.md)

  -   
    [Get-CsProxyConfiguration](get-csproxyconfiguration.md)

  -   
    [New-CsProxyConfiguration](new-csproxyconfiguration.md)

  -   
    [Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)

  -   
    [Set-CsProxyConfiguration](set-csproxyconfiguration.md)

  -   
    [Get-CsSipDomain](get-cssipdomain.md)

  -   
    [New-CsSipDomain](new-cssipdomain.md)

  -   
    [Remove-CsSipDomain](remove-cssipdomain.md)

  -   
    [Set-CsSipDomain](set-cssipdomain.md)

**[使用者權限 Cmdlet](lync-server-2013-user-rights-and-permissions-cmdlets.md)**

  -   
    [Get-CsAdminRole](get-csadminrole.md)

  -   
    [New-CsAdminRole](new-csadminrole.md)

  -   
    [Remove-CsAdminRole](remove-csadminrole.md)

  -   
    [Set-CsAdminRole](set-csadminrole.md)

  -   
    [Update-CsAdminRole](update-csadminrole.md)

  -   
    [Get-CsAdminRoleAssignment](get-csadminroleassignment.md)

  -   
    [Grant-CsOUPermission](grant-csoupermission.md)

  -   
    [Revoke-CsOUPermission](revoke-csoupermission.md)

  -   
    [Test-CsOUPermission](test-csoupermission.md)

  -   
    [Grant-CsSetupPermission](grant-cssetuppermission.md)

  -   
    [Revoke-CsSetupPermission](revoke-cssetuppermission.md)

  -   
    [Test-CsSetupPermission](test-cssetuppermission.md)

**[Interoperability Cmdlet](lync-server-2013-interoperability-cmdlets.md)**

  - [Get-CsOAuthConfiguration](get-csoauthconfiguration.md)

  - [Set-CsOAuthConfiguration](set-csoauthconfiguration.md)

  - [Get-CsOAuthServer](get-csoauthserver.md)

  - [New-CsOAuthServer](new-csoauthserver.md)

  - [Remove-CsOAuthServer](remove-csoauthserver.md)

  - [Set-CsOAuthServer](set-csoauthserver.md)

  - [Get-CsPartnerApplication](get-cspartnerapplication.md)

  - [New-CsPartnerApplication](new-cspartnerapplication.md)

  - [Remove-CsPartnerApplication](remove-cspartnerapplication.md)

  - [Set-CsPartnerApplication](set-cspartnerapplication.md)

## 請參閱

#### 其他資源

[Lync Server PowerShell 部落格](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x404)


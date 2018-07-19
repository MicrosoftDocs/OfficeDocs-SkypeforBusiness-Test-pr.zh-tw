---
title: Lync Server 2013：設定與 Lync Online 的同盟
TOCTitle: 設定與 Lync Online 的同盟
ms:assetid: a10bd1d5-c003-46db-9f57-7d55d3fa08da
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205126(v=OCS.15)
ms:contentKeyID: 49291865
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 2013 與 Lync Online 的同盟

 

_**上次修改主題的時間：** 2015-08-19_

遵循本節中的步驟以在內部部署和 商務用 Skype Online 之間設定互通性。

## 設定與 商務用 Skype Online 同盟的內部部署 Edge 服務

同盟可讓內部部署的使用者與組織中的 Office 365 使用者通訊。若要設定同盟，請執行下列 Cmdlet：

    Set-CSAccessEdgeConfiguration -AllowOutsideUsers 1 -AllowFederatedUsers 1 -UseDnsSrvRouting

    New-CSHostingProvider -Identity LyncOnline -ProxyFqdn "sipfed.online.lync.com" -Enabled $true -EnabledSharedAddressSpace $true -HostsOCSUsers $true -VerificationLevel UseSourceVerification -IsLocal $false -AutodiscoverUrl https://webdir.online.lync.com/Autodiscover/AutodiscoverService.svc/root

## 為共用 SIP 位址空間設定您的 商務用 Skype Online 租用戶

工作階段初始通訊協定 (SIP) 位址乃是網路中各個使用者的唯一識別碼，類似於電話號碼或電子郵件地址。在您嘗試將 Lync 使用者從內部部署移至 商務用 Skype Online 前，您需要設定 Office 365 租用戶，以與您的內部部署共用「共用工作階段初始通訊協定 (SIP)」位址空間。如未設定，您可能會看見下列錯誤訊息：

Move-CsUser : HostedMigration 錯誤: 錯誤=(510)，描述=(為針對共用 sip 位址空間啟用此使用者的租用戶。)

若要設定共用 SIP 位址空間，請使用 商務用 Skype Online 建立遠端 PowerShell 工作階段，然後執行下列 Cmdlet：

    Set-CsTenantFederationConfiguration -SharedSipAddressSpace $true

若要使用 商務用 Skype Online 建立遠端 PowerShell 工作階段，您必須先為 Windows PowerShell 安裝 商務用 Skype Online 模組，您可以在此取得該模組： [http://go.microsoft.com/fwlink/p/?LinkId=391911](http://go.microsoft.com/fwlink/p/?linkid=391911)。

安裝模組之後，您便可使用下列 Cmdlet 建立遠端工作階段：

    Import-Module LyncOnlineConnector

    $cred = Get-Credential

    $CSSession = New-CsOnlineSession -Credential $cred

    Import-PSSession $CSSession -AllowClobber

如需有關如何使用 商務用 Skype Online 建立遠端 PowerShell 工作階段的詳細資訊，請參閱 [使用 Windows PowerShell 連線至 Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)。

如需有關使用 商務用 Skype Online PowerShell 模組的詳細資訊，請參閱 [使用 Windows PowerShell 管理 Lync Online](skype-for-business-online-using-windows-powershell-to-manage-your-tenant.md)。

## 請參閱

#### 其他資源

[New-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostingProvider)


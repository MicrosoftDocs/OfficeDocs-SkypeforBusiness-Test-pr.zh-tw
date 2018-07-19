---
title: 開始將使用者從 Lync Online 移轉至 Lync 內部部署之前的首要步驟
TOCTitle: 開始將使用者從 Lync Online 移轉至 Lync 內部部署之前的首要步驟
ms:assetid: 98245b04-ded4-4186-8da3-ba1c554b5c39
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn689118(v=OCS.15)
ms:contentKeyID: 62247315
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 開始將使用者從 Lync Online 移轉至 Lync 內部部署之前的首要步驟

 

_**上次修改主題的時間：** 2014-05-08_

在您開始將 Lync Online 使用者移至內部部署環境前，請檢查下列所有事項：

  - 您的 Lync Server 內部部署環境必須完整部署與驗證。如需詳細資訊，請參閱[部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)。

  - 您必須設定您的 Lync Online 租用戶以供遠端 PowerShell 存取。
    
    若要執行此操作，請先針對 Windows PowerShell 安裝 商務用 Skype Online 模組 (可從下列位置取得：[http://go.microsoft.com/fwlink/p/?LinkId=391911](http://go.microsoft.com/fwlink/p/?linkid=391911))。
    
    安裝模組後，您可以在 Lync Server 管理命令介面中輸入下列 Cmdlet 以建立遠端工作階段：
    
        Import-Module LyncOnlineConnector
    
        $cred = Get-Credential
    
        $CSSession = New-CsOnlineSession -Credential $cred
    
        Import-PSSession $CSSession -AllowClobber
    
    如需有關如何使用 商務用 Skype Online 建立遠端 PowerShell 工作階段的詳細資訊，請參閱[使用 Windows PowerShell 連線至 Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)。
    
    如需有關使用 商務用 Skype Online PowerShell 模組的詳細資訊，請參閱[使用 Windows PowerShell 管理 Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)。

  - 您必須針對共用 SIP 位址空間設定您的 Lync Online。若要執行此操作，首先啟動 Lync Online 與遠端 Powershell 工作階段，然後執行下列 Cmdlet：
    
        Set-CsTenantFederationConfiguration -SharedSipAddressSpace $True

在您完成這些步驟後，您可以繼續[將 Lync Online 使用者移轉至 Lync 內部部署](lync-server-2013-migrating-lync-online-users-to-lync-on-premises.md)。


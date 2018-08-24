---
title: 使用使用者身分識別的 Cmdlet
TOCTitle: 使用使用者身分識別的 Cmdlet
ms:assetid: be87409f-6372-4c70-91ac-6ef13dfbe65a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362842(v=OCS.15)
ms:contentKeyID: 56269149
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用使用者身分識別的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

在 商務用 Skype Online 中，有幾個方法可以參照個別使用者的身分識別：

  - 採用使用者的 Active Directory 網域服務顯示名稱，例如：
    
        -Identity "Ken Myer"

  - 採用使用者的 SIP 位址，例如：
    
        -Identity "sip:kenmyer@litwareinc.com"

  - 採用使用者的 UPN，例如：
    
        -Identity " kenmyer@litwareinc.com"

  - 採用使用者的 Active Directory 網域服務辨別名稱，例如：
    
        -Identity "CN=48ebd1ba-95d4-460c-b751-811ebf0c4611,OU=fa8226f5-14fa-46da-8 236-039b25bc7a27,OU=Lync Online Tenants,DC=litwareinc,DC=com"

下列 Cmdlet 接受使用者的身分識別：

  - [Disable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Disable-CsMeetingRoom)

  - [Enable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Enable-CsMeetingRoom)

  - [Get-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExUmContact)

  - [Get-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingRoom)

  - [Get-CsOnlineUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsOnlineUser?view=skype-ps)

  - [Get-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUserAcp)

  - [New-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsExUmContact)

  - [Remove-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsExUmContact)

  - [Remove-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsUserAcp)

  - [Set-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExUmContact)

  - [Set-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMeetingRoom)

  - [Set-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUserAcp)

請注意，您無需在呼叫 **Get-Cs** Cmdlet 時指定使用者的身分識別。在此情況下，Cmdlet 會傳回指定項目的所有執行個體。例如，下列命令會傳回已啟用 商務用 Skype Online 之所有使用者的相關資訊：

    Get-CsOnlineUser

只有在您需要傳回特定使用者的相關資訊時，才需要加上 Identity 參數：

    Get-CsOnlineUser -Identity "Ken Myer"

## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)


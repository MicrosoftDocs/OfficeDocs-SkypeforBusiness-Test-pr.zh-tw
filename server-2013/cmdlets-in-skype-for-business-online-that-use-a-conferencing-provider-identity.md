---
title: 使用會議提供者身分識別的 Cmdlet
TOCTitle: 使用會議提供者身分識別的 Cmdlet
ms:assetid: be5621b6-ec11-4b12-83ec-075af269ca6a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362841(v=OCS.15)
ms:contentKeyID: 56269148
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用會議提供者身分識別的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

若要傳回您的組織已與之訂立契約之所有音訊會議提供者的相關資訊，您可以直接呼叫 [Get-CsAudioConferencingProvider](https://docs.microsoft.com/powershell/module/skype/Get-CsAudioConferencingProvider) Cmdlet 而不加入任何參數：

    Get-CsAudioConferencingProvider

若要將傳回資料限制為單一提供者 (在此範例中，該提供者為 Contoso Audio Services)，請使用 Identity 參數：

    Get-CsAudioConferencingProvider -Identity "Contoso Audio Services"

僅有一個 商務用 Skype Online Cmdlet 接受音訊會議提供者識別碼：

  - [Get-CsAudioConferencingProvider](https://docs.microsoft.com/powershell/module/skype/Get-CsAudioConferencingProvider)

## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)


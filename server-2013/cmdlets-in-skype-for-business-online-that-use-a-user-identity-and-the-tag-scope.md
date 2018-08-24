---
title: 使用使用者身分識別與標記範圍的 Cmdlet
TOCTitle: 使用使用者身分識別與標記範圍的 Cmdlet
ms:assetid: 344a21b0-5301-4e77-853a-970bb1c11e1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362781(v=OCS.15)
ms:contentKeyID: 56269078
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用使用者身分識別與標記範圍的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

**Grant-Cs** Cmdlet (用於將原則指派給使用者) 需要兩個識別碼：使用者身分識別 (Identity 參數) 與個別使用者原則的身分識別 (PolicyName 參數)。例如，若要將語音原則 RedmondVoicePolicy 指派給使用者 Ken Myer，請使用下列命令：

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

將原則指派給使用者時，有兩項要點需要注意：首先，您僅能夠指派個別使用者原則。您無法將全域原則指派給使用者。例如，下列命令將會失敗：

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "global"

此命令失敗的原因在於全域原則無需指派。若要使用全域原則管理使用者，只要確定並未將個別使用者原則指派給該使用者即可。若未將任何個別使用者原則指派給使用者，系統將自動使用全域原則管理該使用者。

> [!NOTE]
> 若是使用者先前已有指派個別使用者原則，而要取消指派該原則並改為以全域原則管理該使用者時，該如何處理呢？在此情況下，首先必須使用下列語法，授予 Null 原則給該使用者，以取消指派個別使用者原則：<br />
> Grant-CsVoicePolicy –Identity &quot;Ken Myer&quot; –PolicyName $Null


再者，請記住個別使用者原則是建立於標記範圍。然而，指定原則名稱時可忽略前置詞 tag。以下兩個命令作用相同：

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "tag:RedmondVoicePolicy"
    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

若要傳回所有個別使用者原則的識別碼 (或者，至少傳回指定類型的所有個別使用者原則，例如語音原則)，請使用類似下列的命令：

    Get-CsVoicePolicy -Filter "tag:*"

下列 Cmdlet 同時使用使用者身分識別與標記範圍：

  - [Grant-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsClientPolicy)

  - [Grant-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsConferencingPolicy)

  - [Grant-CsDialPlan](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsDialPlan)

  - [Grant-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsExternalAccessPolicy)

  - [Grant-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsHostedVoicemailPolicy)

  - [Grant-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsVoicePolicy)

## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)


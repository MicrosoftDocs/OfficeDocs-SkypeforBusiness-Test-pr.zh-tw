---
title: 指派個別使用者原則給使用者
TOCTitle: 指派個別使用者原則給使用者
ms:assetid: 37e07da7-6391-4d6d-a428-c70272897039
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362779(v=OCS.15)
ms:contentKeyID: 56269076
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派個別使用者原則給使用者

 

_**上次修改主題的時間：** 2015-06-22_

若要將個別使用者原則指派給使用者，首先必須選擇適當的 **Grant-Cs** Cmdlet (例如，若要指派個別使用者語音原則，必須使用 [Grant-CsVoicePolicy](grant-csvoicepolicy.md))，然後執行 Cmdlet，並確定指定要指派原則的使用者身分識別及指派的原則名稱：

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

若要將相同的原則指派給所有使用者，請使用下列語法：

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName "RedmondVoicePolicy"

請注意，因為授權合約與國家/地區限制有所不同，所以特定會議原則、外部存取原則或行動原則可能無法指派給特定使用者。若要確認個別使用者原則是否真能指派給特定使用者 (例如 kenmyer@litwareinc.com)，請視需要使用下列其中一項命令 (與 ApplicableTo 參數)：

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

上述語法僅會傳回真的能指派給 Ken Myer 的個別使用者原則。

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


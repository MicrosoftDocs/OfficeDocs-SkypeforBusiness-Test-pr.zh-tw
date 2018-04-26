---
title: 傳回個別使用者原則清單
TOCTitle: 傳回個別使用者原則清單
ms:assetid: e95a2755-3501-40cc-a704-5ecd01839d76
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362856(v=OCS.15)
ms:contentKeyID: 56269167
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回個別使用者原則清單

 

_**上次修改主題的時間：** 2015-06-22_

若要傳回可用的個別使用者原則清單，首先選擇適當的 **Get-Cs** Cmdlet (例如，若要傳回個別使用者語音原則，請使用 [Get-CsVoicePolicy](get-csvoicepolicy.md) Cmdlet)。接著，使用下列語法傳回各個個別使用者原則的身分識別：

    Get-CsVoicePolicy -Filter "tag:*" | Select-Object Identity

請注意，因為授權合約與國家/地區限制有所不同，所以特定會議原則、外部存取原則或行動原則可能無法指派給指定使用者。若要確認個別使用者原則是否可實際指派給指定使用者 (例如 kenmyer@litwareinc.com)，請視需要使用下列其中一項命令 (與 ApplicableTo 參數)：

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

上述語法僅會傳回可實際指派給 Ken Myer 的個別使用者原則。

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


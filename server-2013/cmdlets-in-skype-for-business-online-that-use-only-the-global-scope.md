---
title: 僅使用全域範圍的 Cmdlet
TOCTitle: 僅使用全域範圍的 Cmdlet
ms:assetid: 0ffd3bc9-a6a1-4c2e-8d52-e599acc49d2d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362771(v=OCS.15)
ms:contentKeyID: 56269063
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 僅使用全域範圍的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

部分 商務用 Skype Online 設定僅提供於「全域範圍」。這表示有單一設定集合會套用至指派給該租用戶的所有使用者 (各個租用戶均有其專屬的全域設定集合)。使用限制為全域範圍的 Cmdlet 時，Identity 參數為選用項目。舉例來說，若要擷取會議組態設定，您可以使用下列命令：

    Get-CsMeetingConfiguration -Identity "global"

或者，您亦可忽略 Identity 參數並改為下列較為簡單的命令：

    Get-CsMeetingConfiguration

由於會議組態設定僅有全域集合，因此兩個命令會傳回完全相同的資訊。此外，使用任一個 **Set-Cs** Cmdlet 時均可忽略 Identity 參數。下列兩個命令完全相同：

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False
    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

這兩個命令完全相同的原因在於，根據預設，如未包含 Identity 參數，則 Windows PowerShell 會修改全域集合。

下列 Cmdlet 僅會在全域範圍中運作：

  - [Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

  - [Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)

  - [Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)

  - [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

  - [Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

  - [Get-CsTenantLicensingConfiguration](get-cstenantlicensingconfiguration.md)

  - [Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

  - [Remove-CsVoicePolicy](remove-csvoicepolicy.md)

  - [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

  - [Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

請注意，**Remove-CsVoicePolicy** Cmdlet 的狀況較為特殊。首先，此 Cmdlet 並不會要求您包含 Identity 參數。

    Remove-CsVoicePolicy -Identity "global"

再者，**Remove-CsVoicePolicy** Cmdlet 並不會實際刪除全域語音原則；商務用 Skype Online 並不允許您刪除全域原則或組態設定。此 Cmdlet 的作用在於讓您將全域語音原則中的所有屬性重新設為預設值。例如，根據預設，AllowCallForwarding 屬性設為 False。然而，AllowCallForwarding 可能經過修改，屬性值現在設為 True。執行 **Remove-CsVoicePolicy** Cmdlet 後，AllowCallForwarding 屬性將會還原為預設值：False。下表摘要說明此案例：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>AllowCallForwarding 值</th>
<th>案例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>False</p></td>
<td><p>預設值</p></td>
</tr>
<tr class="even">
<td><p>True</p></td>
<td><p>全域原則經過修改後</p></td>
</tr>
<tr class="odd">
<td><p>False</p></td>
<td><p>執行 <strong>Remove-CsVoicePolicy</strong> Cmdlet 後</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)


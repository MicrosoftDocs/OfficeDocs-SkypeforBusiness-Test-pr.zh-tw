---
title: 使用全域範圍與標記範圍的 Cmdlet
TOCTitle: 使用全域範圍與標記範圍的 Cmdlet
ms:assetid: 1e2bc055-8a72-425e-967b-e253add7018c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362774(v=OCS.15)
ms:contentKeyID: 56269072
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用全域範圍與標記範圍的 Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

在 商務用 Skype Online 中，可於「全域範圍」或「標記範圍」 (又稱「個別使用者範圍」) 中設定原則。使用 **Get-Cs** Cmdlet 時，您無需指定範圍或身分識別。若是呼叫其中一個 Cmdlet 而不加入任何參數，則會傳回所有相關項目。例如，下列命令會傳回您的所有外部存取原則的相關資訊：

    Get-CsExternalAccessPolicy

若要限制傳回的資料，您必須僅包含 Identity 參數或 Filter 參數。例如，若是僅要傳回全域原則，請使用下列命令：

    Get-CsExternalAccessPolicy -Identity "global"

若要傳回 Identity 為 “RedmondAccessPolicy” 的個別使用者原則，請使用下列命令：

    Get-CsExternalAccessPolicy -Identity "RedmondAccessPolicy"

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>參照個別使用者原則時，可選擇性加入前置詞 <strong>tag</strong>。語法包含前置詞後同樣有效：<br />
Get-CsExternalAccessPolicy –Identity &quot;tag:RedmondAccessPolicy&quot;</td>
</tr>
</tbody>
</table>


若要傳回全域原則以外的所有原則 (即所有個別使用者原則)，請使用下列命令：

    Get-CsExternalAccessPolicy -Filter "tag:*"

下列 Cmdlet 可在全域範圍與個別使用者 (tag) 範圍中運作：

  - [Get-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClientPolicy)

  - [Get-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsConferencingPolicy)

  - [Get-CsDialPlan](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsDialPlan)

  - [Get-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExternalAccessPolicy)

  - [Get-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostedVoicemailPolicy)

  - [Get-CsPresencePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsPresencePolicy)

  - [Get-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsVoicePolicy)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然名稱為撥號對應表，但就功能而言，撥號對應表實屬原則。之所以採用「撥號對應表」而非撥號原則之類的詞彙，是為了要保留先前版本的 Lync Server 所採用的術語。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[身分識別、範圍，以及租用戶](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)


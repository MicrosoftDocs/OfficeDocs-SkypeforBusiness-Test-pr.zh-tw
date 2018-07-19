---
title: 身分識別、範圍，以及租用戶
TOCTitle: 身分識別、範圍，以及租用戶
ms:assetid: 7cfa194a-2d01-4370-9b48-ee13ff597fa5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362819(v=OCS.15)
ms:contentKeyID: 56269122
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 身分識別、範圍，以及租用戶

 

_**上次修改主題的時間：** 2015-06-22_

許多用於管理 商務用 Skype Online 的 Windows PowerShell Cmdlet 會要求您明確指出所要管理的項目。例如，執行 [Set-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUserAcp) Cmdlet 時，您必須表明所要管理的使用者。其中的道理在於，除非您明確告知該 Cmdlet 所要管理的使用者帳戶為何，否則 **Set-CsUserAcp** Cmdlet 將不清楚應修改哪位使用者的音訊會議資訊。基於此因素，每當執行 **Set-CsUserAcp** Cmdlet 時，您將需要加上 Identity 參數，並且後接所要修改之使用者帳戶的身分識別：

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP"

若是「身分識別」一詞僅是指使用者帳戶的身分識別，應該就不會造成混淆：當處理的是人員 (使用者或連絡人等) 時，身分識別即為使用者個人。然而，使用者帳戶以外的項目亦有身分識別：當處理的是 商務用 Skype Online 服務的元件 (原則或組態設定等)，「身分識別」一詞的意義就會有些許差異。例如，請參閱下列命令：

    Get-CsMeetingConfiguration -Identity "global"

在此案例中，身分識別為 "global" 指的是會議組態設定的範圍。「範圍」是 商務用 Skype Online (與 Lync Server) 中用於指定管理範圍的詞彙。根據預設，原則與設定均有全域範圍。在初次設定您的 商務用 Skype Online 帳戶時，預設將有一套全域原則與設定：全域會議組態設定、全域外部存取原則，以及全域撥號對應表等。

在 Microsoft Lync Server 2010 中引入這些全域原則與設定，有助確保所有使用者與所有元件均可獲得某種形式的管理。這在 Microsoft Office Communicator 2007 R2 中並非一定。根據您存取系統的方式，可能最後大部分項目為未受管理的狀態 (通常是因為群組原則無法套用至您的使用者帳戶)。相對之下，在 Lync Server 與 商務用 Skype Online 中，所有項目均受到管理。這是因為無論取代為其他何種項目，將一律執行全域原則與設定。

為何要說「無論取代為其他何種項目」？在 商務用 Skype Online 的案例中，可以建立「標記範圍」或管理範圍的原則。建立於標記範圍 (亦稱為「個別使用者範圍」) 的原則會優先於建立於全域範圍的原則。換句話說，個別使用者原則將一律優先於全域原則。例如，您可能有兩個外部使用者存取原則。全域原則會禁止使用者與具有公用立即訊息 (IM) 提供者帳戶的人員進行通訊，例如 Windows Live。個別使用者原則 AllowPublicIMCommunication 則允許與公用 IM 提供者進行通訊。

您可能亦有兩名使用者：Ken Myer 與 Pilar Ackerman。Ken Myer 已指派有個別使用者原則。Pilar Ackerman 則未指派個別使用者原則；也就是說，她受全域外部存取原則管理。下表顯示哪個使用者 (如有的話) 可與公用 IM 提供者進行通訊：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>原則設定</th>
<th>Ken Myer</th>
<th>Pilar Ackerman</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>公用 IM 提供者的全域原則設定</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>公用 IM 提供者的個別使用者原則設定</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>使用者可與公用 IM 提供者進行通訊</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


如您所見，Ken Myer 可與公用 IM 提供者進行通訊，因為指派給他的個別使用者原則中的設定會覆寫全域原則中的設定。Pilar Ackerman 無法與公用 IM 提供者進行通訊，因為她受全域原則管理，而全域原則禁止該類通訊。

個別使用者原則必須由 Office 365 支援人員為您建立。在原則建立後，您可以使用適當的 **Grant-Cs** Cmdlet (例如 [Grant-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsExternalAccessPolicy)) 將原則指派給使用者。個別使用者原則相當容易識別，因為原則 Identity 一律會以 tag 前置詞作為開頭。例如：

    Identity : tag:AllowPublicIMCommunication

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tag 前置詞可追溯至 Lync Server 2010 的初期部署階段。當時，個別使用者原則稱為「標記原則」並可由 tag 前置詞 加以識別。這些原則現已更為精確地改稱為「個別使用者原則」，而標記範圍則更為精確地改稱為「個別使用者範圍」。然而，基於技術因素，tag 前置詞的用法從未變更。</td>
</tr>
</tbody>
</table>


另一個在使用 商務用 Skype Online 與 Windows PowerShell 時所會看到的詞彙是「租用戶」。當您設定 商務用 Skype Online 帳戶時，系統會將租用戶識別碼指派給您的新部署，該識別碼即為類似如下的全域唯一識別碼 (GUID)：

    bf19b7db-6960-41e5-a139-2aa373474354

有幾個 商務用 Skype Online Cmdlet 要求您在執行 Cmdlet 時輸入租用戶識別碼。即使您已登入且僅有一個租用戶，您還是必須輸入該租用戶識別碼。所幸您無需記憶該租用戶識別碼；您可以隨時執行下列 Windows PowerShell 命令以擷取您的租用戶識別碼：

    Get-CsTenant | Select-Object TenantId

當然，瞭解全域範圍與個別使用者範圍 (或標記範圍) 之間的差異等資訊僅是成功的一半。另外您還必須瞭解何時可以 (或能夠) 使用這些範圍。身分識別與租用戶參數也是如此。下列主題說明不同的 商務用 Skype Online Cmdlet 是如何使用身分識別、範圍以及租用戶參數。

  - [僅使用全域範圍的 Cmdlet](cmdlets-in-skype-for-business-online-that-use-only-the-global-scope.md)

  - [使用全域範圍與標記範圍的 Cmdlet](cmdlets-in-skype-for-business-online-that-use-the-global-scope-and-the-tag-scope.md)

  - [使用使用者身分識別的 Cmdlet](cmdlets-in-skype-for-business-online-that-use-a-user-identity.md)

  - [使用使用者身分識別與標記範圍的 Cmdlet](cmdlets-in-skype-for-business-online-that-use-a-user-identity-and-the-tag-scope.md)

  - [使用 Tenant 參數的 Cmdlet](cmdlets-in-skype-for-business-online-that-use-the-tenant-parameter.md)

  - [使用會議提供者身分識別的 Cmdlet](cmdlets-in-skype-for-business-online-that-use-a-conferencing-provider-identity.md)

  - [不使用範圍或身分識別的 Cmdlet](cmdlets-in-skype-for-business-online-that-do-not-use-a-scope-or-an-identity.md)


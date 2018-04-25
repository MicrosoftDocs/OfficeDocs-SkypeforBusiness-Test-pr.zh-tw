---
title: Set-CsArchivingPolicy
TOCTitle: Set-CsArchivingPolicy
ms:assetid: 2213f1e7-ebdb-4a70-83d9-41eee6d0e14f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398294(v=OCS.15)
ms:contentKeyID: 49290329
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的立即訊息 (IM) 封存原則。封存原則可讓您封存所有內部使用者之間所發生的 IM 工作階段及會議。除此之外還可以封存內部使用者與同盟協力廠商之間所執行的工作階段。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsArchivingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsArchivingPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ArchiveExternal <$true | $false>] [-ArchiveInternal <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在此範例中， **Set-CsArchivingPolicy** Cmdlet 可用來修改全域封存原則。在此情況下，ArchiveInternal 屬性是設為 True。

    Set-CsArchivingPolicy -Identity global -ArchiveInternal $True

## 範例 2

範例 2 是範例 1 所示命令的變化。但是，這時組織中所有的封存原則都設為允許封存 IM 工作階段。為達成此目的，命令會先使用 **Get-CsArchivingPolicy** Cmdlet 傳回目前所使用之所有 IM 工作階段封存原則的集合。然後，此集合會管線傳送到 **Set-CsArchivingPolicy** Cmdlet，將每個原則的 ArchiveInternal 屬性設為 True。

    Get-CsArchivingPolicy | Set-CsArchivingPolicy -ArchiveInternal $True

## 詳細描述

許多組織發現保留使用者參與的所有 IM 工作階段封存很有幫助。其他組織則依法需保留這樣的封存。您必須執行兩項步驟，才能使用 Lync Server 封存 IM 工作階段。首先，您必須使用 **Set-CsArchivingConfiguration** Cmdlet，在全域範圍和/或網站範圍啟用封存。這讓您可以封存 IM 工作階段；不過，它不會自動開始封存那些工作階段。

若要實際儲存 IM 工作階段的文字記錄，您必須完成步驟 2：建立一或多個封存原則。這些原則會決定哪些使用者要記錄其 IM 工作階段，以及要封存哪些類型的 IM 工作階段 (內部和/或外部)。內部 IM 工作階段是工作階段中，所有參與者都是擁有組織中 Active Directory 帳戶的已驗證使用者；外部 IM 工作階段是工作階段中，至少有一個參與者是沒有組織中 Active Directory 帳戶的未驗證使用者。您可以選擇只封存內部工作階段、只封存外部工作階段，或是同時封存內部和外部工作階段。

可將封存原則 (使用 **New-CsArchivingPolicy** Cmdlet 建立) 指派至全域網站或網站範圍。此外，可將這些原則指派給每個使用者範圍；這表示可先建立原則，然後將原則套用到特定使用者或一群使用者。例如，您可以擁有為全部使用者封存內部 IM 工作階段的全域原則。此外，您可以建立同時封存內部和外部工作階段的次要原則；然後只將次要原則套用到您自己的銷售人員。因為每個使用者原則優先於全域和網站原則，所以銷售人員的成員可以封存全部的 IM 工作階段。其他使用者 (也就是不在銷售部門且不受銷售原則影響的使用者) 就只會封存其內部 IM 工作階段。

**Set-CsArchivingPolicy** Cmdlet 可讓您修改組織目前所使用之任何 IM 工作階段封存原則的屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsArchivingPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingPolicy"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ArchiveExternal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否封存外部 IM 工作階段(外部 IM 工作階段至少有一位參與者是未經過驗證的使用者，他們在組織內沒有 Active Directory 帳戶)。預設值為 False，表示不封存包含外部使用者的 IM 工作階段。</p></td>
</tr>
<tr class="even">
<td><p><em>ArchiveInternal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否封存內部 IM 工作階段(內部 IM 工作階段的所有參與者都是經過驗證的使用者，他們在組織內擁有 Active Directory 帳戶)。預設值為 False，表示不封存內部 IM 工作階段。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供關於原則的其他文字。例如，可使用 Description 屬性詳細說明原則應套用到哪些使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之封存原則的唯一識別碼。可將封存原則設定在全域、網站或每個使用者範圍。若要修改全域原則，請使用下列語法：-Identity global。若要修改網站原則，請使用類似下列的語法：-Identity site:Redmond。若要修改每個使用者原則，請使用類似下列的語法：-Identity SalesArchivingPolicy。若未指定此參數，會修改全域原則。</p>
<p>指定 Identity 時不允許使用萬元字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>IMArchivingPolicy 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy 物件。 **Remove-CsArchivingPolicy** Cmdlet 接受管線傳送的封存原則物件輸入。

## 傳回類型

**Set-CsArchivingPolicy** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Policy.IM.IMArchivingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)


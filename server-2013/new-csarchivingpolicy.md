---
title: New-CsArchivingPolicy
TOCTitle: New-CsArchivingPolicy
ms:assetid: e7c9b310-fbd0-4793-90ef-c752b941e02f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399032(v=OCS.15)
ms:contentKeyID: 49292655
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsArchivingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的立即訊息 (IM) 工作階段封存原則。這些原則可讓您封存內部使用者之間及/或封存內部使用者與外部協力廠商之間所發生的所有 IM 工作階段。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsArchivingPolicy -Identity <XdsIdentity> [-ArchiveExternal <$true | $false>] [-ArchiveInternal <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **New-CsArchivingPolicy** Cmdlet，來建立 Identity 為 site:Redmond 的新封存原則。此外，還會將 ArchiveInternal 參數設為 True；這表示此新原則將啟用內部 IM 工作階段與會議的封存。

    New-CsArchivingPolicy -Identity site:Redmond -ArchiveInternal $True

## 範例 2

範例 2 會使用 InMemory 參數，來建立最初只存在於記憶體的封存原則。在此命令集中，會先呼叫 **New-CsArchivingPolicy** Cmdlet 搭配 InMemory 參數，以建立 Identity 為 site:Redmond 的新網站原則。這個只存在記憶體中的新原則會儲存於變數 $x 中。在命令 2 與 3 中，會修改此虛擬原則的屬性值；在命令 2 中，會將 ArchiveInternal 屬性值設為 True，而在命令 3 中，會將 ArchiveExternal 屬性設為 True。

最後，範例中的最後一個命令會使用 **Set-CsArchivingPolicy** Cmdlet，將虛擬原則 site:Redmond 轉換為實際的 IM 工作階段封存原則。

    $x = New-CsArchivingPolicy -Identity site:Redmond -InMemory
    $x.ArchiveInternal = $True
    $x.ArchiveExternal = $True
    Set-CsArchivingPolicy -Instance $x

## 詳細描述

許多組織發現保留使用者參與的所有 IM 工作階段封存很有幫助；其他組織則依法必須保留這樣的封存。您必須執行兩項步驟，才能使用 Lync Server 封存 IM 工作階段。首先，您必須使用 **Set-CsArchivingConfiguration** Cmdlet 來啟用全域和/或網站範圍的封存。這讓您可以封存 IM 工作階段；不過，它不會自動開始封存那些工作階段。

若要確實儲存您的 IM 工作階段的記錄，您必須完成步驟 2：建立一或多個 IM 工作階段封存原則，決定將記錄其 IM 工作階段的使用者，及將封存之 IM 工作階段的類型 (內部和/或外部)。內部 IM 工作階段的所有參與者都是經過驗證的使用者，他們在組織內擁有 Active Directory 帳戶；外部 IM 工作階段至少有一位參與者是未經過驗證的使用者，他們在組織內沒有 Active Directory 帳戶。您可以選擇只封存內部工作階段、只封存外部工作階段，或內部和外部工作階段都封存。

封存原則可以指派給全域範圍或網站範圍。此外，這些原則還可以指派給個別使用者範圍，然後套用至特定使用者或特定一組使用者。例如，假設您的全域原則只會封存所有使用者的內部 IM 工作階段。在此情況下，您可以建立同時封存內部和外部工作階段的次要原則，然後只將該原則套用到您自己的銷售人員。因為每個使用者原則優先於全域和網站原則，所以銷售人員的成員可以封存全部的 IM 工作階段。其他使用者 (不在銷售部門且不受銷售原則影響的使用者) 就只會封存其內部 IM 工作階段。

您可使用 **New-CsArchivingPolicy** Cmdlet 建立新的封存原則 (在網站或個別使用者範圍)。如果您在網站範圍建立原則，它會在建立原則的同時自動套用至網站。如果您在個別使用者範圍建立原則，則在您呼叫 **Grant-CsArchivingPolicy** Cmdlet 以明確地將其指派給某位使用者或使用者集之前，不會使用該原則。您無法在全域範圍建立新原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsArchivingPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsArchivingPolicy"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要指派給原則的唯一 Identity。可在網站範圍或個別使用者範圍建立新的封存原則。若要建立新的網站原則，請使用首碼 &quot;site:&quot;，後面再加上網站的名稱。例如，這個語法會為 Redmond 網站建立新原則：-Identity site:Redmond。若要建立新的個別使用者原則，請使用如下的 Identity：-Identity SalesArchivingPolicy。</p>
<p>請注意，您無法建立新的全域原則；如果您要對全域原則進行變更，請改用 <strong>Set-CsArchivingPolicy</strong> Cmdlet。同樣的，如果使用該 Identity 的原則已存在，您便無法建立新的網站原則或個別使用者原則。</p></td>
</tr>
<tr class="even">
<td><p><em>ArchiveExternal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否封存外部 IM 工作階段(外部 IM 工作階段至少有一位參與者是未經過驗證的使用者，他們在組織內沒有 Active Directory 帳戶)。預設值為 False，表示不封存包含外部使用者的 IM 工作階段。</p></td>
</tr>
<tr class="odd">
<td><p><em>ArchiveInternal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否封存內部 IM 工作階段(內部 IM 工作階段的所有參與者都是經過驗證的使用者，他們在組織內擁有 Active Directory 帳戶)。預設值為 False，表示不封存內部 IM 工作階段。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>啟用系統管理員提供封存原則的簡短說明。例如，Description 可用來說明應套用原則的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsArchivingPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsArchivingPolicy** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)


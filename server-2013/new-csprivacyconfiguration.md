---
title: New-CsPrivacyConfiguration
TOCTitle: New-CsPrivacyConfiguration
ms:assetid: 9b7f02d7-93a5-4fa5-a74c-3fe4baf8bbfc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398807(v=OCS.15)
ms:contentKeyID: 49291797
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPrivacyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的隱私權組態設定集合。隱私權組態設定可指定使用者所能使用的資訊量。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsPrivacyConfiguration -Identity <XdsIdentity> [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立將套用至 Redmond 網站 (-Identity site:Redmond) 的新私密性組態設定集合。新的設定會啟用隱私權模式；這可以透過加入 EnablePrivacyMode 參數，並將參數值設為 True 完成。請注意，如果 Redmond 網站已有隱私權設定集合，則此命令將會失敗。

    New-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $True

## 範例 2

範例 2 示範如何使用 InMemory 參數建立一開始僅存在於記憶體中的新隱私權組態設定集合。為達成此目的，會呼叫 **New-CsPrivacyConfiguration** Cmdlet 並搭配 Identity 和 InMemory 參數；產生的物件會儲存在名為 $x 的變數中。隱私權設定此時只存在於記憶體中；如果您執行 **Get-CsPrivacyConfiguration** Cmdlet，將不會看到 site:Redmond 列於清單中。

在第二個命令中，EnablePrivacyMode 屬性的值會設為 True。最後，第三個命令會使用 **Set-CsPrivacyConfiguration** Cmdlet，將虛擬隱私權設定集合轉換為套用到 Redmond 網站的實際設定集合。呼叫 **Set-CsPrivacyConfiguration** Cmdlet 是最關鍵的部分：如果無法呼叫此 Cmdlet，則您的新隱私權設定將不會套用到 Redmond 網站，而且會在您終止 Windows PowerShell 工作階段或刪除變數 $x 時消失。

    $x = New-CsPrivacyConfiguration -Identity site:Redmond -InMemory
    $x.EnablePrivacyMode = $True
    Set-CsPrivacyConfiguration -Instance $x

## 詳細描述

Lync Server 可以提供使用者與其他人共用大量目前狀態資訊的機會：他們可以發佈自己的照片、提供詳細的位置資訊，並將自己的目前狀態資訊自動提供給組織內的每一個人 (而不是只將此資訊提供給其連絡人清單上的人)。

有些使用者會很高興能夠有將此資訊提供給同事的機會；有些使用者可能會不願意共用此資料 (例如，許多人可能會對於在目前狀態資料中加入相片還有些遲疑)。一般而言，使用者可控制是否分享哪些資訊，例如使用者可勾選或取消勾選核取方塊，來控制是否要與他人分享其位置資訊。此外，隱私權組態 Cmdlet 可讓系統管理員管理使用者的隱私權設定。在某些情況下，系統管理員可以啟用或停用設定；例如，如果 AutoInitiateContacts 屬性設為 True，則會將小組成員自動新增至每位使用者的連絡人清單中；如果設為 False，則不會將小組成員自動新增至每位使用者的連絡人清單中。

在其他狀況下，系統管理員可在 Lync 中設定預設值，同時仍讓使用者有權利變更這些值。例如，預設會發佈使用者的位置資訊，但是使用者擁有停止位置發佈的權限。透過將 PublishLocationDataByDefault 屬性設為 False，系統管理員可以變更此行為：在該情況下，預設將不會發佈位置資料，但是如果使用者選擇這麼做，仍然擁有發佈此資料的權限。

私密性組態設定可以在全域範圍、網站範圍及服務範圍 (儘管只針對 User Server 服務) 套用。**New-CsPrivacyConfiguration** Cmdlet 可讓您建立套用至網站或服務的新私密性組態設定。(您無法在全域範圍建立新集合)。請注意，每個個別網站或服務最多只能有一個單一的私密性組態設定集合：如果您嘗試建立 Redmond 網站的新集合，而且該網站已經有隱私權設定的集合，則您的命令將會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsPrivacyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPrivacyConfiguration"}

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
<td><p>要建立之私密性組態設定的唯一識別碼。若要在網站範圍建立設定的新集合，請使用類似下列的語法：-Identity site:Redmond。若要在服務範圍建立新的設定，請使用類似下列的語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。您只可以建立 User Server 服務的隱私權設定。如果您嘗試將這些設定套用至其他任何服務，將會發生錯誤。</p>
<p>請注意，如果指定的網站或服務已有私密性組態設定，則您的命令將會失敗。同樣地，如果您嘗試建立全域設定的新集合，命令也會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，Lync 會自動將您的經理和直屬員工新增至連絡人清單。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則會自動在 Lync 中發佈使用者的相片。若為 False，除非使用者明確選取 [讓其他人看到我的相片] 選項，否則將無法使用使用者的相片。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果為 True，可以提供使用者啟用進階隱私權模式的機會。在進階隱私權模式中，只允許您連絡人清單上的人員檢視您的目前狀態資訊。若為 False，則您的目前狀態資訊會提供給組織中的任何人。預設值為 False。</p></td>
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
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則會自動在 Lync 中發佈位置資料。若為 False，除非使用者明確選取 [向連絡人顯示我的位置] 選項，否則將無法使用位置資料。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新隱私權組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令，為每個租用戶傳回租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

無。**New-CsPrivacyConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPrivacyConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)


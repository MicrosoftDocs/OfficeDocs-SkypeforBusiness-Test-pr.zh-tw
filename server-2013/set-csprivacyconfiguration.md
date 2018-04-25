---
title: Set-CsPrivacyConfiguration
TOCTitle: Set-CsPrivacyConfiguration
ms:assetid: 67fbd99a-0708-4e6f-8755-cb1a08d07ff3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398484(v=OCS.15)
ms:contentKeyID: 49291184
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPrivacyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的隱私權組態設定集合。隱私權組態設定可指定使用者提供給其他使用者的資訊量。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsPrivacyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPrivacyConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 site:Redmond 之私密性組態設定的三個屬性值。修改的三個屬性值為 AutoInitiateContacts、PublishLocationDataDefault 以及 DisplayPublishedPhotoDefault。

    Set-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $False -AutoInitiateContacts $True -PublishLocationDataDefault $True -DisplayPublishedPhotoDefault $True

## 範例 2

範例 2 可為組織中目前使用的所有隱私權組態設定啟用隱私權模式。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPrivacyConfiguration** Cmdlet，以傳回隱私權設定的完整集合。然後，此集合會管線傳送到 **Set-CsPrivacyConfiguration** Cmdlet，以將集合中每個項目的 EnablePrivacyMode 屬性設為 True。

    Get-CsPrivacyConfiguration | Set-CsPrivacyConfiguration -EnablePrivacyMode $True

## 範例 3

範例 3 會修改目前未使用隱私權模式的所有隱私權組態設定。為了執行此工作，命令會先使用 **Get-CsPrivacyConfiguration** Cmdlet 傳回所有隱私權組態設定的集合。然後再將該集合管線傳送給 **Where-Object** Cmdlet，這會只選取 EnablePrivacyMode 屬性等於 False 的設定。接著將篩選後的集合管線傳送到 **Set-CsPrivacyConfiguration** Cmdlet，以將值指派給集合中每個項目的 AutoInitiateContacts、PublishLocationDataDefault 及 DisplayPublishedPhotoDefault 屬性。

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Set-CsPrivacyConfiguration -AutoInitiateContacts $True -PublishLocationDataDefault $True -DisplayPublishedPhotoDefault $True

## 詳細描述

Lync Server 可以提供使用者與其他人共用大量目前狀態資訊的機會：他們可以發佈自己的照片、提供詳細的位置資訊，並將自己的目前狀態資訊自動提供給組織內的每一個人 (而不是只將此資訊提供給其連絡人清單上的人)。

有些使用者會很高興能夠有將此資訊提供給同事的機會；有些使用者可能會不願意共用此資料 (例如，許多人可能會對於在目前狀態資料中加入相片還有些遲疑)。一般而言，使用者可控制是否分享哪些資訊，例如使用者可勾選或取消勾選核取方塊，來控制是否要與他人分享其位置資訊。此外，隱私權組態 Cmdlet 可讓系統管理員管理使用者的隱私權設定。在某些情況下，系統管理員可以啟用或停用設定；例如，如果 AutoInitiateContacts 屬性設為 True，則會將小組成員自動新增至每位使用者的連絡人清單中；如果設為 False，則不會將小組成員自動新增至每位使用者的連絡人清單中。

在其他狀況下，系統管理員可在 Lync 中設定預設值，同時仍讓使用者有權利變更這些值。例如，預設會發佈使用者的位置資訊，但是使用者擁有停止位置發行的權限。透過將 PublishLocationDataByDefault 屬性設為 False，系統管理員可以變更此行為：在該情況下，預設將不會發佈位置資料，但是如果使用者選擇這麼做，仍然擁有發佈此資料的權限。

私密性組態設定可以在全域範圍、網站範圍及服務範圍 (儘管只針對 User Server 服務) 套用。**Set-CsPrivacyConfiguration** Cmdlet 可讓您修改組織中目前所使用的任何私密性組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPrivacyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPrivacyConfiguration"}

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
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數若為 True，Lync 會自動將您的主管和直屬員工新增至連絡人清單。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數若為 True，則會自動在 Lync 中發佈使用者的相片。若為 False，除非使用者明確選取 [讓其他人看到我的相片] 選項，否則將無法使用使用者的相片。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果為 True，可以提供使用者啟用進階隱私權模式的機會。在進階隱私權模式中，只允許您連絡人清單上的人員檢視您的目前狀態資訊。若為 False，則您的目前狀態資訊會提供給組織中的任何人。預設值為 False。</p></td>
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
<td><p>要修改之私密性組態設定的唯一識別碼。若要修改全域設定，請使用下列語法：-Identity global。若要修改在網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要修改服務層級的設定，請使用類似下列的語法：-Identity service:Redmond-UserServices-1.。請注意，私密性設定只可套用至 User Server 服務。如果您嘗試將這些設定套用至其他任何服務，將會發生錯誤。</p>
<p>若未指定此參數，則在您呼叫 <strong>Set-CsPrivacyConfiguration</strong> Cmdlet 時，將會更新全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PrivacyConfiguration 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數若為 True，則會自動在 Lync Server 中發佈位置資料。若為 False，除非使用者明確選取 [向連絡人顯示我的位置] 選項，否則將無法使用位置資料。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改之隱私權組態設定的 商務用 Skype Online 租用戶帳戶之全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration 物件。**Set-CsPrivacyConfiguration** Cmdlet 會接受管線傳送的隱私組態物件輸入。

## 傳回類型

**Set-CsPrivacyConfiguration** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)


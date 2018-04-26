---
title: Get-CsVoicePolicy
TOCTitle: Get-CsVoicePolicy
ms:assetid: 05096aec-321c-4a50-99be-6e9fbbbe17fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398101(v=OCS.15)
ms:contentKeyID: 49289950
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicePolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所設定之一或多個語音原則的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

此範例會顯示所有為組織定義的語音原則及各項語音原則的設定。

    Get-CsVoicePolicy

## 範例 2

此範例會使用 Identity 參數來擷取名為 UserPolicy1 之個別使用者原則的語音原則設定。

    Get-CsVoicePolicy -Identity UserPolicy1

## 範例 3

此範例會使用 Filter 參數來擷取可指派給使用者的所有語音原則設定。所有使用者語音原則都具有 **tag:\<UserVoicePolicy\>** 格式的 Identity，因此我們篩選 tag 來擷取所有使用者語音原則。

    Get-CsVoicePolicy -Filter tag*

## 詳細描述

此 Cmdlet 會擷取語音原則資訊。語音原則可用來管理 Enterprise Voice 相關功能，例如同時響鈴 (每次有人撥打到您的辦公室電話時，能夠讓第二支電話響起) 和來電轉接。請使用此 Cmdlet 來擷取設定，以啟用和停用其中的許多功能。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsVoicePolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicePolicy"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數接受萬用字元字串，並傳回識別符合該字串的所有語音原則。例如，Filter 值為 site:* 會傳回網站層級上定義的所有語音原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指定原則的範圍和 (在某些情況下) 名稱的唯一識別碼。如果省略此參數，則會傳回組織的所有語音原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取語音原則，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取其語音原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)


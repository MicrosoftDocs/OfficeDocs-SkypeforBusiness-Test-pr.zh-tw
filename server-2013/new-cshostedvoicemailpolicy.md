---
title: New-CsHostedVoicemailPolicy
TOCTitle: New-CsHostedVoicemailPolicy
ms:assetid: 81e1ec62-45c4-49ad-8e2b-3568c092b6c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398653(v=OCS.15)
ms:contentKeyID: 49291495
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsHostedVoicemailPolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的代管語音信箱原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsHostedVoicemailPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Destination <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Organization <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會建立新主控語音信箱原則 ExRedmond (未指定範圍時，表示此原則可以指派給個別使用者或連絡人)。此原則會定義 Exchange UM 目的地，以將此原則放在 FQDN ExUM.fabrikam.com。此外，此原則的 Lync Server 使用者可能分散在 litwareinc 的 corp1 和 corp2 組織內。此原則可描述為 (具有的 Description 參數值為)「Redmond 使用者的主控語音信箱屬性」。

    New-CsHostedVoicemailPolicy -Identity ExRedmond -Destination ExUM.fabrikam.com -Description "Hosted voicemail policy for Redmond users." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"

## 範例 2

範例 2 所示的命令是範例 1 所示的命令的變化；不過，在此情況下，新的代管語音信箱原則會指派給租用戶識別碼為 73d355dd-ce5d-4ab9-bf49-7b822c18dd98 的 Lync Online 租用戶。若要為 Lync Online 租用戶建立新原則，您必須包含 InMemory 參數，並將產生的原則存放在變數中。第一個命令的效果便是如此：新原則存放在一個名為 $x 的變數中。另外也請注意，您必須將 Identity 設為 Global，並將 Tenant 參數設為適當的租用戶識別碼。

為了建立新原則，接著第二個命令會呼叫 **Set-CsHostedVoiceMailPolicy** Cmdlet 並搭配 Instance 參數和 Tenant 參數。

    $x = New-CsHostedVoiceMailPolicy -Identity global -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98" -Destination ExUM.fabrikam.com -Description "Hosted voicemail policy for Redmond users." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"
    Set-CsHostedVoiceMailPolicy -Instance $x -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98"

## 詳細描述

此 Cmdlet 會建立原則來設定已啟用 Lync Server 或 Office Communications Server 的使用者帳戶，以使用 Exchange 整合通訊 (UM) 裝載的語音信箱服務。此原則決定如何將使用者未接聽的來電轉接至裝載的 Exchange UM 服務。

使用者必須已啟用 Exchange UM 主控的語音信箱，此原則才會生效。您可以呼叫 **Get-CsUser** Cmdlet 並檢查 HostedVoiceMail 屬性，以判斷使用者是否已啟用主控的語音信箱 (值為 True 表示使用者已啟用)。

在網站範圍建立的原則會自動指派給這些網站裝載的使用者。在個別使用者範圍上建立的原則必須透過 **Grant-CsHostedVoicemailPolicy** Cmdlet 來指派給使用者或連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsHostedVoicemailPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsHostedVoicemailPolicy"}

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
<td><p>原則的唯一識別碼，其包含範圍和網站 (若是網站原則，例如 site:Redmond)，或原則名稱 (若是個別使用者原則，例如 RenoHostedVoicemail)。全域原則永遠存在而且無法移除，因此您無法建立全域原則。</p></td>
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
<td><p>System.String</p></td>
<td><p>原則的簡易描述。</p></td>
</tr>
<tr class="even">
<td><p><em>Destination</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指派給此參數的值是裝載之 Exchange UM 服務的完整網域名稱 (FQDN)。請注意，所選擇的目的地必須為路由所信任。</p>
<p>此參數是選用的，但如果您企圖啟用使用者的主控語音信箱，且指派給使用者的原則沒有 Destination 值，則啟用作業會失敗。</p>
<p>此值必須為 255 個以下 (含) 的字元，格式為 FQDN，例如 server.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Organization</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數包含 Exchange 租用戶 (含 Lync Server 使用者) 的逗號分隔清單。必須以裝載 Exchange 服務上之租用戶的 FQDN 來指定每一位租用戶。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立之新代管語音信箱原則所針對的 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令，為每個租用戶傳回租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy 類型的物件

## 請參閱

#### 其他資源

[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)


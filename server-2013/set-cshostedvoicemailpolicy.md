---
title: Set-CsHostedVoicemailPolicy
TOCTitle: Set-CsHostedVoicemailPolicy
ms:assetid: 9c47d2a5-356c-4bab-9cef-8346c4b5d99c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412722(v=OCS.15)
ms:contentKeyID: 49291801
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsHostedVoicemailPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改代管的語音信箱原則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsHostedVoicemailPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsHostedVoicemailPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Destination <String>] [-Force <SwitchParameter>] [-Organization <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會修改主控的語音信箱原則 ExRedmond 的 Destination 屬性。它會將此原則的 Exchange UM 目的地設定在 FQDN ExUM.contoso.com。

    Set-CsHostedVoicemailPolicy -Identity ExRedmond -Destination ExUM.contoso.com

## 範例 2

此命令會將 Exchange 租用戶新增至 ExRedmond 原則的租用戶 (組織) 逗號分隔清單。第一行呼叫 **Get-CsHostedVoicemailPolicy** Cmdlet 以 Identity ExRedmond 來擷取原則。此 Cmdlet 呼叫會以括弧括住，因為我們需要先擷取此原則。接著，我們使用「點標記法」來擷取原則的 Organization 屬性。我們將傳回的字串以變數 $a 儲存。下一行使用 += 運算子，將指派的字串 (,corp3.litwareinc.com) 附加到以 $a 變數儲存的字串尾端 (請注意指派字串中的逗號。Organization 是逗號分隔清單，因此若清單中已經有值，則其他任何值的前面都必須加上逗號)。最後，我們在最終一行呼叫 **Set-CsHostedVoicemailPolicy** Cmdlet 並將變數 $a 傳遞給參數 Organization，以指派新的 Organization 字串。

    $a = (Get-CsHostedVoicemailPolicy -Identity ExRedmond).Organization
    $a += ",corp3.litwareinc.com"
    Set-CsHostedVoicemailPolicy -Identity ExRedmond -Organization $a

## 範例 3

範例 3 所示的命令可修改已指派給 Lync Online 租用戶 (租用戶識別碼為 73d355dd-ce5d-4ab9-bf49-7b822c18dd98) 之代管語音信箱原則的 Destination 屬性。

    Set-CsHostedVoicemailPolicy -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98" -Destination "ExUM.contoso.com"

## 詳細描述

此 Cmdlet 會修改原則來設定啟用 Lync Server 或 Microsoft Office Communications Server 的使用者帳戶使用 Exchange 整合通訊 (UM) 主控的語音信箱服務。此原則決定如何將使用者未接聽的來電轉接至主控的 Exchange UM 服務。

使用者必須已啟用 Exchange UM 主控的語音信箱，此原則才會生效。您可以呼叫 **Get-CsUser** Cmdlet 並檢查 HostedVoiceMail 屬性，以判斷使用者是否已啟用主控的語音信箱 (值為 True 表示使用者已啟用)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsHostedVoicemailPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsHostedVoicemailPolicy"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>原則的簡易描述。</p></td>
</tr>
<tr class="odd">
<td><p><em>Destination</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指派給此參數的值是裝載之 Exchange UM 服務的完整網域名稱 (FQDN)。請注意，所選擇的目的地必須為路由所信任。</p>
<p>如果您嘗試為主控的語音信箱啟用使用者，而為該使用者指派的原則沒有 Destination 值，則啟用將會失敗。</p>
<p>此值必須有 255 個字元或更少，且格式必須符合規則運算式字串 ^[a-zA-Z0-9\-_]+(\.[a-zA-Z0-9\-_]+){0,}$。這只是表示它應該為 FQDN 的格式，例如 server.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要修改之主控語音信箱原則的唯一識別碼。這個 Identifier 包括範圍 (若是全域)、範圍和網站 (指網站原則，例如 site:Redmond) 或原則名稱 (指個別使用者原則，例如 HVUserPolicy)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>HostedVoicemailPolicy</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。 物件的類型必須是 HostedVoicemailPolicy，而且可以透過呼叫 <strong>Get-CsHostedVoicemailPolicy</strong> Cmdlet 來擷取。</p></td>
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
<td><p>主控要修改之語音信箱原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy 物件。接受管線傳送的主控語音信箱原則物件輸入。

## 傳回類型

此 Cmdlet 會修改 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy 類型的物件

## 請參閱

#### 其他資源

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)


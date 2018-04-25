---
title: Get-CsHostedVoicemailPolicy
TOCTitle: Get-CsHostedVoicemailPolicy
ms:assetid: 52dd4397-b1c5-44a5-a744-75d715a4511b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398348(v=OCS.15)
ms:contentKeyID: 49290923
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHostedVoicemailPolicy

 

_**上次修改主題的時間：** 2015-03-09_

擷取代管的語音信箱原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsHostedVoicemailPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsHostedVoicemailPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

此命令會傳回 Lync Server 實作已定義的所有主控語音信箱原則。

    Get-CsHostedVoicemailPolicy

## 範例 2

此命令會傳回個別使用者主控語音信箱原則 ExRedmond 的原則設定。

    Get-CsHostedVoicemailPolicy -Identity ExRedmond

## 範例 3

此命令會傳回所有個別使用者主控語音信箱原則 (以標籤範圍開頭的原則) 的原則設定。

    Get-CsHostedVoicemailPolicy -Filter tag:*

## 範例 4

此命令會針對租用戶識別碼為 73d355dd-ce5d-4ab9-bf49-7b822c18dd98 的 Lync Online 租用戶傳回裝載的語音信箱原則。

    Get-CsHostedVoicemailPolicy -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98"

## 詳細描述

此 Cmdlet 會擷取原則，此原則會指定如何將使用者未接聽的來電轉接至主控的 Exchange 整合通訊 (UM) 服務。

使用者必須已啟用 Exchange UM 主控的語音信箱，此原則才會生效。您可以呼叫 **Get-CsUser** Cmdlet 並檢查 HostedVoiceMail 屬性，以判斷使用者是否已啟用主控的語音信箱(值為 True 表示使用者已啟用)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsHostedVoicemailPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHostedVoicemailPolicy"}

``` 
```

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
<td><p>此參數可讓您在主控語音信箱原則的 Identity 上執行萬用字元搜尋。這樣會擷取 Identity 符合 Filter 值中指定之萬用字元模式的所有主控語音信箱原則的執行個體。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之主控語音信箱原則的唯一識別碼。Identifier 包括範圍 (若是全域範圍)、範圍和網站 (指網站原則，例如 site:Redmond) 或原則名稱 (指個別使用者原則，例如 HVUserPolicy)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取主控的語音信箱原則，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取其語音信箱原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy 類型的物件

## 請參閱

#### 其他資源

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)


---
title: Set-CsOAuthServer
TOCTitle: Set-CsOAuthServer
ms:assetid: 52825ca3-d287-4e09-9aec-b8b2d7bafc06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204896(v=OCS.15)
ms:contentKeyID: 49290918
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOAuthServer

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的開放授權 (OAuth) 伺服器。OAuth 伺服器亦稱為安全性權杖伺服器，會發出用於伺服器對伺服器驗證及授權的安全性權杖。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsOAuthServer <COMMON PARAMETERS>

    Set-CsOAuthServer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MetadataUrl <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會更新 OAuth Server Office 365 的中繼資料 URL。

    Set-CsOAuthServer -Identity "Office 365" -MetadataUrl "https://sts.office365.microsoft.com/metadata/json/1"

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Microsoft Exchange Server 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若是使用內部部署版的 Lync Server 2013，又需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013或 Microsoft SharePoint 2013) 通訊，一般不會需要使用權杖伺服器。這是因為這些伺服器產品本身即可核發自己的安全性權杖。但您若是需要與其他伺服器產品 (包括 Office 365 的伺服器產品) 通訊，便須使用權杖伺服器。您可以使用 CsOAuthServer Cmdlet 管理這些權杖伺服器。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOAuthServer"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsOAuthServer** Cmdlet 所執行的功能。

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>用於識別 OAuth 伺服器的易記 (及唯一的) 名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MetadataUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>發佈伺服器之 WS-FederationMetadata 所在的 URL。伺服器會使用中繼資料來同意將要交換的權杖類型，以及要用來簽署這些權杖的金鑰。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改 OAuth 伺服器之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
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

**Set-CsOAuthServer** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Set-CsOAuthServer** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsOAuthServer](get-csoauthserver.md)  
[New-CsOAuthServer](new-csoauthserver.md)  
[Remove-CsOAuthServer](remove-csoauthserver.md)


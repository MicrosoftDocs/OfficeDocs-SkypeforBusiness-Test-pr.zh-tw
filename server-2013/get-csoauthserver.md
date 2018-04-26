---
title: Get-CsOAuthServer
TOCTitle: Get-CsOAuthServer
ms:assetid: c2a61eb0-cdff-4069-99e4-2bdf42812f47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205238(v=OCS.15)
ms:contentKeyID: 49292225
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOAuthServer

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之開放授權 (OAuth) 伺服器的資訊。OAuth 伺服器 (又稱為安全性權杖伺服器) 可核發伺服器對伺服器驗證及授權所需的安全性權杖。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsOAuthServer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsOAuthServer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 會傳回設定供組織使用之所有 OAuth 伺服器的資訊。

    Get-CsOAuthServer

## 範例 2

範例 2 會傳回 Identity 為 "Office 365" 的 OAuth 伺服器資訊。

    Get-CsOAuthServer -Identity "Office 365"

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Microsoft Exchange Server 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若是使用內部部署版的 Lync Server 2013，但需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，則通常不需使用權杖伺服器。這是因為這些伺服器產品就能核發自己的安全性權杖。但您若是需要與其他伺服器產品 (包括 Office 365 的伺服器產品) 通訊，便須使用權杖伺服器。您可以使用 **CsOAuthServer** Cmdlet 管理這些權杖伺服器。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOAuthServer"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsOAuthServer** Cmdlet 所執行的功能。

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
<td><p>可讓您使用萬用字元傳回一或多部 OAuth 伺服器。例如，若要傳回 Identity 包含字串值 &quot;Microsoft&quot; 的所有 OAuth 伺服器，請使用下列語法：</p>
<p>-Filter &quot;*Microsoft*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之 OAuth 伺服器的唯一識別碼。例如：</p>
<p>-Identity &quot;Office 365&quot;</p>
<p>若未在命令中加入 Identity 參數和 Filter 參數，則 <strong>Get-CsOAuthServer</strong> Cmdlet 會傳回所有 OAuth 伺服器的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 OAuth 服務資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取 OAuth 伺服器設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsOAuthServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsOAuthServer** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsOAuthServer](new-csoauthserver.md)  
[Remove-CsOAuthServer](remove-csoauthserver.md)  
[Set-CsOAuthServer](set-csoauthserver.md)


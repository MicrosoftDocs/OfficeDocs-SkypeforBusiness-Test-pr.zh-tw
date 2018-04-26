---
title: New-CsOAuthServer
TOCTitle: New-CsOAuthServer
ms:assetid: b9d10216-a743-4e62-9cf0-6d5fb55dd64e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205206(v=OCS.15)
ms:contentKeyID: 49292114
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOAuthServer

 

_**上次修改主題的時間：** 2015-03-09_

建立新的開放授權 (OAuth) 伺服器供組織使用。OAuth 伺服器 (又稱為安全性權杖伺服器) 可核發伺服器對伺服器驗證及授權所需的安全性權杖。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsOAuthServer -MetadataUrl <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsGlobalRelativeIdentity>] [-InMemory <SwitchParameter>] [-Realm <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立名為 "Office 365" 的新 OAuth 伺服器。此新伺服器使用中繼資料 URL https://sts.office365.microsoft.com/metadata/json/1。

    New-CsOAuthServer -Identity "Office 365" -MetadataUrl "https://sts.office365.microsoft.com/metadata/json/1"

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Microsoft Exchange Server 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若是使用內部部署版的 Lync Server 2013，又需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，通常不需要使用權杖伺服器。這是因為這些伺服器產品本身即可核發自己的安全性權杖。但您若是需要與其他伺服器產品 (包括 Office 365 的伺服器產品) 通訊，就需要使用權杖伺服器。您可以使用 **CsOAuthServer** Cmdlet 來管理這些權杖伺服器。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOAuthServer"}

**Lync Server 控制台：**Lync Server 控制台不提供 New-CsOAuthServer Cmdlet 所執行的功能。

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
<td><p><em>MetadataUrl</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>發行伺服器之 WS-FederationMetadata 的 URL。伺服器會使用中繼資料，以針對要交換的權杖類型及要用於簽署這些權杖的金鑰取得共識。請注意，當您執行 <strong>New-CsOAuthServer</strong> Cmdlet 時，必須提供指定的 URL，否則命令會失敗。</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>用於識別 OAuth 伺服器的易記 (及唯一的) 名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Realm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>伺服器對伺服器安全性容器。根據預設，Lync Server 2013會使用預設 SIP 網域做為其 OAuth 領域。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>所建立的新 OAuth 伺服器之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
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

無。**New-CsOAuthServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsOAuthServer** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsOAuthServer](get-csoauthserver.md)  
[Remove-CsOAuthServer](remove-csoauthserver.md)  
[Set-CsOAuthServer](set-csoauthserver.md)


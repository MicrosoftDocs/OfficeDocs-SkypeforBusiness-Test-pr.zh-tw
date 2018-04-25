---
title: Set-CsOAuthConfiguration
TOCTitle: Set-CsOAuthConfiguration
ms:assetid: 43193254-acb1-47c8-8e21-143b610c2edc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204841(v=OCS.15)
ms:contentKeyID: 49290744
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOAuthConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改組織目前所使用的開放授權 (OAuth) 組態設定。OAuth 是標準通訊協定，可用於伺服器對伺服器的驗證及授權。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsOAuthConfiguration [-ExchangeAutodiscoverAllowedDomains <String>] [-ExchangeAutodiscoverUrl <String>] [-Identity <XdsIdentity>] [-Realm <String>] [-ServiceName <String>] <COMMON PARAMETERS>

    Set-CsOAuthConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改全域的 OAuth 組態設定集合。在此範例中，Realm 屬性設為 "contoso.com"。

    Set-CsOAuthConfiguration -Identity global -Realm "contoso.com"

## 詳細描述

在 Lync Server 2013中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 及 Microsoft Exchange Server 2013 共用資訊的驗證) 由 OAuth 安全性通訊協定執行。在 Lync Server 2013 中，OAuth 一律為開啟，因此無須 (也無法) 啟用或停用此通訊協定。但 Lync Server 若要與其他伺服器產品 (例如 Exchange 2013或 Microsoft SharePoint 2013) 通訊，便須修改 OAuth 組態設定。例如，您可能需要指為 Office 365 版的 Exchange 指定自動探索 URL 及您的領域名稱。這些設定必須透過 **CsOAuthConfiguration** Cmdlet 進行管理。Lync Server 2013 控制台不提供用以管理 OAuth 設定的選項。

請注意，內部部署版的 Lync Server 2013 只會提供一組全域的 OAuth 設定集合。您無法另外建立其他 OAuth 設定集合，也無法刪除此全域集合。每個 商務用 Skype Online 租用戶都只有一個 OAuth 組態設定集合。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOAuthConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsOAuthConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>ExchangeAutodiscoverAllowedDomains</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>自動探索要求的重新導向目標網域的集合。例如：</p>
<p>-ExchangeAutodiscoverAllowedDomains &quot;*.contoso.com&quot;,&quot;*.fabrikam.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeAutodiscoverUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>Office 365 版的 Microsoft Exchange Server 所使用之自動探索服務的 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>OAuth 組態設定的唯一 Identity。因為您只能有這些設定的單一、全域執行個體，所以在呼叫 <strong>Set-CsOAuthConfiguration</strong> Cmdlet 時，不需要指定 Identity。然而，您可以使用下列語法來參照全域設定：</p>
<p>-Identity global</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Realm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>伺服器對伺服器安全性容器。根據預設，Lync Server 2013會使用預設 SIP 網域做為其 OAuth 領域。</p></td>
</tr>
<tr class="even">
<td><p><em>ServiceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>指派給 OAuth 服務的全域唯一識別碼 (GUID)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改 OAuth 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
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

**Set-CsOAuthConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthSettings 物件執行個體。

## 傳回類型

無。反之， **Set-CsOAuthConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsOAuthConfiguration](get-csoauthconfiguration.md)


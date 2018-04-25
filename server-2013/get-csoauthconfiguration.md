---
title: Get-CsOAuthConfiguration
TOCTitle: Get-CsOAuthConfiguration
ms:assetid: a3fda8bf-84e3-4d14-a1c5-093e6eb36ffe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205155(v=OCS.15)
ms:contentKeyID: 49291875
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOAuthConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織中目前所使用之開放授權 (OAuth) 組態設定的資訊。OAuth 是伺服器對伺服器驗證及授權時所使用的標準通訊協定。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsOAuthConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsOAuthConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織中使用之 OAuth 組態設定的資訊。

    Get-CsOAuthConfiguration

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 與 Microsoft Exchange Server 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。在 Lync Server 2013 中，OAuth 一律為開啟，因此您無需 (也無法) 啟用或停用此通訊協定。若 Lync Server 需要和其他伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，便需修改 OAuth 組態設定。例如，您必須指定 Office 365 版之 Exchange 的自動探索 URL 及您的領域名稱。這些設定只能透過 **CsOAuthConfiguration** Cmdlet 加以管理。Lync Server 2013 控制台不提供管理 OAuth 設定的選項。

請注意，內部部署版的 Lync Server 2013 只能有一個通用的 OAuth 設定集合，亦即您無法建立其他的 OAuth 設定集合，也無法刪除該全域集合。每個 商務用 Skype Online 租用戶也只有一個 OAuth 組態設定集合。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOAuthConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsOAuthConfiguration** Cmdlet 所執行的功能。

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
<td><p>可讓您在參考 OAuth 組態設定集合時使用萬用字元值。因為您只會有這些設定的單一全域執行個體，所以不需要使用 Filter 參數。但您可以視需要使用下列語法來參考全域設定：</p>
<p>-Filter &quot;g*&quot;</p>
<p>此語法會傳回 Identity 開頭為字母 &quot;g&quot; 的所有 OAuth 組態設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>OAuth 組態設定的唯一 Identity。因為您只會有這些設定的單一通用執行個體，所以不需要在呼叫 <strong>Get-CsOAuthConfiguration</strong> Cmdlet 時指定 Identity。但是，您可以視需要使用下列語法來參照全域設定：</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 OAuth 組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取 OAuth 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsOAuthConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsOAuthConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsOAuthConfiguration](set-csoauthconfiguration.md)


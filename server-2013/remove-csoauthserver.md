---
title: Remove-CsOAuthServer
TOCTitle: Remove-CsOAuthServer
ms:assetid: fac7be48-06bb-4572-86a2-b872fe96d199
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205408(v=OCS.15)
ms:contentKeyID: 49292886
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsOAuthServer

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的開放授權 (OAuth) 伺服器。OAuth 伺服器 (又稱為安全性權杖伺服器) 可核發伺服器對伺服器驗證及授權所需的安全性權杖。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsOAuthServer -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除單一 OAuth 伺服器：Identity 為 "Office 365" 的伺服器。

    Remove-CsOAuthServer -Identity "Office365"

## 範例 2

範例 2 會刪除已設定要在組織中使用的所有 OAuth 伺服器。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsOAuthServer** Cmdlet，以傳回所有 OAuth 伺服器。接著，再將這些伺服器管線傳送到 **Remove-CsOAuthServer** Cmdlet 加以移除。

    Get-CsOAuthServer | Remove-CsOAuthServer

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Microsoft Exchange Server 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若是使用內部部署版的 Lync Server 2013，又需要與其他完全支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，一般來講，您不需使用權杖伺服器。這是因為這些伺服器產品本身即可核發自己的安全性權杖。但您若是需要與其他伺服器產品 (包括 Office 365 的伺服器產品) 通訊，便須使用權杖伺服器。您可以使用 **CsOAuthServer** Cmdlet 管理這些權杖伺服器。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsOAuthServer"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsOAuthServer** Cmdlet 所執行的功能。

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
<td><p>要刪除之 OAuth 伺服器的唯一識別碼。例如：</p>
<p>-Identity &quot;Office 365&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>所刪除的 OAuth 伺服器之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsOAuthServer** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated 物件執行個體。

## 傳回類型

無。反之，**Remove-CsOAuthServer** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsOAuthServer](get-csoauthserver.md)  
[New-CsOAuthServer](new-csoauthserver.md)  
[Set-CsOAuthServer](set-csoauthserver.md)


---
title: Remove-CsPartnerApplication
TOCTitle: Remove-CsPartnerApplication
ms:assetid: 3918a2eb-d464-4729-888b-fafebe2227ce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204820(v=OCS.15)
ms:contentKeyID: 49290618
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPartnerApplication

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的夥伴應用程式。夥伴應用程式是 Lync Server 2013 不需要透過第三方的安全性權杖伺服器，即可直接與之交換安全性權杖的應用程式。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 "MicrosoftExchange" 的夥伴應用程式。

    Remove-CsPartnerApplication -Identity "MicrosoftExchange"

## 範例 2

範例 2 會刪除設定供組織使用的所有夥伴應用程式。為達成此目的，命令會先使用 **Get-CsPartnerApplication** Cmdlet 傳回所有夥伴應用程式的集合。然後，此集合會管線傳送到 **Remove-CsPartnerApplication** Cmdlet，以刪除集合中的每一個應用程式。

    Get-CsPartnerApplication | Remove-CsPartnerApplication

## 範例 3

範例 3 會刪除信任層級不是設為 Full 的所有夥伴應用程式。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsPartnerApplication** Cmdlet，以傳回設定供組織使用之所有夥伴應用程式的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只選取 ApplicationTrustLevel 屬性不等於 (-ne) "Full" 的應用程式。接著將符合該準則的應用程式管線傳送到 **Remove-CsPartnerApplication** Cmdlet 加以移除。

    Get-CsPartnerApplication | Where-Object {$_.ApplicationTrustLevel -ne "Full"} | Remove-CsPartnerApplication

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Exchange 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若您是使用內部部署版的 Lync Server 2013，並需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，通常來說不需要透過權杖伺服器；這是因為這些伺服器產品可以發行自己的安全性權杖。但您必須將另一項伺服器產品 (例如 Exchange 2013) 設定為夥伴應用程式 (此外也必須將 Lync Server 2013 設定為其他伺服器產品的夥伴應用程式)。在 Lync Server 2013 中，必須使用 **CsPartnerApplication** Cmdlet 管理夥伴應用程式。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPartnerApplication"}

**Lync Server 控制台：** **Remove-CsPartnerApplication** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要移除之夥伴應用程式的唯一識別碼。例如：</p>
<p>-Identity &quot;MicrosoftExchange&quot;</p>
<p>請注意，指定 Identity 時不能使用萬用字元。</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要刪除夥伴應用程式之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p></td>
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

**Remove-CsPartnerApplication** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated 物件執行個體。

## 傳回類型

無。反之，**Remove-CsPartnerApplication** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPartnerApplication](get-cspartnerapplication.md)  
[New-CsPartnerApplication](new-cspartnerapplication.md)  
[Set-CsPartnerApplication](set-cspartnerapplication.md)


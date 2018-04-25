---
title: Get-CsPartnerApplication
TOCTitle: Get-CsPartnerApplication
ms:assetid: a20738b5-d9e7-4da4-bcac-e967f73c4bdc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205128(v=OCS.15)
ms:contentKeyID: 49291851
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPartnerApplication

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之所有夥伴應用程式的資訊。夥伴應用程式是 Lync Server 2013 不需要透過第三方的安全性權杖伺服器，即可直接與之交換安全性權杖的應用程式。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPartnerApplication [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPartnerApplication [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有夥伴應用程式的資訊。

    Get-CsPartnerApplication

## 範例 2

範例 2 會傳回 Identity 為 MicrosoftExchange 之夥伴應用程式的資訊。

    Get-CsPartnerApplication -Identity "MicrosoftExchange"

## 範例 3

範例 3 會傳回應用程式識別碼等於 "microsoft.exchange" 之所有夥伴應用程式的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPartnerApplication** Cmdlet，以傳回所有已設定的夥伴應用程式集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 ApplicationIdentifier 屬性等於 "microsoft.exchange" 的夥伴應用程式。

    Get-CsPartnerApplication | Where-Object {$_.ApplicationIdentifier -eq "microsoft.exchange"}

## 範例 4

範例 4 會傳回目前已停用之所有夥伴應用程式的資訊。為達成此目的，命令會先呼叫 **Get-CsPartnerApplication** Cmdlet，以傳回已啟用及已停用之所有夥伴應用程式集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Enabled 屬性等於 False 的應用程式。

    Get-CsPartnerApplication | Where-Object {$_.Enabled -eq $False}

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Exchange 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若您是使用內部部署版的 Lync Server 2013，並需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，通常來說不需要透過權杖伺服器；這是因為這些伺服器產品可以發行自己的安全性權杖。但您必須將另一項伺服器產品 (例如 Exchange 2013) 設定為夥伴應用程式 (此外也必須將 Lync Server 2013 設定為其他伺服器產品的夥伴應用程式)。在 Lync Server 2013 中，必須使用 **CsPartnerApplication** Cmdlet 管理夥伴應用程式。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPartnerApplication"}

**Lync Server 控制台：** **Get-CsPartnerApplication** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>System.Strkng</p></td>
<td><p>可讓您使用萬用字元值傳回一或多個夥伴應用程式。例如，若要傳回 Identity 包含字串值 &quot;Microsoft&quot; 的所有夥伴應用程式，請使用下列語法：</p>
<p>-Filter &quot;*Microsoft*&quot;</p>
<p>請勿在同一個命令中同時使用 Filter 參數和 Identity 參數。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>夥伴應用程式的唯一識別碼。例如：</p>
<p>-Identity &quot;MicrosoftExchange&quot;</p>
<p>命令中若未加入 Identity 參數和 Filter 參數， <strong>Get-CsPartnerApplication</strong> Cmdlet 會傳回所有夥伴應用程式的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取夥伴應用程式組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取夥伴應用程式設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPartnerApplication** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPartnerApplication** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsPartnerApplication](new-cspartnerapplication.md)  
[Remove-CsPartnerApplication](remove-cspartnerapplication.md)  
[Set-CsPartnerApplication](set-cspartnerapplication.md)


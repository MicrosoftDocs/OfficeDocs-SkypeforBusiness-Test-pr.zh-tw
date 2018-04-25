---
title: New-CsPartnerApplication
TOCTitle: New-CsPartnerApplication
ms:assetid: 0248acde-626d-42b4-a071-c96171364a18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204628(v=OCS.15)
ms:contentKeyID: 49289906
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPartnerApplication

 

_**上次修改主題的時間：** 2015-03-09_

建立新的夥伴應用程式。夥伴應用程式是 Lync Server 2013不需要透過第三方的安全性權杖伺服器，即可直接與之交換安全性權杖的應用程式。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPartnerApplication -ApplicationIdentifier <String> -ApplicationTrustLevel <User | Application | Full> -CertificateRawData <String> -Realm <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Tenant <Guid>] <COMMON PARAMETERS>

    New-CsPartnerApplication -ApplicationIdentifier <String> -ApplicationTrustLevel <User | Application | Full> -CertificateFileData <String> -Realm <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Tenant <Guid>] <COMMON PARAMETERS>

    New-CsPartnerApplication -ApplicationIdentifier <String> -ApplicationTrustLevel <User | Application | Full> -UseOAuthServer <SwitchParameter> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Realm <String>] [-Tenant <Guid>] <COMMON PARAMETERS>

    New-CsPartnerApplication -ApplicationTrustLevel <User | Application | Full> -MetadataUrl <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Tenant <Guid>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Identity 為 "MicrosoftExchange" 的新夥伴應用程式。在此範例中，新夥伴應用程式會使用中繼資料 URL https://autodiscover.litwareinc.com/metadata/json/1。

    New-CsPartnerApplication -Identity "MicrosoftExchange" -ApplicationTrustLevel "Full" -MetadataUrl"https://autodiscover.litwareinc.com/metadata/json/1"

## 範例 2

範例 2 所示的命令也會建立 Identity 為 "MicrosoftExchange" 的新夥伴應用程式。但在此範例中，新夥伴應用程式不會使用中繼資料 URL，而會設定成使用預先定義的 OAuth Server。為達此目的，命令會使用 UseOAuthServer 參數，而不會使用 MetadataUrl 參數。

    New-CsPartnerApplication -Identity "MicrosoftExchange" -ApplicationIdentifier "microsoft.exchange" -ApplicationTrustLevel "Full" -UseOAuthServer

## 詳細描述

在 Lync Server 2013 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Exchange 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若您是使用內部部署版的 Lync Server 2013，並需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，通常來說不需要透過權杖伺服器；這是因為這些伺服器產品可以發行自己的安全性權杖。但您必須將另一項伺服器產品 (例如 Exchange 2013) 設定為夥伴應用程式 (此外也必須將 Lync Server 2013 設定為其他伺服器產品的夥伴應用程式)。在 Lync Server 2013 中，必須使用 **CsPartnerApplication** Cmdlet 管理夥伴應用程式。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPartnerApplication"}

**Lync Server 控制台：** **New-CsPartnerApplication** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>ApplicationIdentifier</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>夥伴應用程式的唯一識別碼。ApplicationIdentifier 由伺服器應用程式提供。您無法在同一命令中使用 ApplicationIdentifier 參數與 MetadataUrl 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>ApplicationTrustLevel</em></p></td>
<td><p>必要</p></td>
<td><p>ApplicationTrustLevel</p></td>
<td><p>指定 Lync Server 2013與夥伴應用程式之間的信任層級。允許的值為：</p>
<p>* Full -- 信任夥伴應用程式代表自己，並模擬該領域中的使用者。此為預設值。</p>
<p>* Application -- 信任夥伴應用程式在領域中代表自己。若要模擬使用者，必須先取得安全性權杖伺服器的同意聲明。</p>
<p>* User -- 夥伴應用程式必須先取得安全性權杖伺服器的同意聲明，才可代表使用者，而且也不可代表自己。</p>
<p>預設值為 Full。</p></td>
</tr>
<tr class="odd">
<td><p><em>CertificateFileData</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>可指派給夥伴應用程式之憑證檔案的路徑。例如：</p>
<p>-CertificateFileData &quot;C:\Certificates\PartnerApplication.cer&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateRawData</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>可指派給夥伴應用程式的憑證 (Base64 編碼格式)。若要從憑證讀取原始資料，然後將該資料轉換成所需格式，請使用類似下列的命令：</p>
<p>$x = Get-Content &quot;C:\Certificates\PartnerApplication.cer&quot; –Encoding Byte</p>
<p>$y = [Convert]::ToBase64String($x)</p>
<p>您可以使用此語法指派 $y 變數中所儲存的憑證資料：</p>
<p>-CertificateRawData $y</p></td>
</tr>
<tr class="odd">
<td><p><em>MetadataUrl</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>發佈夥伴應用程式之 WS-FederationMetadata 所在的 URL。夥伴應用程式會使用中繼資料來接受所要交換的權杖類型，以及要用於簽署這些權杖的金鑰。</p></td>
</tr>
<tr class="even">
<td><p><em>UseOAuthServer</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>如有指定此參數，表示夥伴應用程式將使用其中一部預先授權的 OAuth 伺服器，而不是使用應用程式本身所內建的安全性權杖伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><em>AcceptSecurityIdentifierInformation</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True ($True) 時，安全性識別碼 (SID) 可用於驗證。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，將會啟用夥伴應用程式供立即之用。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>新夥伴應用程式的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Realm</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>伺服器對伺服器安全性容器。根據預設， Lync Server 2013會使用預設 SIP 網域做為其 OAuth 領域。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>Guid</p></td>
<td><p>要建立新夥伴應用程式之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsPartnerApplication** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPartnerApplication** Cmdlet 會建立新的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPartnerApplication](get-cspartnerapplication.md)  
[Remove-CsPartnerApplication](remove-cspartnerapplication.md)  
[Set-CsPartnerApplication](set-cspartnerapplication.md)


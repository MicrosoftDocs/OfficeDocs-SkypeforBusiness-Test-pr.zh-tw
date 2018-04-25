---
title: Set-CsPartnerApplication
TOCTitle: Set-CsPartnerApplication
ms:assetid: 29c8c511-157b-478e-814f-b911955a8251
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204755(v=OCS.15)
ms:contentKeyID: 49290399
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPartnerApplication

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的夥伴應用程式。夥伴應用程式是 商務用 Skype Online 不需要透過第三方的安全性權杖伺服器，即可直接與之交換安全性權杖的應用程式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> -MetadataUrl <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -CertificateRawData <String> -Identity <XdsGlobalRelativeIdentity> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -CertificateFileData <String> -Identity <XdsGlobalRelativeIdentity> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> -UseOAuthServer <SwitchParameter> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用夥伴應用程式 MicrosoftExchange。作法是將 Enabled 屬性設為 False ($False)。

    Set-CsPartnerApplication -Identity "MicrosoftExchange" -Enabled $False

## 範例 2

在範例 2 中，會停用組織目前所使用的所有夥伴應用程式。為達成此目的，命令會先呼叫 **Get-CsPartnerApplication** Cmdlet 傳回所有夥伴應用程式的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。接著 **ForEach-Object** Cmdlet 會對集合中的每個應用程式執行 **Set-CsPartnerApplication** Cmdlet ，以停用所有夥伴應用程式。

    Get-CsPartnerApplication | ForEach-Object {Set-CsPartnerApplication -Identity $_.Identity -Enabled $False}

## 範例 3

範例 3 會停用 ApplicationTrustLevel 屬性設為 User 的所有夥伴應用程式。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsPartnerApplication** Cmdlet ，它會傳回設定供組織使用之所有夥伴應用程式的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 ApplicationTrustLevel 屬性等於 "User" 的應用程式。接著將篩選後的集合管線傳送到 **ForEach-Object** Cmdlet，它使用 **Set-CsPartnerApplication** Cmdlet 取得集合中的每個項目，並將 Enabled 屬性設為 $False。

    Get-CsPartnerApplication | Where-Object {$_.ApplicationTrustLevel -eq "User"} | ForEach-Object {Set-CsPartnerApplication -Identity $_.Identity -Enabled $False}

## 詳細描述

在 商務用 Skype Online 中，伺服器對伺服器的驗證 (例如可以讓 Lync Server 2013 與 Exchange 2013 共用資訊的驗證) 可利用 OAuth 安全性通訊協定來達成。此種驗證類型通常會需要三部伺服器：其中兩部 (伺服器 A 與 B) 需要相互通訊，另一部則是協力廠商安全性權杖伺服器。當伺服器 A 與 B 需要相互通訊時，會連絡權杖伺服器 (又稱為 OAuth 伺服器)，以取得彼此信任的安全性權杖讓兩部伺服器可以交換證明其身分。

若您是使用內部部署版的 Lync Server 2013，並需要與其他支援 OAuth 通訊協定的伺服器產品 (例如 Exchange 2013 或 Microsoft SharePoint 2013) 通訊，通常來說不需要透過權杖伺服器；這是因為這些伺服器產品可以發行自己的安全性權杖。但您必須將另一項伺服器產品 (例如 Exchange 2013) 設定為夥伴應用程式 (此外也必須將 Lync Server 2013 設定為其他伺服器產品的夥伴應用程式)。在 Lync Server 2013 中，必須使用 **CsPartnerApplication** Cmdlet 管理夥伴應用程式。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPartnerApplication"}

**Lync Server 控制台：** **Set-CsPartnerApplication** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>夥伴應用程式的唯一識別碼。例如：</p>
<p>-Identity &quot;MicrosoftExchange&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>MetadataUrl</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>帶有簽署金鑰、發行者識別碼及發行者端點 URL 之安全性權杖服務同盟中繼資料的 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseOAuthServer</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>如有指定此參數，夥伴應用程式會使用所設定的 OAuth Server 來進行伺服器對伺服器驗證。此參數不存在時，夥伴應用程式會使用其內建的安全性權杖服務來進行伺服器對伺服器驗證。</p></td>
</tr>
<tr class="even">
<td><p><em>AcceptSecurityIdentifierInformation</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True ($True) 時，安全性識別碼 (SID) 可用於驗證。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>ApplicationTrustLevel</em></p></td>
<td><p>選用</p></td>
<td><p>ApplicationTrustLevel</p></td>
<td><p>指定 Lync Server 2013 與夥伴應用程式之間的信任層級。允許的值為：</p>
<p>* Full -- 信任夥伴應用程式代表自己，並模擬該領域中的使用者。此為預設值。</p>
<p>* Application -- 信任夥伴應用程式在領域中代表自己。若要模擬使用者，必須先取得安全性權杖伺服器的同意聲明。</p>
<p>* User -- 夥伴應用程式必須先取得安全性權杖伺服器的同意聲明，才可代表使用者，而且也不可代表自己。</p>
<p>預設值為 Full。</p></td>
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
<td><p>此參數設為 True 時，夥伴應用程式可與 Lync Server 2013 搭配使用。設為 False 時，夥伴應用程式會繼續執行，但無法與 Lync Server 通訊，直到 Enabled 屬性設為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>Guid</p></td>
<td><p>要修改夥伴應用程式之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
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

無。**Set-CsPartnerApplication** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之， **Set-CsPartnerApplication** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPartnerApplication](get-cspartnerapplication.md)  
[New-CsPartnerApplication](new-cspartnerapplication.md)  
[Remove-CsPartnerApplication](remove-cspartnerapplication.md)


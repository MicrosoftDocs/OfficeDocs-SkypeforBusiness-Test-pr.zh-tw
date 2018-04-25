---
title: Request-CsCertificate
TOCTitle: Request-CsCertificate
ms:assetid: 24e8ba6f-6023-4c03-a594-5b40784fd16a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425723(v=OCS.15)
ms:contentKeyID: 49290362
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Request-CsCertificate

 

_**上次修改主題的時間：** 2015-03-09_

可用於要求憑證，以在 Lync Server 伺服器與伺服器角色上使用。此外也可用於檢查現有憑證要求的狀態及 (如有需要) 取消任何 (或所有) 要求。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Request-CsCertificate -New <SwitchParameter> -Type <CertType[]> [-AllSipDomain <SwitchParameter>] [-CA <String>] [-CaAccount <String>] [-CaPassword <String>] [-City <String>] [-ClientEKU <$true | $false>] [-ComputerFqdn <Fqdn>] [-Country <String>] [-DomainName <String>] [-FriendlyName <String>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-KeyAlg <RSA | ECDH_P256 | ECDH_P384 | ECDH_P521>] [-KeySize <Int32>] [-Organization <String>] [-OU <String>] [-Output <String>] [-PrivateKeyExportable <$true | $false>] [-State <String>] [-Template <String>] <COMMON PARAMETERS>

    Request-CsCertificate -List <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Retrieve <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Clear <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新的憑證要求：它會連絡 CA atl-ca-001.litwareinc.com\\myca 並要求新的 WebServicesExternal 憑證。

    Request-CsCertificate -New -Type WebServicesExternal -CA "atl-ca-001.litwareinc.com\myca"

## 範例 2

範例 2 會列出使用 **Request-CsCertificate** Cmdlet 來提出的所有擱置中憑證要求。

    Request-CsCertificate -List

## 範例 3

範例 3 會使用 Output 參數建立離線憑證要求。

    Request-CsCertificate -New -Type WebServicesExternal -Output C:\Certificates\WebServicesExternal.cer

## 範例 4

範例 4 更詳細 (更實際) 地說明如何使用 Request-CsCertificate。此範例要求一個與 Lync Server 標準版搭配使用的憑證

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Standard Edition Certficate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-cs-001.litwareinc.com,atl-ext.litwareinc.com"

## 範例 5

在範例 5 中，要求一個與 Lync Server 企業版搭配使用的集區憑證

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Enterprise Edition Pool Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "pool1.litwareinc.com,pool1int.litwareinc.com,pool1ext.litwareinc.com"

## 範例 6

範例 6 顯示如何要求用於內部 Edge Server 的憑證。

    Request-CsCertificate -New -Type Internal -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Internal Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com, ap.litwareinc.com"

## 範例 7

範例 7 是範例 6 所示命令的另一種變化。但在此範例中，要求是針對外部 Edge Server。

    Request-CsCertificate -New -Type AccessEdgeExternal,DataEdgeExternal,AudioVideoAuthentication -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "External Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com,ap.litwareinc.com,dp.litwareinc.com,atl-edge-001"

## 詳細描述

Lync Server 使用憑證做為一種讓伺服器和伺服器角色確認其身分的方法；例如，Edge Server 會使用憑證確認與其通訊的電腦是否真的是前端伺服器，反之亦然。若要完整實作 Lync Server，您必須將適當的憑證指派給適當的伺服器角色。

要求憑證以便搭配 Lync Server 使用的其中一個方法是呼叫 **Request-CsCertificate** Cmdlet。雖然可以使用其他標準 Windows 工具來要求憑證以便搭配 Lync Server 使用，但是，使用 **Request-CsCertificate** Cmdlet 的其中一個主要優點是，該 Cmdlet 將會先分析您的拓撲，之後才連絡憑證授權單位 (CA)。根據該分析，**Request-CsCertificate** Cmdlet 將會使用適當的 \[主體名稱\] 及 \[主體別名\] 欄位自動要求憑證。

**Request-CsCertificate** Cmdlet 是特別針對要求搭配 Lync Server 使用的憑證而設計，而不是針對進行所有用途的憑證管理工具而設計。

除了要求新的憑證之外，此 Cmdlet 也可以用來檢閱任何擱置的憑證要求；前提是，那些是使用 **Request-CsCertificate** Cmdlet 所做的要求。**Request-CsCertificate** Cmdlet 也可以用來刪除擱置的憑證要求，前提是，那些是使用該 Cmdlet 所做的要求。

在嘗試擷取憑證要求時，如果您有任何撤銷的要求，可能會收到錯誤訊息；目前 **Request-CsCertificate** Cmdlet 僅支援下列要求類型：發行、拒絕和擱置。如果您因為撤銷的憑證而遇到問題，請使用類似下列的命令來清除撤銷的要求 (其中 224 是撤銷的憑證要求的 RequestID)：

Request-CsCertificate –Clear –RequestID 224

之後，您應該就能夠擷取憑證要求。

誰可以執行這個 Cmdlet：您必須是本機系統管理員，且具有指定之憑證授權單位的權限，才能在本機執行 **Request-CsCertificate** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Request-CsCertificate"}

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
<td><p><em>Clear</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果使用此參數，會刪除使用 <strong>Request-CsCertificate</strong> Cmdlet 所做的所有擱置中憑證要求。</p></td>
</tr>
<tr class="even">
<td><p><em>List</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果使用此參數，會列出使用 <strong>Request-CsCertificate</strong> Cmdlet 所做的所有擱置中憑證要求。</p></td>
</tr>
<tr class="odd">
<td><p><em>New</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，表示您要要求新的憑證。</p></td>
</tr>
<tr class="even">
<td><p><em>Retrieve</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果使用此參數，會擷取使用 <strong>Request-CsCertificate</strong> Cmdlet 所做的所有擱置中憑證要求，並嘗試完成作業及匯入要求的憑證。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要求的憑證類型。憑證類型包括 (但不限於)：</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (僅限 Microsoft Lync Online 2010)</p>
<p>ProvisionService (僅限 Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>例如，以下這個語法要求一個新預設憑證：-Type Default。</p>
<p>您可以在單一命令中以逗號隔開憑證類型，以指定多種類型：</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>AllSipDomain</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，您所有的 SIP 網域應會自動新增至憑證的 [主體替代名稱] 欄位中。如果不存在，則預設只會新增主要 SIP 網域。不過，您可以使用 DomainName 參數來指定其他網域。</p></td>
</tr>
<tr class="odd">
<td><p><em>CA</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指向 CA 的完整網域名稱 (FQDN)。例如：-CA &quot;atl-ca-001.litwareinc.com\myca&quot;。若要取得已知 CA 的清單，請在 Windows PowerShell 提示字元下輸入下列字串，然後按下 ENTER：</p>
<p>certutil</p>
<p>由 Certutil 傳回的 Config 屬性會指出 CA 的位置。</p></td>
</tr>
<tr class="even">
<td><p><em>CaAccount</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要求新憑證之使用者的帳戶名稱，必須使用「網域名稱\使用者名稱」格式。例如：-CaAccount &quot;litwareinc\kenmyer&quot;。若未指定，<strong>Request-CsCertificate</strong> Cmdlet 會使用要求新憑證時所登入之使用者的憑證。</p></td>
</tr>
<tr class="odd">
<td><p><em>CaPassword</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要求新憑證之使用者的密碼 (使用 CaAccount 參數指定)。</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將要部署憑證的城市。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientEKU</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果要使用憑證來進行用戶端驗證，請將此參數設為 True。如果您希望您的使用者能夠與擁有 AOL 帳戶的人員交換立即訊息，則需要這種類型的驗證。參數名稱的 EKU 部分是 Extended Key Usage (擴充金鑰使用方法) 的縮寫；擴充金鑰使用方法欄位會列出有效的憑證使用方法。</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>正在要求憑證之電腦的 FQDN。如果使用此參數，會強制 <strong>Request-CsCertificate</strong> 連線至中央管理存放區 Cmdlet 找出指定的電腦。要求憑證時，即使是要求集區憑證，一律應該使用電腦名稱。<strong>Request-CsCertificate</strong> Cmdlet 會自動將集區名稱新增至使用此 Cmdlet 所取得之任何憑證的主體名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將要部署憑證的國家/地區。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>逗號分隔的完整網域名稱清單應該新增至憑證的 [主體替代名稱] 欄位中。例如：</p>
<p>-DomainName &quot;atl-cs-001.litwareinc.com, atl-cs-002.litwareinc.com,atl-cs-003.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>FriendlyName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>使用者指派的名稱，這個名稱較容易識別憑證。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果您要在電腦上使用網域中的帳戶執行 <strong>Request-CsCertificate</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定儲存在 Active Directory 網域服務 的系統容器中，則此參數必須指向根網域控制站。如果全域設定儲存在設定容器中，則可以使用任何網域控制站，而且可以省略此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>KeyAlg</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.X509Certificates.KeyAlgorithmIdentifier</p></td>
<td><p>表示用來為新憑證產生公開金鑰與私密金鑰的密碼編譯演算法類型。有效的金鑰演算法包括：</p>
<p>RSA</p>
<p>ECDH_P256</p>
<p>ECDH_P384</p>
<p>ECDH_P521</p></td>
</tr>
<tr class="odd">
<td><p><em>KeySize</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>表示憑證使用的私密金鑰大小 (以位元為單位)。金鑰越大越安全，但需要更多額外處理工作才能解密。</p>
<p>有效金鑰大小為：1024、2048 和 4096。例如：-KeySize 2048。</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要求新憑證之組織的名稱。例如：-Organization &quot;Litwareinc&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將被指派新憑證之電腦的 Active Directory 組織單位。</p></td>
</tr>
<tr class="even">
<td><p><em>Output</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>憑證檔案的路徑。如果您想要建立離線憑證要求，請使用 Output 參數，並指定憑證要求的檔案路徑；例如：-Output C:\Certificates\NewCertificate.pfx。這樣會建立憑證要求檔，此檔案可以透過電子郵件寄給憑證授權單位以進行處理。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果您希望憑證的私密金鑰變成可以匯出，請將此參數設為 True。當私密金鑰可以匯出時，即可複製該憑證並在多台電腦上使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestId</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>與憑證要求相關聯的識別碼。RequestID 參數可讓您列出、擷取或清除個別的憑證。</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將要部署憑證的美國州名。例如：-State WA。</p></td>
</tr>
<tr class="odd">
<td><p><em>Template</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>表示產生新憑證時要使用的憑證範本；例如：-Template &quot;WebServer&quot;。要求的範本必須安裝在 CA 上。請注意，輸入的值必須是範本名稱，而非範本顯示名稱。</p></td>
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

無。**Request-CsCertificate** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Request-CsCertificate** Cmdlet 有助於管理 Microsoft.Rtc.Management.Deployment.CertificateReference 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)


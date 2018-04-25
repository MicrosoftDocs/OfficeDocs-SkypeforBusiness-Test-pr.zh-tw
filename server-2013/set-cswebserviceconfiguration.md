---
title: Set-CsWebServiceConfiguration
TOCTitle: Set-CsWebServiceConfiguration
ms:assetid: 5aa0316d-afd8-4cc2-b606-0e720e6ab021
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398396(v=OCS.15)
ms:contentKeyID: 49291018
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2014-06-05_

修改現有的 Web 服務組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsWebServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsWebServiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowAnonymousAccessToLWAConference <$true | $false>] [-AllowExternalAuthentication <$true | $false>] [-AutoLaunchLyncWebAccess <$true | $false>] [-CASigningKeyLength <UInt64>] [-Confirm [<SwitchParameter>]] [-CrossDomainAuthorizationList <PSListModifier>] [-DefaultValidityPeriodHours <UInt64>] [-EnableCertChainDownload <$true | $false>] [-EnableGroupExpansion <$true | $false>] [-Force <SwitchParameter>] [-InferCertChainFromSSL <$true | $false>] [-MACResolverUrl <String>] [-MaxCSRKeySize <UInt64>] [-MaxGroupSizeToExpand <UInt32>] [-MaxValidityPeriodHours <UInt64>] [-MinCSRKeySize <UInt64>] [-MinValidityPeriodHours <UInt64>] [-SecondaryLocationSourceUrl <String>] [-ShowAlternateJoinOptionsExpanded <$true | $false>] [-ShowDownloadCommunicatorAttendeeLink <$true | $false>] [-ShowJoinUsingLegacyClientLink <$true | $false>] [-TrustedCACerts <PSListModifier>] [-UseCertificateAuth <$true | $false>] [-UseDomainAuthInLWA <$true | $false>] [-UsePinAuth <$true | $false>] [-UseWindowsAuth <None | Negotiate | NTLM>] [-UseWsFedPassiveAuth <$true | $false>] [-WhatIf [<SwitchParameter>]] [-WsFedPassiveMetadataUri <String>]

## 範例

## 範例 1

範例 1 將 Web 服務 組態設定的群組擴充套用至 Redmond 網站 (-Identity site:Redmond)。加入 EnableGroupExpansion 屬性，並將參數值設為 True 可完成這個工作。

    Set-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $True

## 範例 2

在範例 2 中，於網站範圍套用之所有 Web 服務組態設定的有效期間上限會變更為 16 小時。為了執行此工作，命令會呼叫 **Get-CsWebServiceConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭為字元 "site:" 的設定。然後，此集合會管線傳送到 **Set-CsWebServiceConfiguration** Cmdlet，以將集合中每個項目的 MaxValidityPeriodHours 屬性變更為 16。

    Get-CsWebServiceConfiguration -Filter "site:*" | Set-CsWebServiceConfiguration -MaxValidityPeriodHours 16

## 範例 3

範例 3 會將允許群組擴充之 Web 服務組態設定的每個集合的群組擴充大小設為 400。為達成此目的，命令會呼叫不含任何參數的 **Get-CsWebServiceConfiguration** Cmdlet，以傳回組織中所使用之所有 Web 服務組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnableGroupExpansion 屬性等於 True 的設定。接著將篩選後的集合管線傳送到 **Set-CsWebServiceConfiguration** Cmdlet，以將集合中每個項目的 MaxGroupSizeToExpand 屬性的值設為 400。

    Get-CsWebServiceConfiguration | Where-Object {$_.EnableGroupExpansion -eq $True} | Set-CsWebServiceConfiguration -MaxGroupSizeToExpand 400

## 範例 4

範例 4 所示的命令會顯示如何設定全域 Web 服務設定，以便使用 Lync 以外的用戶端應用程式加入會議的使用者先看到一個指引他們下載 Lync Web App 的網站連結。作法是加入 ShowDownloadCommunicatorAttendeeLink 參數，並將參數值設為 $True。

    Set-CsWebServiceConfiguration -Identity global -ShowDownloadCommunicatorAttendeeLink $True 

## 範例 5

範例 5 所示的命令會將網域 http://fabrikam.com 新增至現有的 Web 服務組態設定集合。為了執行此工作，範例中的第一個命令使用 **New-CsWebOrigin** Cmdlet 建立 fabrikam.com 的網域物件。產生的網域物件儲存於名為 $x 的變數中。

範例中的第二個命令使用 **Set-CsWebServiceConfiguration** Cmdlet，將 http://fabrikam.com 新增至套用於 Redmond 網站的 Web 服務組態設定。其中語法 @{Add=$x} 會新增該網域至已獲得可執行跨網域指令碼之網域集合中的任何網域。若要僅以 http://fabrikam.com 取代現有的集合，可使用語法 @{Replace=$x}。

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    Set-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList @{Add=$x}

## 範例 6

範例 6 會將列在已獲得授權可執行跨網域指令碼之網域集合中的第一個網域，從 Redmond 網站的 Web 服務組態設定中移除。為了執行此工作，範例中第一個命令使用 **Get-CsWebServiceConfiguration** Cmdlet 傳回 Redmond 網站目前的設定。這些值會儲存在名為 $x 的變數中。

第二個命令使用 RemoveAt 方法，以移除 CrossDomainAuthorizationList 屬性中的第一個網域。網域是以陣列的方式儲存在此屬性中，其中第一個網域的索引號碼為 0，第二個網域的索引號碼為 1，以此類推。若要從 CrossDomainAuthorizationList 屬性中移除第二個網域 (索引號碼 1)，請使用下列語法︰

$x.CrossDomainAuthorizationList.RemoveAt(1)

請注意，命令 2 是從儲存在 $x 變數的 Redmond 網站複本中移除網域，而非從網站本身移除。為了要實際從 Redmond 網站移除網域，範例中第三個命令使用 **Set-CsWebServiceConfiguration** Cmdlet 與 Instance 參數，以使用儲存在 $x 中的設定來覆寫 Redmond 網站的設定。

    $x = Get-CsWebServiceConfiguration -Identity "site:Redmond"
    $x.CrossDomainAuthorizationList.RemoveAt(0)
    Set-CsWebServiceConfguration -Instance $x

## 範例 7

範例 7 所示的命令會移除已獲得授權可執行跨網域指令碼的所有網域，進而修改 Redmond 網站的 Web 服務組態設定。作法是將 CrossDomainAuthorizationList 屬性設為 Null 值 ($Null)。

    Set-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $Null

## 詳細描述

許多 Lync Server 元件都是 Web 元件，會使用 Web 服務或網頁執行工作。例如，使用者利用 Web 服務搜尋通訊錄的新連絡人，或使用群組擴充來檢視通訊群組的個別成員。同樣地，從電話撥入式會議到 Lync Server 控制台，都會使用網頁做為 Lync Server 和使用者之間的介面。

**CsWebServiceConfiguration** Cmdlet 可讓系統管理員管理整個組織的 Web 服務組態設定。其中包括管理群組擴充、憑證設定以及允許的驗證方法。因為您可以在全域、網站和服務範圍 (雖然只針對 Web 服務) 設定不同的設定，所以可以為不同的使用者和不同的位置自訂 Web 服務功能。 **CsWebServiceConfiguration** Cmdlet 可讓系統管理員管理整個組織的 Web 服務組態設定。其中包括管理群組擴充、憑證設定以及允許的驗證方法。因為您可以在全域、網站及服務範圍 (只針對 Web 服務) 設定不同的設定，所以可以為不同的使用者和不同的位置自訂 Web 服務功能。

您可以在建立新的 Web 服務 組態設定集合時，指定自訂設定 (例如憑證的自訂有效期間)。或者，您可以使用 **Set-CsWebServiceConfiguration** Cmdlet 修改現有集合的屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsWebServiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsWebServiceConfiguration"}

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
<td><p><em>AllowAnonymousAccessToLWAConference</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，允許匿名使用者參加 Lync Web App 會議。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExternalAuthentication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True (預設值)，可使用 OAuth 驗證來驗證外部使用者。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AutoLaunchLyncWebAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數已被淘汰，無法再於內部部署版的 Lync Server 2013中使用。</p>
<p>此參數設為 True 時，會自動使用 Lync Web App 來做為參加線上會議的預設 Web 快顯視窗，但需符合使用 Lync Web App 的先決條件 (例如，已安裝 Silverlight，而且 Internet Explorer 不會封鎖快顯視窗)。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>CASigningKeyLength</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>設定 CA 簽署金鑰的大小；簽署金鑰是憑證授權單位 (CA) 用來簽署數位憑證的私密金鑰。簽署金鑰的長度可設為 2048 和 16384 個位元組之間的任何整數值；預設值為 2048。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CrossDomainAuthorizationList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可主控會傳送跨網域指令碼要求至 Lync Server 2013 部署之 Web 應用程式的網域集合。</p>
<p>要新增至此清單的網域必須使用 New-CsWebOrigin Cmdlet 建立，然後新增至 Web 服務組態設定的新集合中。請注意，網域名稱的開頭也必須使用 http: 或 https: 前置詞。如需詳細資訊，請參閱此說明主題的範例 5、6 和 7。</p>
<p>此參數已在 Lync Server 2013 的 2013 年 2 月版本中導入。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultValidityPeriodHours</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>使用憑證驗證時，用戶端可要求憑證保持有效的時間 (單位為小時)。DefaultValidityPeriodHours 代表如果用戶端不要求自訂有效期間，則憑證將維持有效的時間長度。</p>
<p>DefaultValidityPeriodHours 可以是介於 8 小時到 8760 小時 (365 天) 之間的任何整數值。預設值為 4320 (180 天)。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCertChainDownload</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，具有驗證憑證的伺服器將下載該憑證的憑證鏈結。憑證鏈結會追蹤個別憑證，一直追溯到發行的 CA。憑證的 CA 必須是受信任的，系統才會接受該憑證進行驗證。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableGroupExpansion</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數若設為 True，則將啟用 Lync 中的群組擴充。使用者可以使用群組擴充，將通訊群組設定為連絡人，然後「展開」該群組。群組展開後，使用者就可以看到群組的個別成員及其目前狀態資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之 Web 服務 組態設定的唯一識別碼。若要修改在網站範圍設定的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要修改在服務範圍設定的設定，請使用類似下列的語法：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>若要修改在全域範圍設定的設定，您可以使用下列語法：-identity global。</p>
<p>如果未使用 Identity 參數，則 <strong>Set-CsWebServiceConfiguration</strong> Cmdlet 將會自動修改全域集合。</p></td>
</tr>
<tr class="even">
<td><p><em>InferCertChainFromSSL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，伺服器會使用安全通訊端層 (SSL) 通訊協定中包含的憑證資訊來判斷發行的 CA。憑證的 CA 必須是受信任的，系統才會接受該憑證進行驗證。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>WebServiceSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>MACResolverUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可執行媒體存取控制 (MAC) 解析之 Web 服務的 URL。MAC 解析包括取得連線之用戶端的 MAC 位址，然後再傳回該用戶端所連線之網路交換器的機架與連接埠號碼。增強型 9-1-1 服務會用 MAC 解析。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCSRKeySize</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>設定憑證簽署要求 (CSR) 金鑰的大小上限 (CSR 是從申請人傳送至 CA 的訊息，以便申請數位憑證)。可將 CSR 金鑰大小上限設為介於 1024 和 16384 位元組之間的任何整數值。預設值為 16384。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxGroupSizeToExpand</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>代表展開群組時要顯示之人員的數目上限。例如，如果 MaxGroupSizeToExpand 設為 75，每次展開群組時，只會顯示前 75 個群組成員。</p>
<p>MaxGroupSizeToExpand 可設為介於 1 和 1000 (含) 之間的任何整數值。預設值為 100。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxValidityPeriodHours</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>使用憑證驗證時，用戶端可要求憑證保持有效的時間 (單位為小時)。MaxValidityPeriodHours 代表用戶端可要求的時間長度上限。</p>
<p>MaxValidityPeriodHours 可以是介於 8 小時到 8760 小時 (365 天) 之間的任何整數值。預設值為 8760。</p></td>
</tr>
<tr class="even">
<td><p><em>MinCSRKeySize</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>設定憑證簽署要求 (CSR) 金鑰的大小下限 可將大小下限設為介於 1024 和 16384 位元組之間的任何整數值。預設值為 16384。</p></td>
</tr>
<tr class="odd">
<td><p><em>MinValidityPeriodHours</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>使用憑證驗證時，用戶端可要求憑證保持有效的時間 (單位為小時)。MinValidityPeriodHours 代表用戶端可要求的時間長度下限。</p>
<p>MinValidityPeriodHours 可以是介於 8 小時到 4320 小時 (180 天) 之間的任何整數值。預設值為 8。</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLocationSourceUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可處理位置要求的 Web 服務 URL。只有在本機無法解析位置要求時才會使用此服務。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowAlternateJoinOptionsExpanded</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數已被淘汰，無法再於內部部署版的 Lync Server 2013中使用。</p>
<p>此參數設為 True 時，就會自動展開參加線上會議 (例如 Office Communicator 2007 R2) 的其他選項，並且顯示給使用者。設為 False (預設值) 時，這些選項仍然可用，但使用者必須自行顯示選項清單。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDownloadCommunicatorAttendeeLink</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數已被淘汰，無法再於內部部署版的 Lync Server 2013中使用。</p>
<p>此參數若設為 True (預設值)，使用 Lync 以外之用戶端應用程式加入會議的使用者，將會看到一個指引他們下載 Lync Web App 的連結。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowJoinUsingLegacyClientLink</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數已被淘汰，無法再於內部部署版的 Lync Server 2013中使用。</p>
<p>此參數若設為 True，可讓使用 Lync 以外之用戶端應用程式加入會議的使用者，有機會使用目前的用戶端應用程式加入會議。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedCACerts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>受 Web 伺服器信任之憑證鏈結的憑證集合。新增到集合的新憑證必須使用 <strong>New-CsWebTrustedCACertificate</strong> Cmdlet 建立。</p>
<p>如果 InferCertChainFromSSL 屬性設為 True，則不會使用此集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCertificateAuth</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，可使用憑證來驗證用戶端。將此值設為 False 可停用憑證驗證。</p></td>
</tr>
<tr class="even">
<td><p><em>UseDomainAuthInLWA</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，就可以將網域驗證用來作為驗證 Lync Web App 使用者的方法。</p></td>
</tr>
<tr class="odd">
<td><p><em>UsePinAuth</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，會使用個人識別碼 (PIN) 驗證用戶端。將此值設為 False 可停用 PIN 驗證。</p></td>
</tr>
<tr class="even">
<td><p><em>UseWindowsAuth</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Web.UseWindowsAuth</p></td>
<td><p>決定如何 (以及是否) 使用 Windows 驗證來驗證使用者；亦即使用當使用者登入 Windows 時所使用的相同認證進行驗證。有效值為：</p>
<p>Negotiate - 用戶端與伺服器會共同運作，以決定適當的驗證通訊協定 (Kerberos 或 NTLM)。</p>
<p>NTLM – 允許 Windows 驗證，但僅使用 NTLM 通訊協定。</p>
<p>None – 不允許 Windows 驗證。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseWsFedPassiveAuth</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，可允許被動驗證：使用 URL 重新導向或智慧連結來驗證使用者。預設值為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="odd">
<td><p><em>WsFedPassiveMetadataUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>WS-同盟 Web 要求者通訊協定所用的 URI。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings 物件。 **Set-CsWebServiceConfiguration** Cmdlet 接受管線傳送的 Web 服務設定物件輸入。

## 傳回類型

**Set-CsWebServiceConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)


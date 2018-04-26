---
title: New-CsWebServiceConfiguration
TOCTitle: New-CsWebServiceConfiguration
ms:assetid: 6225cf8d-b669-464e-9848-a292953e3a3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398440(v=OCS.15)
ms:contentKeyID: 49291099
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2014-06-05_

建立新的 Web 服務組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsWebServiceConfiguration -Identity <XdsIdentity> [-AllowAnonymousAccessToLWAConference <$true | $false>] [-AllowExternalAuthentication <$true | $false>] [-AutoLaunchLyncWebAccess <$true | $false>] [-CASigningKeyLength <UInt64>] [-Confirm [<SwitchParameter>]] [-CrossDomainAuthorizationList <PSListModifier>] [-DefaultValidityPeriodHours <UInt64>] [-EnableCertChainDownload <$true | $false>] [-EnableGroupExpansion <$true | $false>] [-Force <SwitchParameter>] [-InferCertChainFromSSL <$true | $false>] [-InMemory <SwitchParameter>] [-MACResolverUrl <String>] [-MaxCSRKeySize <UInt64>] [-MaxGroupSizeToExpand <UInt32>] [-MaxValidityPeriodHours <UInt64>] [-MinCSRKeySize <UInt64>] [-MinValidityPeriodHours <UInt64>] [-SecondaryLocationSourceUrl <String>] [-ShowAlternateJoinOptionsExpanded <$true | $false>] [-ShowDownloadCommunicatorAttendeeLink <$true | $false>] [-ShowJoinUsingLegacyClientLink <$true | $false>] [-TrustedCACerts <PSListModifier>] [-UseCertificateAuth <$true | $false>] [-UseDomainAuthInLWA <$true | $false>] [-UsePinAuth <$true | $false>] [-UseWindowsAuth <None | Negotiate | NTLM>] [-UseWsFedPassiveAuth <$true | $false>] [-WhatIf [<SwitchParameter>]] [-WsFedPassiveMetadataUri <String>]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站 (-Identity site:Redmond) 建立新的 Web 服務組態設定集合。此範例包含兩個選用參數：一是 EnableGroupExpansion，此參數會設為 False ($False)；而另一個則是 UseCertificateAuth，此參數會設為 True ($True)。這兩個參數分別用於停用群組擴充，以及讓憑證能夠用於驗證。

請注意，如果已經建立用於 Redmond 網站的 Web 服務組態設定集合，則此命令會失敗。這是因為網站只能有一個 Web 服務組態設定集合的限制。

    New-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $False -UseCertificateAuth $True

## 範例 2

範例 2 是範例 1 所示命令的變化；不過在此範例中，新的 Web 服務組態設定集合一開始只會在記憶體中建立，之後才會套用到 Redmond 網站。為達成此目的，範例的第一個命令會使用 **New-CsWebServiceConfiguration** Cmdlet 建立 Redmond 網站的設定集合，並加入 InMemory 參數，確保此集合只會建立在記憶體中，而不會立即套用到 Redmond 網站 (因為設定只存於記憶體中，所以必須儲存在變數中；在此範例中，變數的名稱為 $x)。

範例中的命令 2 與命令 3 會取得這些虛擬組態設定，並修改 EnableGroupExpansion 和 UseCertificateAuth 屬性的值。在做出這些變更後，最後一個命令會使用 **Set-CsWebServiceConfiguration** Cmdlet，將這些虛擬設定套用到 Redmond 網站。如果您沒有呼叫 **Set-CsWebServiceConfiguration** Cmdlet，則不會將任何新的設定指派給網站。而且，一旦您終止 Windows PowerShell 工作階段或刪除變數 $x，虛擬的 Web 服務組態設定隨即會消失。

    $x = New-CsWebServiceConfiguration -Identity site:Redmond -InMemory
    $x.EnableGroupExpansion = $False 
    $x.UseCertificateAuth = $True
    Set-CsWebServiceConfiguration -Instance $x

## 範例 3

範例 3 所示的命令會將網域 http://fabrikam.com 新增至針對 Redmond 網站所建之新的 Web 服務組態設定集合的獲授權網域清單。為達成此目的，範例中的第一個命令使用 **New-CsWebOrigin** Cmdlet 建立 fabrikam.com 的網域物件。產生的網域物件儲存於名為 $x 的變數中。

範例中的第二個命令使用 **New-CsWebServiceConfiguration** Cmdlet，建立 Redmond 網站的 Web 服務組態設定。其中語法 – CrossDomainAuthorizationList $x 會將 http://fabrikam.com 新增至已獲授權可執行跨網域指令碼的網域集合。

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    New-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $x

## 範例 4

範例 4 顯示如何將多個已獲授權網域新增至新的 Web 服務組態設定集合。若要新增多個網域，您必須建立多個網域物件，並將各個物件儲存在不同的變數中。在範例 4 中，http://fabrikam.com 的網域物件是儲存在名為 $x 的變數中，http://contoso.com 的網域物件則是儲存在名為 $y 的變數中。

在建立所有的網域物件後，您只需在 CrossDomainAuthorizationList 參數的參數值中包含各個變數名稱。例如︰

–CrossDomainAuthorizationList $x, $y

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    $y = New-CsWebOrigin -Url "http://contoso.com"
    New-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $x, $y

## 詳細描述

許多 Lync Server 都是 Web 元件，會使用 Web 服務或網頁執行作業。例如，使用者利用 Web 服務搜尋通訊錄的新連絡人，或使用群組擴充來檢視通訊群組的個別成員。同樣地，從電話撥入式會議到 Lync Server都是使用網頁做為 Lync Server 和使用者之間的介面。

**CsWebServiceConfiguration** Cmdlet 可讓系統管理員管理整個組織的 Web 服務組態設定。包括管理群組擴充、憑證設定和容許的驗證方法。因為您可以在全域、網站和服務範圍設定不同的設定 (雖然僅適用於 Web Services 服務)，所以可以為不同的使用者和不同的位置自訂 Web 服務功能。

新的 Web 服務組態設定是使用 **New-CsWebServiceConfiguration** Cmdlet 所建立的。請注意，這些設定只能在網站範圍或服務範圍 (且僅適用於 Web Services 服務) 建立；如果您嘗試在全域範圍建立新集合，則命令會失敗。同樣的，如果您嘗試在網站範圍建立新的集合，例如在 Redmond 網站，而該網站已託管 Web 服務設定的集合，則命令會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsWebServiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWebServiceConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要建立之 Web 服務組態設定的唯一識別碼。若要建立在此網站範圍完成的設定，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要建立在此服務範圍設定的設定，請使用下列語法：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。請注意，在服務範圍建立的任何設定必須指派給 Web 伺服器服務。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowAnonymousAccessToLWAConference</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，允許匿名使用者參加 Lync Web App 會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalAuthentication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True (預設值)，可使用 OAuth 驗證來驗證外部使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>AutoLaunchLyncWebAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數已被淘汰，無法再於內部部署版的 Lync Server 2013中使用。</p>
<p>此參數設為 True 時，會自動使用 Lync Web App 來做為參加線上會議的預設 Web 快顯視窗，但需符合使用 Lync Web App 的先決條件 (例如，已安裝 Silverlight，而且 Internet Explorer 不會封鎖快顯視窗)。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>CASigningKeyLength</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>設定憑證授權單位 (CA) 簽署金鑰的大小；簽署金鑰是 CA 用來簽署數位憑證的私密金鑰。簽署金鑰的長度可設為介於 2048 到 16384 位元組之間的任何整數值，預設值為 2048。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>CrossDomainAuthorizationList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可主控會傳送跨網域指令碼要求至 Lync Server 2013 部署之 Web 應用程式的網域集合。</p>
<p>要新增至此清單的網域必須使用 New-CsWebOrigin Cmdlet 建立，然後新增至 Web 服務組態設定的新集合中。請注意，網域名稱的開頭也必須使用 http: 或 https: 前置詞。如需詳細資訊，請參閱此說明主題的範例 3。</p>
<p>此參數已在 Lync Server 2013 的 2013 年 2 月版本中導入。</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultValidityPeriodHours</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>使用憑證驗證時，用戶端可要求憑證保持有效的時間 (單位為小時)。DefaultValidityPeriodHours 代表如果用戶端不要求自訂有效期間，則憑證將維持有效的時間長度。</p>
<p>DefaultValidityPeriodHours 可以是介於 8 小時到 8760 小時 (365 天) 之間的任何整數值。預設值為 4320 (180 天)。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCertChainDownload</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，具有驗證憑證的伺服器將下載該憑證的憑證鏈結。憑證鏈結會追蹤個別憑證，一直追溯到發行的 CA。憑證的 CA 必須是受信任的，系統才會接受該憑證進行驗證。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableGroupExpansion</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數若設為 True，則將啟用 Lync Server 中的群組擴充。透過群組擴充，使用者可設定通訊群組做為連絡人，然後「擴充」該群組。當群組已擴充時，使用者便會看見群組所有的個別成員，以及目前的目前狀態資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InferCertChainFromSSL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，伺服器會使用安全通訊端層 (SSL) 通訊協定中包含的憑證資訊來判斷發行的 CA。憑證的 CA 必須是受信任的，系統才會接受該憑證進行驗證。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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
<td><p>設定憑證簽署要求 (CSR) 金鑰大小上限(CSR 是申請者為了申請數位憑證而傳送給 CA 的訊息)。可將大小上限設為介於 1024 和 16384 位元組之間的任何整數值。預設值為 16384。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxGroupSizeToExpand</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>代表當擴充群組時顯示的人數上限。例如，如果 MaxGroupSizeToExpand 設為 75，則任何時候擴充群組時，只會顯示群組的前 75 個成員。</p>
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
<td><p>設定 CSR 金鑰的大小下限。可將大小下限設為介於 1024 和 16384 位元組之間的任何整數值。預設值為 16384。</p></td>
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
<td><p>可處理位置要求的 Web 服務 URL。一般來說，只有在本機無法解析位置要求時才會使用這個服務。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowAlternateJoinOptionsExpanded</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數已被淘汰，無法再於內部部署版的 Lync Server 2013中使用。</p>
<p>此參數設為 True 時，就會自動擴充參加線上會議的其他選項 (例如 Office Communicator 2007 R2)，並且對使用者顯示。設為 False (預設值) 時，可使用這些選項，但使用者必須自行顯示選項清單。</p></td>
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
<td><p>設為 True (預設值) 時，會使用憑證驗證用戶端。將此值設為 False ($False) 可停用憑證驗證。</p></td>
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
<td><p>設為 True (預設值) 時，會使用個人識別碼 (PIN) 驗證用戶端。將此值設為 False ($False) 可停用 PIN 驗證。</p></td>
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

無。**New-CsWebServiceConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsWebServiceConfiguration** Cmdlet 會建立新的 Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)


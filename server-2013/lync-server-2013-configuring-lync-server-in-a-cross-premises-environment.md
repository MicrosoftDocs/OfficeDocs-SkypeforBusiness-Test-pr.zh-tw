---
title: 在跨單位環境中設定 Microsoft Lync Server 2013
TOCTitle: 在跨單位環境中設定 Microsoft Lync Server 2013
ms:assetid: 700639ec-5264-4449-a8a6-d7386fad8719
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204990(v=OCS.15)
ms:contentKeyID: 49291267
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在跨單位環境中設定 Microsoft Lync Server 2013

 

_**上次修改主題的時間：** 2014-02-05_

在跨部署 (Cross-Premise) 設定中，您的某些使用者會指派至 Microsoft Lync Server 2013 内部部署安裝，而其他使用者指派至 Lync Server 的 Office 365 版本。如要在跨部署環境中設定伺服器對伺服器驗證，您首必須先將 Lync Server 2013 内部部署安裝設定為信任的 Office 365 授權伺服器。藉由操作下列 Lync Server 管理命令介面指令碼，可執行本流程初始步驟：

    $TenantID = (Get-CsTenant -Filter {DisplayName -eq "Fabrikam.com"}).TenantId
    
    $sts = Get-CsOAuthServer microsoft.sts -ErrorAction SilentlyContinue
            
       if ($sts -eq $null)
          {
             New-CsOAuthServer microsoft.sts -MetadataUrl "https://accounts.accesscontrol.windows.net/$TenantId/metadata/json/1"
          }
       else
          {
             if ($sts.MetadataUrl -ne  "https://accounts.accesscontrol.windows.net/$TenantId/metadata/json/1")
                {
                   Remove-CsOAuthServer microsoft.sts
                   New-CsOAuthServer microsoft.sts -MetadataUrl "https://accounts.accesscontrol.windows.net/$TenantId/metadata/json/1"
                }
            }
    
    $exch = Get-CsPartnerApplication microsoft.exchange -ErrorAction SilentlyContinue
            
    if ($exch -eq $null)
       {
          New-CsPartnerApplication -Identity microsoft.exchange -ApplicationIdentifier 00000002-0000-0ff1-ce00-000000000000 -ApplicationTrustLevel Full -UseOAuthServer
        }
    else
        {
           if ($exch.ApplicationIdentifier -ne "00000002-0000-0ff1-ce00-000000000000")
              {
                 Remove-CsPartnerApplication microsoft.exchange
                 New-CsPartnerApplication -Identity microsoft.exchange -ApplicationIdentifier 00000002-0000-0ff1-ce00-000000000000 -ApplicationTrustLevel Full -UseOAuthServer 
              }
           else
              {
                 Set-CsPartnerApplication -Identity microsoft.exchange -ApplicationTrustLevel Full -UseOAuthServer
              }
       }
    
    Set-CsOAuthConfiguration -ServiceName 00000004-0000-0ff1-ce00-000000000000

請記住，租用戶的領域名稱通常和組織名稱不同；事實上，領域名稱和租用戶 ID 幾乎相同。因此，指令碼第一行是用來為指定的租用戶傳回 TenantId 屬性值 (在這種情況下為 fabrikam.com)，接著將該名稱指派至變數 $TenantId：

    $TenantID = (Get-CsTenant -DisplayName "Fabrikam.com").TenantId

完成指令碼後，接著您必須設定 Lync Server 2013 與授權伺服器之間的信任關係，以及設定 Exchange 2013 與授權伺服器之間的第二個信任關係。唯有使用 Microsoft Online Services Cmdlet 才能完成這項作業。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您尚未安裝 Microsoft Online Services Cmdlet，那麼，您必需先完成兩個動作才能繼續進行。首先，下載及安裝 Microsoft Online Services 登入小幫手 64 位元版本。完成安裝後，下載及安裝適用於 Windows PowerShell 的 Microsoft Online Services 模組 64 位元版本。您可以在 Office 365 網站找到有關安裝及使用 Microsoft Online Services 模組的詳細資訊。這些說明也將告訴您如何設定 Office 365 與 Active Directory 之間的單一登入、同盟與同步處理。<br />
如果您尚未安裝這些 Cmdlet，您的指令碼將會失敗，因為 Get-CsTenant Cmdlet 將無法使用。</td>
</tr>
</tbody>
</table>


完成 Office 365 設定並建立 Lync Server 2013 與 Exchange 2013 Office 365 服務主體後，接著您將需要藉由這些服務主體註冊您的認證。為了完成這項作業，您首先必須取得副檔名為 .CER 的 X.509 Base64 檔案。接著此憑證將會套用至 Office 365 服務主體。

當您取得 X.509 憑證後，請啟動 Microsoft Online Services 模組 (請依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Microsoft Online Services\]**，接著按一下 Windows PowerShell**\[Microsoft Online Services 模組\]** )。Services 模組啟動後，請鍵入以下內容，以匯入包含可用於管理服務主體之 Cmdlet 的 Microsoft Online Windows PowerShell 模組：

    Import-Module MSOnlineExtended

匯入模組後，請鍵入下列命令並按下 ENTER 鍵，以連線至 Office 365：

    Connect-MsolService

按下 ENTER 鍵後，將會出現認證對話方塊。請在對話方塊內輸入您的 Office 365 使用者名稱和密碼，然後按一下 \[確定\]。

一旦連線至 Office 365，您就可以執行下列命令以傳回有關服務主體的資訊：

    Get-MsolServicePrincipal

您能以類似的方式為所有服務主體取得資訊：

    ExtensionData        : System.Runtime.Serialization.ExtensionDataObject
    AccountEnabled       : True
    Addresses            : {}
    AppPrincipalId       : 00000004-0000-0ff1-ce00-000000000000
    DisplayName          : Microsoft Lync Server
    ObjectId             : aada5fbd-c0ae-442a-8c0b-36fec40602e2
    ServicePrincipalName : LyncServer/litwareinc.com
    TrustedForDelegation : True

下一個步驟為匯入、編碼以及指派 X.509 憑證。若要匯入及對憑證進行編碼，請使用下列 Windows PowerShell 命令，確認您叫用「匯入」方法時將完整的檔案路徑指定至 .CER 檔：

    $certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $certificate.Import("C:\Certificates\Office365.cer")
    $binaryValue = $certificate.GetRawCertData()
    $credentialsValue = [System.Convert]::ToBase64String($binaryValue)

憑證匯入且完成編碼後，接著您可以將憑證指派至 Office 365 服務主體。若要執行該動作，首先，請使用 Get-MsolServicePrincipal 擷取 Lync Server 與 Microsoft Exchange 服務主體的 AppPrincipalId 屬性值；AppPrincipalId 屬性值將會用來識別指派憑證的服務主體。藉由手邊的 Lync Server 2013 AppPrincipalId 屬性值，使用下列命令將憑證指派至 Lync Server Office 365 版本 (StartDate 與 EndDate 屬性應對應至憑證的有效期間)：

    New-MsolServicePrincipalCredential -AppPrincipalId 00000004-0000-0ff1-ce00-000000000000 -Type Asymmetric -Usage Verify -Value $credentialsValue -StartDate 6/1/2012 -EndDate 5/31/2013

接著，您必須重複命令，這次使用 Exchange 2013 的 AppPrincipalId 屬性值。

日後如需刪除該憑證，您可透過先擷取憑證的 KeyId 來完成作業：

    Get-MsolServicePrincipalCredential -AppPrincipalId 00000004-0000-0ff1-ce00-000000000000

該指令將會以這種方式傳回資料：

    Type      : Asymmetric
    Value     : 
    KeyId     : bc2795f3-2387-4543-a95d-f92c85c7a1b0
    StartDate : 6/1/2012 8:00:00 AM
    EndDate   : 5/31/2013 8:00:00 AM
    Usage     : Verify

接著您可以用類似這樣的命令來刪除憑證：

    Remove-MsolServicePrincipalCredential -AppPrincipalId 00000004-0000-0ff1-ce00-000000000000 -KeyId bc2795f3-2387-4543-a95d-f92c85c7a1b0

除了指派憑證，您也必須設定 Exchange Online 服務主體並將您的 Lync Server 2013 內部部署版本設定為 Office 365 服務主體。執行下列兩個命令即可完成該項作業：

    Set-MSOLServicePrincipal -AppPrincipalID 00000002-0000-0ff1-ce00-000000000000 -AccountEnabled $true
    
    $lyncSP = Get-MSOLServicePrincipal -AppPrincipalID 00000004-0000-0ff1-ce00-000000000000
    $lyncSP.ServicePrincipalNames.Add("00000004-0000-0ff1-ce00-000000000000/lync.contoso.com")
    Set-MSOLServicePrincipal -AppPrincipalID 00000004-0000-0ff1-ce00-000000000000 -ServicePrincipalNames $lyncSP.ServicePrincipalNames


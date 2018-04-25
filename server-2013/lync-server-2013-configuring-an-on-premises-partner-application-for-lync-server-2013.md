---
title: 設定 Microsoft Lync Server 2013 的內部部署夥伴應用程式
TOCTitle: 設定 Microsoft Lync Server 2013 的內部部署夥伴應用程式
ms:assetid: 696f2b26-e5d0-42b5-9785-a26c2ce25bb7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204975(v=OCS.15)
ms:contentKeyID: 49291199
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Microsoft Lync Server 2013 的內部部署夥伴應用程式

 

_**上次修改主題的時間：** 2013-02-04_

在您指派 OAuthTokenIssuer 憑證後，就必須設定 Microsoft Lync Server 2013 合作夥伴應用程式 (即將討論的程序可將 Microsoft Exchange Server 2013 和 Microsoft SharePoint 設定當做合作夥伴應用程式)。若要設定內部合作夥伴應用程式，您必須從將以下 Windows PowerShell 指令碼的程式碼複製到記事本 (或任何其他文字編輯器) 的動作開始：

    if ((Get-CsPartnerApplication -ErrorAction SilentlyContinue) -ne $Null)
       {
           Remove-CsPartnerApplication app
       }
    
    $exch = Get-CsPartnerApplication microsoft.exchange -ErrorAction SilentlyContinue
            
    if ($exch -eq $null)
       {
          New-CsPartnerApplication -Identity microsoft.exchange -MetadataUrl https://atl-exchange-001.litwareinc.com/autodiscover/metadata/json/1 -ApplicationTrustLevel Full 
        }
    else
        {
           if ($exch.ApplicationIdentifier -ne "00000002-0000-0ff1-ce00-000000000000")
              {
                 Remove-CsPartnerApplication microsoft.exchange
    New-CsPartnerApplication -Identity microsoft.exchange -MetadataUrl https://atl-exchange-001.litwareinc.com/autodiscover/metadata/json/1 -ApplicationTrustLevel Full 
               }
            else
               {
                 Set-CsPartnerApplication -Identity microsoft.exchange -ApplicationTrustLevel Full 
               }
         }
    
    $shp = Get-CsPartnerApplication microsoft.sharepoint -ErrorAction SilentlyContinue
            
    if ($shp -eq $null)
       {
          New-CsPartnerApplication -Identity microsoft.sharepoint -MetadataUrl http://atl-sharepoint-001.litwareinc.com/jsonmetadata.ashx -ApplicationTrustLevel Full 
        }
    else
        {
           if ($shp.ApplicationIdentifier -ne "00000003-0000-0ff1-ce00-000000000000")
              {
                 Remove-CsPartnerApplication microsoft.sharepoint
      
                 New-CsPartnerApplication -Identity microsoft.sharepoint -MetadataUrl http://atl-sharepoint-001.litwareinc.com/jsonmetadata.ashx -ApplicationTrustLevel Full 
               }
            else
               {
                 Set-CsPartnerApplication -Identity microsoft.sharepoint -ApplicationTrustLevel Full 
                }
       }
    
    Set-CsOAuthConfiguration -ServiceName 00000004-0000-0ff1-ce00-000000000000

在複製代碼後，請使用 .PS1 副檔名儲存指令碼 (例如 C:\\Scripts\\ServerToServerAuth.ps1)。請注意，在您執行此指令碼前，必須以 Exchange 2013 和 SharePoint 伺服器使用的中繼資料 URL 分別取代中繼資料 URL https://atl-exchange-001.litwareinc.com/autodiscover/metadata/json/1 和 http://atl-sharepoint-001.litwareinc.com/jsonmetadata.ashx。請參閱 Exchange 2013 和 SharePoint 的產品文件，以取得如何識別個別產品的中繼資料 URL 之相關資訊。

如果您注意指令碼的最後一行，就會發現是使用此語法來呼叫 Set-CsOAuthConfiguration Cmdlet ：

    Set-CsOAuthConfiguration -ServiceName 00000004-0000-0ff1-ce00-000000000000

因為呼叫 Set-CsOAuthConfiguration 時未使用 Realm 參數，所以領域會自動設為您組織的完整網域名稱 (FQDN) (例如 litwareinc.com)。如果您的領域名稱與組織名稱不同，就應包含領域名稱，方式如下：

    Set-CsOAuthConfiguration -ServiceName 00000004-0000-0ff1-ce00-000000000000 -Realm "contoso.com"

在進行這些變更後，您就可以執行指令碼，並從 Lync Server 2013 管理命令介面內部執行指令碼檔案，將 Exchange 2013 和 SharePoint 設定為合作夥伴應用程式。例如：

    C:\Scripts\ServerToServerAuth.ps1

請注意，即使您未安裝 Exchange 2013 和 SharePoint Server，也可以執行此指令碼；即使您未安裝 SharePoint Server，假設您將 SharePoint Server 設為合作夥伴應用程式，也不會發生問題。

當您執行此指令碼時，可能會收到如下的錯誤訊息：

    New-CsPartnerApplication : Cannot bind parameter 'MetadataUrl' to the target. Exception setting "MetadataUrl": "The metadata document could not be downloaded from the URL in the MetadataUrl parameter or downloaded data is not a valid metadata document."

此錯誤訊息通常代表發生下列兩種情況其中之一：1) 指令碼中其中一個指定的 URL 無效 (亦即，其中一個中繼資料 URL 並非實際的中繼資料 URL)；或 2) 無法連絡其中一個中繼資料 URL。如果發生這種情況，請驗證 URL 為正確且可存取，然後重新執行指令碼。

在建立 Lync Server 2013 的合作夥伴應用程式之後，您就必須將 Lync Server 設定為 Exchange 2013 的合作夥伴應用程式。您可以執行指令碼 Configure-EnterprisePartnerApplication.1 來設定 Exchange 2013 的協力廠商應用程式；只要為 Lync Server 指定中繼資料 URL 並指明 Lync Server 是新的協力廠商應用程式即可。

若要將 Lync Server 設為 Exchange 的協力廠商應用程式，請開啟 Exchange 管理命令介面，並執行如下的命令

    "c:\Program Files\Microsoft\Exchange Server\V15\Scripts\Configure-EnterprisePartnerApplication.ps1" -AuthMetadataUrl "https://lync.contoso.com/metadata/json/1" -ApplicationType "Lync"


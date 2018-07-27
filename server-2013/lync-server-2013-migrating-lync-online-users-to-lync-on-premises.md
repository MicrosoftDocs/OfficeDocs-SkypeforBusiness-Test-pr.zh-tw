---
title: 將 Lync Online 使用者移轉至 Lync 內部部署
TOCTitle: 將 Lync Online 使用者移轉至 Lync 內部部署
ms:assetid: 0e29605b-db2d-4cbf-b6a9-15db6b9fdabc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn689115(v=OCS.15)
ms:contentKeyID: 62247312
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Lync Online 使用者移轉至 Lync 內部部署

 

_**上次修改主題的時間：** 2015-03-09_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這些步驟僅適用於移轉在部署 Lync 內部部署前於 Lync Online 中原本為 Lync 啟用的使用者帳戶。若要移動原本為 Lync 內部部署啟用而稍後移至 Lync Online 的使用者，請參閱<a href="lync-server-2013-administering-users-in-a-hybrid-deployment.md">管理 Lync Server 2013 混合部署中的使用者</a>。<br />
此外，所有要移動的使用者都必須在內部部署的 Active Directory 中擁有帳戶。</td>
</tr>
</tbody>
</table>


## 將原本在 Lync Online 中啟用的使用者帳戶移轉至 Lync 內部部署

1.  首先，確認您的組織設為混合式部署。
    
      - 安裝 Windows Azure Active Directory Sync Tool。如需詳細資訊，請參閱 <http://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool.aspx>。
    
      - 若要讓您的使用者能夠針對 Lync Online 使用單一登入，請安裝 Active Directory Federation Services <http://social.technet.microsoft.com/wiki/contents/articles/1011.active-directory-federation-services-ad-fs-overview.aspx>。
    
      - 在您的內部部署中，於 Lync Server 管理命令介面輸入下列 Cmdlet，以建立 Lync Online 的主機服務提供者：
        
        ```
        Set-CSAccessEdgeConfiguration -AllowOutsideUsers 1 -AllowFederatedUsers 1 -UseDnsSrvRouting -EnablePartnerDiscovery $true
        ```
        ```
        New-CSHostingProvider -Identity LyncOnline -Name LyncOnlin -ProxyFqdn "sipfed.online.lync.com" -Enabled $true -EnabledSharedAddressSpace $true -HostsOCSUsers $true -VerificationLevel UseSourceVerification -IsLocal $false -AutodiscoverUrl https://webdir.online.lync.com/Autodiscover/AutodiscoverService.svc/root
        ```

2.  確認您在內部部署的 Edge Server 上有憑證鏈結可讓您連線至 Lync Online (如下表所示)。您可以在下列位置中下載此鏈結： [https://corp.sts.microsoft.com/Onboard/ADFS\_Onboarding\_Pack/corp\_sts\_certs.zip](https://corp.sts.microsoft.com/onboard/adfs_onboarding_pack/corp_sts_certs.zip)。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>憑證</th>
    <th>憑證存放區</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Baltimore CyberTrust Root</p></td>
    <td><p>可信任的根 CA</p></td>
    </tr>
    <tr class="even">
    <td><p>Microsoft 網際網路授權 (新 CA 憑證)</p></td>
    <td><p>中繼 CA</p></td>
    </tr>
    <tr class="odd">
    <td><p>MSIT 機器授權 CA2 (新發行 CA2)</p></td>
    <td><p>中繼 CA</p></td>
    </tr>
    </tbody>
    </table>


3.  在內部部署的 Active Directory 中，針對 Lync 內部部署啟用相關的使用者帳戶。若要針對個別使用者執行此動作，您可以輸入下列 Cmdlet：
    
        Enable-CsUser
        -Identity "username" 
        -SipAddress "sip: username@contoso.com"
        -HostingProviderProxyFqdn "sipfed.online.lync.com"
    
    或者，您也可以建立指令碼，從檔案中讀取使用者名稱並提供作為 Enable-CsUser Cmdlet 的輸入：
    
        Enable-CsUser
        -Identity $Identity 
        -SipAddress $SipAddress 
        -HostingProviderProxyFqdn "sipfed.online.lync.com"

4.  執行 DirSync 同步處理 Lync Online 使用者與更新的 Lync 內部部署使用者。

5.  更新部分 DNS 記錄，以將所有 SIP 流量導向至 Lync 內部部署：
    
      - 更新 **lyncdiscover.contoso.com** (指向內部部署反向 Proxy 伺服器之 FQDN 的記錄)
    
      - 更新 ***\_sip*.\_tls.contoso.com** (解析為 Lync 內部部署之 Access Edge Service 的公用 IP 或 VIP 位址的 SRV 記錄)
    
      - 更新 ***\_sipfederationtls*.\_tcp.contoso.com** (解析為 Lync 內部部署之 Access Edge Service 的公用 IP 或 VIP 位址的 SRV 記錄)
    
      - 如果您的組織使用的是分割 DNS (有時稱為「核心分割 DNS」)，請確認透過內部 DNS 區域解析名稱的使用者經導向至前端集區。

6.  輸入 `Get-CsUser` Cmdlet 以檢查要移動之使用者的部分屬性。您必須確認 HostingProviderProxyFQDN 設為 `"sipfed.online.lync.com"` 且該 SIP 位址的設定正確無誤。

7.  將 Lync Online 使用者移至 Lync 內部部署。
    
    若要移動單一使用者，請輸入：
    
    ```
    $cred = Get-Credential
    ```
    ```
    Move-CsUser -Identity <username>@contoso.com -Target "<fe-pool>.contoso.com" -Credential $cred -HostedMigrationOverrideURL <URL>
    ```
    
    若要移動多位使用者，請使用 **Get-CsUSer** Cmdlet 搭配 –Filter 參數，以選取具有特定屬性的使用者。舉例來說，若要選取所有 Lync Online 使用者，請使用下列篩選：{Hosting Provider –eq “sipfed.online.lync.om”}。接著，您可以將傳回的使用者結果輸送至 **Move-CsUSer** Cmdlet，如下所示。
    
        Get-CsUser -Filter {Hosting Provider -eq "sipfed.online.lync.com"} | Move-CsUser -Target "<fe-pool>.contoso.com" -Credential $creds -HostedMigrationOverrideURL <URL>
    
    為 **HostedMigrationOverrideUrl** 參數指定的 URL 格式必須是正在執行裝載移轉服務之集區的 URL，格式如下：*Https://\<集區 FQDN\>/HostedMigration/hostedmigrationService.svc*。
    
    您可以檢視 Office 365 租用戶帳戶的 Lync Online 控制台 URL，以判定裝載移轉服務的 URL。
    
    ## 決定 Office 365 租用戶的代管移轉服務 URL
    
    1.  以系統管理員身分登入 Office 365 租用戶。
    
    2.  開啟 \[Lync 系統管理中心\]。
    
    3.  顯示 \[Lync 系統管理中心\]之後，在位址列中選取並複製 URL **lync.com**。範例 URL 看起來應該像以下這樣：
        
        `https://webdir0a.online.lync.com/lscp/?language=en-US&tenantID=`
    
    4.  將 URL 中的 **webdir** 取代為 **admin**，產生下列結果：
        
        `https://admin0a.online.lync.com`
    
    5.  將下列字串附加至 URL：**/HostedMigration/hostedmigrationservice.svc**。
        
        產生的 URL (**HostedMigrationOverrideUrl** 的值) 應該如下所示：
        
        `https://admin0a.online.lync.com/HostedMigration/hostedmigrationservice.svc`
    
    > [!NOTE]  
    > rtcxds 資料庫之交易記錄檔的預設大小上限為 16 GB。如果您要一次移動大量的使用者，特別是有啟用鏡像時，空間可能會不夠。若要因應此問題，請提高檔案大小或定期備份記錄檔。如需詳細資訊，請參閱 <a href="http://support.microsoft.com/kb/2756725" class="uri">http://support.microsoft.com/kb/2756725</a>。
    


8.  這是選擇性步驟：如果您需要與 Exchange 2013 Online 整合，必須使用額外的主機服務提供者。如需詳細資料，請參閱 [設定內部部署 Lync Server 2013 與 Exchange Online 整合](lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md)。

9.  使用者現已移動完成。若要針對下表所示的屬性，檢查使用者是否擁有正確的屬性值，請輸入下列 Cmdlet：
    
        Get-CsUser | fl DisplayName,HostingProvider,SipAddress,Enabled
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Active Directory 屬性</th>
    <th>屬性名稱</th>
    <th>Lync Online 使用者的正確值</th>
    <th>Lync 內部部署使用者的正確值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>msRTCSIP-DeploymentLocator</p></td>
    <td><p>HostingProvider</p></td>
    <td><p>sipfed.online.lync.com</p></td>
    <td><p>SRV:</p></td>
    </tr>
    <tr class="even">
    <td><p>msRTCSIP-PrimaryUserAddress</p></td>
    <td><p>SIPAddress</p></td>
    <td><p>sip:userName@contoso.com</p></td>
    <td><p>sip:userName@contoso.com</p></td>
    </tr>
    <tr class="odd">
    <td><p>sRTCSIP-UserEnabled</p></td>
    <td><p>Enabled</p></td>
    <td><p>True</p></td>
    <td><p>True</p></td>
    </tr>
    </tbody>
    </table>


10. 已移動的各個使用者均必須先登出 Lync，然後重新登入。登入後，這些使用者應檢查其連絡人清單，然後視需要新增連絡人。
    
    請注意，排程的會議不會從 Lync Online 移轉至 Lync 內部部署。使用者在移動後必須重新排程這些會議。
    
    在 DNS 記錄更新完畢且所有使用者均導向至內部部署後，HostingProvider 屬性會將 Lync 使用者導向為使用 SRV 記錄或導向至線上提供者 “sipfed.online.lync.com”。


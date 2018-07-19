---
title: 設定 Lync Server 被動式驗證
TOCTitle: 設定 Lync Server 被動式驗證
ms:assetid: 9a904b8d-9fce-4abf-be73-5c8e48cfb53a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn308569(v=OCS.15)
ms:contentKeyID: 56269131
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 被動式驗證

 

_**上次修改主題的時間：** 2013-07-11_

下節說明如何設定具備累計更新 (2013 年 7 月) 的 Lync Server 2013 支援被動式驗證。啟用後，啟用了雙因素驗證的 Lync 使用者將需要使用實體或虛擬智慧卡和有效的 PIN，透過具備累計更新 (2013 年 7 月) 的 Lync 2013 用戶端登入。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們極力建議客戶於服務層級針對登錄器和 Web 服務啟用被動式驗證。如果於全域層級針對登錄器和 Web 服務啟用被動式驗證，可能導致未使用具備累計更新 (2013 年 7 月) 之 Lync 2013 桌面用戶端登入的使用者於整個組織發生驗證失敗情形。</td>
</tr>
</tbody>
</table>


## Web 服務組態

下列步驟說明如何為將啟用被動式驗證的 Director、Enterprise 集區和 Standard Edition 伺服器建立自訂 Web 服務組態。

**建立自訂 Web 服務組態**

1.  使用 Lync 系統管理員帳戶登入具備累計更新 (2013 年 7 月) 的 Lync Server 2013 Front End 伺服器。

2.  啟動 Lync Server 2013 管理命令介面。

3.  從 Lync Server 管理命令介面 命令列執行下列命令，為每個將啟用被動式驗證的 Director、Enterprise 集區和 Standard Edition 伺服器建立新的 Web 服務組態：
    
        new-cswebserviceconfiguration -Identity "Service:WebServer:LyncPool01.contoso.com" -UseWsFedPassiveAuth $true -WsFedPassiveMetadataUri https://dc.contoso.com/federationmetadata/2007-06/federationmetadata.xml
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>WsFedPassiveMetadataUri FQDN 的值為 AD FS 2.0 的 Federation Service 名稱。您可以在 AD FS 2.0 管理主控台上，從瀏覽窗格中在 <strong>[服務]</strong> 上按一下滑鼠右鍵，接著選取 <strong>[編輯 Federation Service 內容]</strong>，找出 Federation Service 名稱值。</td>
    </tr>
    </tbody>
    </table>


4.  執行下列命令，確認已正確設定 UseWsFedPassiveAuth 和 WsFedPassiveMetadataUri 值：
    
        Get-CsWebServiceConfiguration -identity "Service:WebServer:LyncPool01.contoso.com" | format-list UseWsFedPassiveAuth, WsFedPassiveMetadataUri

5.  對於用戶端而言，被動式驗證是最不建議使用的 WebTicket 驗證方法。對於所有將啟用被動式驗證的 Director、Enterprise 集區和 Standard Edition 伺服器，必須透過執行下列命令，於 Lync Web 服務中停用所有其他驗證類型：
    
        Set-CsWebServiceConfiguration -Identity "Service:WebServer:LyncPool01.contoso.com" -UseCertificateAuth $false -UsePinAuth $false -UseWindowsAuth NONE

6.  執行下列命令，確認所有其他驗證類型都已成功停用：
    
        Get-CsWebServiceConfiguration -Identity "Service:WebServer:LyncPool01.contoso.com" | format-list UseCertificateAuth, UsePinAuth, UseWindowsAuth

## Proxy 組態

當 Lync Web 服務的憑證驗證停用時，Lync 用戶端會使用較不常用的驗證類型 (例如 Kerberos 或 NTLM) 驗證登錄器服務。仍然需要憑證驗證，才能讓 Lync 用戶端擷取 WebTicket，然而，必須停用登錄器服務的 Kerberos 和 NTLM。

下列步驟說明如何為將啟用被動式驗證的 Edge 集區、Enterprise 集區和 Standard Edition 伺服器建立自訂 Proxy 組態。

**建立自訂 Proxy 組態**

1.  從 Lync Server 管理命令介面 命令列執行下列命令，為每個將啟用被動式驗證且具備累計更新 (2013 年 7 月) 的 Lync Server 2013 Edge 集區、Enterprise 集區和 Standard Edition 伺服器建立新的 Proxy 組態：
    
        New-CsProxyConfiguration -Identity "Service:EdgeServer:EdgePool01.contoso.com" 
        -UseKerberosForClientToProxyAuth $False -UseNtlmForClientToProxyAuth $False
    
        New-CsProxyConfiguration -Identity "Service:Registrar:LyncPool01.contoso.com" 
        -UseKerberosForClientToProxyAuth $False -UseNtlmForClientToProxyAuth $False

2.  執行下列命令，確認所有其他 Proxy 驗證類型都已成功停用：
    
        Get-CsProxyConfiguration -Identity "Service:Registrar:LyncPool01.contoso.com"
         | format-list UseKerberosForClientToProxyAuth, UseNtlmForClientToProxyAuth, UseCertifcateForClientToProxyAuth


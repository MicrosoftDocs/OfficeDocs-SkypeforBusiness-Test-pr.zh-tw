---
title: 設定 Microsoft SharePoint Server 2013 搜尋已封存的 Microsoft Lync Server 2013 資料
TOCTitle: 設定 Microsoft SharePoint Server 2013 搜尋已封存的 Microsoft Lync Server 2013 資料
ms:assetid: 17f49365-8778-4962-a41b-f96faf6902f1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687978(v=OCS.15)
ms:contentKeyID: 49889957
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Microsoft SharePoint Server 2013 搜尋已封存的 Microsoft Lync Server 2013 資料

 

_**上次修改主題的時間：** 2014-02-04_

將立即訊息和 Web 會議文字記錄儲存在 Microsoft Exchange Server 2013 而不儲存在 Microsoft Lync Server 2013 的主要優點之一，就是將資料儲存在相同位置可讓系統管理員使用單一工具來搜尋 Exchange 封存資料及/或 Lync Server 封存資料。由於所有資料都儲存在同一個地方 (Exchange)，因此可搜尋 Exchange 封存資料的任何工具也都可以搜尋 Lync Server 封存資料。

可讓您輕鬆搜尋封存資料的工具之一，就是 Microsoft SharePoint Server 2013。如果您想要使用 SharePoint 來搜尋 Lync Server 資料，必須先完成在 Lync Server 中設定 Exchange 封存的所有步驟。在 Exchange 2013 與 Lync Server 2013 成功整合之後，您必須將 Exchange Web Services Managed API 2.0 版安裝在 SharePoint Server 上；您可以從 Microsoft 下載中心下載該 API 的安裝程式 ([http://go.microsoft.com/fwlink/?linkid=258305\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=258305%26clcid=0x404))。下載的檔案 (EWSManagedAPI.msi) 可以儲存至 SharePoint Server 上的任何資料夾。

下載檔案之後，在 SharePoint Server 上完成下列程序：

1.  依序按一下 \[開始\]、\[所有程式\] 及 \[附屬應用程式\]，再以滑鼠右鍵按一下 \[命令提示字元\]，然後按一下 \[以系統管理員身分執行\]，以開啟命令視窗。

2.  在命令視窗中，使用 **cd** 命令將現行目錄切換至儲存 EWSManagedAPI.msi 檔案的資料夾。例如，如果您已將該檔案儲存至 C:\\Downloads，請在命令視窗中輸入下列命令，然後按 ENTER 鍵：
    
        cd C:\Downloads

3.  若要安裝 API，請輸入下列命令，然後按 ENTER 鍵：
    
        msiexec /I EwsManagedApi.msi addlocal="ExchangeWebServicesApi_Feature,ExchangeWebServicesApi_Gac"

4.  安裝 API 之後，輸入下列命令並按 ENTER 鍵，以重設 IIS：
    
        iisreset

安裝 Exchange Web Services 之後，您必須設定 SharePoint Server 2013 與 Exchange 2013 之間的伺服器對伺服器驗證。若要執行這項作業，請先開啟 SharePoint 2013 管理命令介面，並執行下列命令集：

    New-SPTrustedSecurityTokenIssuer -Name "Exchange" -MetadataEndPoint "https://autodiscover.litwareinc.com/autodiscover/metadata/json/1"
    $service = Get-SPSecurityTokenServiceConfig
    $service.HybridStsSelectionEnabled = $True
    $service.AllowMetadataOverHttp = $False
    $service.AllowOAuthOverHttp = $False
    $service.Update()

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請務必將該 URI 用於自動探索服務。不要使用範例 URI https://autodiscover.litwareinc.com/autodiscover/metadata/json/1。</td>
</tr>
</tbody>
</table>


在建立 Token 發行者以及設定 Token 服務之後，執行下列命令，請務必以 SharePoint 網站的 URL 來替代範例 URL http://atl-sharepoint-001：

    $exchange = Get-SPTrustedSecurityTokenIssuer "Exchange"
    $app = Get-SPAppPrincipal -Site "https://atl-sharepoint-001" -NameIdentifier $exchange.NameID
    $site = Get-SPSite  "https://atl-sharepoint-001"
    Set-SPAppPrincipalPermission -AppPrincipal $app -Site $site.RootWeb -Scope "SiteSubscription" -Right "FullControl" -EnableAppOnlyPolicy

若要設定 Exchange 2013 的伺服器對伺服器驗證，請開啟 Exchange 管理命令介面，並執行如下命令 (假設 Exchange 安裝在磁碟機 C:，且其使用預設資料夾路徑)：

    "C:\Program Files\Microsoft\Exchange Server\V15\Scripts\Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl 'https://atl-sharepoint-001/_layouts/15/metadata/json/1' -ApplicationType SharePoint"

設定夥伴應用程式之後，建議您在所有 Exchange 信箱及用戶端存取伺服器上停止並重新啟動 Internet Information Services (IIS)。您可以使用如下命令來重新啟動 IIS，其會在電腦 atl-exchange-001 上重新啟動該服務：

    iisreset atl-exchange-001

此命令可從 Exchange 管理命令介面或任何其他命令視窗中執行。

接著，執行如下命令，它會將在 Exchange 上執行探索的權限提供給指定的使用者 (在此範例中為 kenmyer)：

    Add-RoleGroupMember "Discovery Management" -Member "kenmyer"

在 Exchange 與 SharePoint 之間建立伺服器對伺服器驗證之後，下個步驟就是在 SharePoint 中建立 eDiscovery 網站。若要執行此作業，您可以從 SharePoint 管理命令介面執行如下命令：

    $template = Get-SPWebTemplate | Where-Object {$_.Title -eq "eDiscovery Center"}
    New-SPSite -Url "https://atl-sharepoint-001/sites/discovery" -OwnerAlias "kenmyer" -Template $Template -Name "Discovery Center"

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>&quot;eDiscovery&quot; 是 &quot;electronic discovery&quot; (電子化探索) 的縮寫，此程序通常是指在電子化封存中尋找可以在法庭上「合理計算以導出可採納證據」的項目。</td>
</tr>
</tbody>
</table>


當新網站準備好時，下個步驟就是設定 Exchange 2013 來做為 SharePoint 的結果來源。若要執行此作業，您可以從「SharePoint 2013 管理中心」頁面來完成下列程序：

1.  在「管理中心」頁面上，按一下 \[管理服務應用程式\]，然後按一下 \[Search Service 應用程式\]。

2.  在「Search Service 應用程式：搜尋管理」頁面上，按一下 \[結果來源\] ，然後按一下 \[新增結果來源\]。

3.  在 \[新增結果來源\] 窗格的 \[名稱\] 方塊中，輸入新結果來源的名稱 (例如，**Microsoft Exchange**)。選取 \[Exchange\] 做為結果來源 \[通訊協定\]，然後在 \[Exchange 來源 URL\] 方塊中輸入 Exchange Server 的 Web 服務來源 URL。來源 URL 看起來應該像下面這樣：
    
    https://atl-exchange-001.litwareinc.com/ews/exchange.asmx

4.  請確定未選取 \[使用自動探索\]，然後按一下 \[確定\]。

最後，從 SharePoint Discovery 網站 (例如，https://atl-sharepoint-001/sites/discovery) 完成下列程序，以建立新的 eDiscovery 案例及新的 eDiscovery 集：

1.  在「網站內容」頁面上，按一下 \[建立新案例\]。

2.  在「網站內容：建立 SharePoint 網站」頁面上的 \[標題\] 方塊中，輸入使用者的電子郵件別名 (例如，**kenmyer**)，然後將那相同的 URL 新增至 \[網站位址\] 方塊中。如此將會產生像下面這樣的 URL：
    
    https://atl-sharepoint-001/sites/eDiscovery/kenmyer

3.  按一下 \[建立\]。

4.  當「eDiscovery 集」頁面出現時，按一下 \[識別與保留: Discovery 集\] 底下的 \[新項目\]。

5.  在「新增：Discovery 集」頁面上的 \[Discovery 集名稱\] 方塊中，輸入使用者電子郵件別名。在 \[篩選\] 方塊中輸入 **eDiscovery Lync\***，然後按一下 \[新增及管理來源\]。

6.  在「新增及管理來源」頁面上 \[信箱\] 底下的第一個文字方塊中，輸入使用者的電子郵件別名。按一下位在文字方塊旁邊的檢查信箱圖示，確認 SharePoint 可以連線至指定的信箱。

7.  按一下 \[確定\]。

8.  在「eDiscovery 集」頁面上， 按一下 \[儲存\]，以儲存新的 eDiscovery 集。

此時，您可以搜尋指定的信箱 (kenmyer) 及/或啟用「就地保留」(In-Place Hold)，方法就和您用於任何其他 SharePoint 內容或結果來源一樣。


---
title: Lync Server 2013：IIS 組態
TOCTitle: IIS 組態
ms:assetid: b458babf-bf64-43f0-8a8e-612f5096b63c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412871(v=OCS.15)
ms:contentKeyID: 49292061
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 IIS 組態

 

_**上次修改主題的時間：** 2015-03-09_

若要成功完成此程序，您應該至少以本機系統管理員或網域使用者身分登入伺服器。

為 Lync Server 2013、 Standard Edition 或集區中的第一個 前端伺服器設定及安裝 前端伺服器之前，您會為 Internet Information Services (IIS) 安裝及設定伺服器角色和 Web 服務。

> [!IMPORTANT]  
> 如果您的組織要求您找到系統磁碟機以外之磁碟機上的 IIS 和所有 Web 服務，在一開始安裝 Lync Server 2013 系統管理工具時，您可以變更 [安裝程式] 對話方塊中的 Lync Server 2013 檔案的安裝位置路徑。安裝 IIS 前先安裝系統管理工具。如果您將安裝檔案 (包括 OCSCore.msi) 安裝到此路徑，其餘的 Lync Server 2013 檔案也會部署到此磁碟機。如需詳細資訊，請參閱＜ <a href="lync-server-2013-install-lync-server-administrative-tools.md">安裝 Lync Server 2013 系統管理工具</a>＞。如需安裝 IIS 時如何重新安置由 Windows 伺服器管理員部署的 INETPUB 的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=216888" class="uri">http://go.microsoft.com/fwlink/?linkid=216888</a>。



下表指出所需的 IIS 7.5 角色服務。

### IIS 7.5 角色服務

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色標題</th>
<th>角色服務</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>已安裝的一般 HTTP 功能</p></td>
<td><p>靜態內容</p></td>
</tr>
<tr class="even">
<td><p>已安裝的一般 HTTP 功能</p></td>
<td><p>預設文件</p></td>
</tr>
<tr class="odd">
<td><p>已安裝的一般 HTTP 功能</p></td>
<td><p>HTTP 錯誤</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>ASP.NET</p>
<p>Windows Server 2012 也需要 ASP.NET4.5</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>.NET 擴充性</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>網際網路伺服器 API (ISAPI) 延伸模組</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>ISAPI 篩選器</p></td>
</tr>
<tr class="even">
<td><p>健康情況及診斷</p></td>
<td><p>HTTP 記錄</p></td>
</tr>
<tr class="odd">
<td><p>健康情況及診斷</p></td>
<td><p>記錄工具</p></td>
</tr>
<tr class="even">
<td><p>健康情況及診斷</p></td>
<td><p>追蹤</p></td>
</tr>
<tr class="odd">
<td><p>安全性</p></td>
<td><p>匿名驗證 (預設會安裝並啟用)</p></td>
</tr>
<tr class="even">
<td><p>安全性</p></td>
<td><p>Windows 驗證</p></td>
</tr>
<tr class="odd">
<td><p>安全性</p></td>
<td><p>用戶端憑證對應驗證</p></td>
</tr>
<tr class="even">
<td><p>安全性</p></td>
<td><p>要求篩選</p></td>
</tr>
<tr class="odd">
<td><p>效能</p></td>
<td><p>靜態內容壓縮</p>
<p>動態內容壓縮</p></td>
</tr>
<tr class="even">
<td><p>管理工具</p></td>
<td><p>IIS 管理主控台</p></td>
</tr>
<tr class="odd">
<td><p>管理工具</p></td>
<td><p>IIS 管理指令碼及工具</p></td>
</tr>
</tbody>
</table>


在 Windows Server 2008 R2 SP1 x64 作業系統上，您可以使用 Windows PowerShell 2.0。您必須先匯入 ServerManager 模組，再安裝 IIS 7.5 角色和角色服務。

```
    Import-Module ServerManager
```
```
    Add-WindowsFeature Web-Server, Web-Static-Content, Web-Default-Doc, Web-Scripting-Tools, Web-Windows-Auth, Web-Asp-Net, Web-Log-Libraries, Web-Http-Tracing, Web-Stat-Compression, Web-Dyn-Compression, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Http-Errors, Web-Http-Logging, Web-Net-Ext, Web-Client-Auth, Web-Filtering, Web-Mgmt-Console
```

> [!NOTE]  
> 匿名驗證預設會與 IIS 伺服器角色一起安裝。您可以在安裝 IIS 之後管理匿名驗證。如需詳細資訊，請參閱＜啟用匿名驗證 (IIS 7)＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=203935" class="uri">http://go.microsoft.com/fwlink/?linkid=203935</a>。



下表指出 Windows Server 2012 與 Windows Server 2012 R2 所需的 IIS 8.0 和 IIS 8.5 角色服務。

> [!NOTE]  
> 針對 Windows Server 2012 與 Windows Server 2012 R2，Add-WindowsFeature Cmdlet 已由 Install-WindowsFeature Cmdlet 取代。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=392274">Install-WindowsFeature</a> (英文)。

### IIS 8.0 和 IIS 8.5 角色服務

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色標題</th>
<th>角色服務</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Web 伺服器 (IIS)</p></td>
<td><p>Web 伺服器</p></td>
</tr>
<tr class="even">
<td><p>一般 HTTP 功能</p></td>
<td><p>預設文件</p></td>
</tr>
<tr class="odd">
<td><p>一般 HTTP 功能</p></td>
<td><p>目錄瀏覽</p></td>
</tr>
<tr class="even">
<td><p>一般 HTTP 功能</p></td>
<td><p>HTTP 錯誤</p></td>
</tr>
<tr class="odd">
<td><p>一般 HTTP 功能</p></td>
<td><p>靜態內容</p></td>
</tr>
<tr class="even">
<td><p>一般 HTTP 功能</p></td>
<td><p>HTTP 重新導向</p></td>
</tr>
<tr class="odd">
<td><p>健康情況及診斷</p></td>
<td><p>HTTP 記錄</p></td>
</tr>
<tr class="even">
<td><p>健康情況及診斷</p></td>
<td><p>記錄工具</p></td>
</tr>
<tr class="odd">
<td><p>健康情況及診斷</p></td>
<td><p>要求監控</p></td>
</tr>
<tr class="even">
<td><p>健康情況及診斷</p></td>
<td><p>追蹤</p></td>
</tr>
<tr class="odd">
<td><p>安全性</p></td>
<td><p>要求篩選</p></td>
</tr>
<tr class="even">
<td><p>安全性</p></td>
<td><p>基本驗證</p></td>
</tr>
<tr class="odd">
<td><p>安全性</p></td>
<td><p>用戶端憑證對應驗證</p></td>
</tr>
<tr class="even">
<td><p>安全性</p></td>
<td><p>Windows 驗證</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>.Net 擴充性 3.5</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>.Net 擴充性 4.5</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>ASP.Net 3.5</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>ASP.Net 4.5</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>ISAPI 擴充程式</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>ISAPI 篩選器</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>伺服器端包含項目</p></td>
</tr>
<tr class="even">
<td><p>管理工具</p></td>
<td><p>IIS 管理主控台</p></td>
</tr>
<tr class="odd">
<td><p>管理工具</p></td>
<td><p>IIS 6 Metabase 相容性</p></td>
</tr>
<tr class="even">
<td><p>管理工具</p></td>
<td><p>IIS 管理指令碼及工具</p></td>
</tr>
<tr class="odd">
<td><p>.Net 3.5 Framework 功能</p></td>
<td><p>.Net 3.5 Framework</p></td>
</tr>
<tr class="even">
<td><p>.Net 4.5 Framework 功能</p></td>
<td><p>.Net Framework 4.5</p></td>
</tr>
<tr class="odd">
<td><p>.Net 4.5 Framework 功能</p></td>
<td><p>ASP.Net 4.5</p></td>
</tr>
<tr class="even">
<td><p>.Net 4.5 Framework 功能</p></td>
<td><p>HTTP 啟動</p></td>
</tr>
<tr class="odd">
<td><p>.Net 4.5 Framework 功能</p></td>
<td><p>TCP 連接埠共用</p></td>
</tr>
<tr class="even">
<td><p>背景智慧型傳送服務</p></td>
<td><p>IIS 伺服器擴充程式</p></td>
</tr>
<tr class="odd">
<td><p>筆跡和手寫輸入服務</p></td>
<td><p>筆跡和手寫輸入服務</p></td>
</tr>
<tr class="even">
<td><p>媒體基礎</p></td>
<td><p>媒體基礎</p></td>
</tr>
<tr class="odd">
<td><p>使用者介面與基礎結構</p></td>
<td><p>圖形管理工具與基礎結構</p></td>
</tr>
<tr class="even">
<td><p>使用者介面與基礎結構</p></td>
<td><p>桌面體驗</p></td>
</tr>
<tr class="odd">
<td><p>使用者介面與基礎結構</p></td>
<td><p>伺服器圖形化介面</p></td>
</tr>
<tr class="even">
<td><p>Windows Identity Foundation 3.5</p></td>
<td><p>Windows Identity Foundation 3.5</p></td>
</tr>
<tr class="odd">
<td><p>Windows 處理序啟用服務</p></td>
<td><p>處理序模型</p></td>
</tr>
<tr class="even">
<td><p>Windows 處理序啟用服務</p></td>
<td><p>組態 API</p></td>
</tr>
</tbody>
</table>


在 Windows Server 2012 與 Windows Server 2012 R2 中，您可以使用 Windows PowerShell 3.0 來安裝 IIS 需求。使用 Windows PowerShell 3.0 的 ServerManager 模組，輸入：

```
    Import-Module ServerManager
```
```
    Add-WindowsFeature Web-Server, Web-Static-Content, Web-Default-Doc, Web-Http-Errors, Web-Asp-Net, Web-Net-Ext, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Http-Logging, Web-Log-Libraries, Web-Request-Monitor, Web-Http-Tracing, Web-Basic-Auth, Web-Windows-Auth, Web-Client-Auth, Web-Filtering, Web-Stat-Compression, Web-Dyn-Compression, NET-Framework-45-Core, NET-WCF-HTTP-Activation45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Scripting-Tools, Web-Mgmt-Console, Web-Mgmt-Compat, Windows-Identity-Foundation, Server-Media-Foundation, BITS -Source D:\sources\sxs
```

> [!IMPORTANT]  
> Windows Server 2012 的新項目是 –Source 參數，用於定義 Windows Server 2012 來源媒體的位置。您可將媒體定義為 DVD 光碟機 (例如 D:\Sources\Sxs)，或是已將媒體檔案複製到其上的網路共用 (例如 \\fileserver\windows2012\sources\Sxs)。

## 請參閱

#### 概念

[Lync Server 2013 中的前端集區與 Standard Edition Server 的 IIS 需求](lync-server-2013-iis-requirements-for-front-end-pools-and-standard-edition-servers.md)


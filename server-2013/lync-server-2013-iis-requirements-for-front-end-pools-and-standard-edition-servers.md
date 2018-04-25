---
title: Lync Server 2013：前端集區與 Standard Edition Server 的 IIS 需求
TOCTitle: 前端集區與 Standard Edition Server 的 IIS 需求
ms:assetid: e8a6c7ac-b6d5-4c7e-abe9-d8ea5eedbc62
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399038(v=OCS.15)
ms:contentKeyID: 49292666
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的前端集區與 Standard Edition Server 的 IIS 需求

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 安裝程式會針對 Standard Edition Server、前端伺服器和 Directors，在 Internet Information Services (IIS) 中建立虛擬目錄，以達成下列目的：

  - 讓使用者能夠從通訊錄服務下載檔案

  - 讓用戶端取得更新

  - 啟用會議

  - 讓使用者下載會議內容

  - 讓使用者擴充通訊群組

  - 啟用電話會議

  - 啟用回應群組功能

此外，「 Lync Server 2010 的累計更新：2011 年 11 月」安裝程式會針對下列目的，在 IIS 中建立虛擬目錄：

  - 在 前端伺服器 或 Standard Edition Server 上，以支援行動裝置上的行動功能，例如立即訊息 (IM) 和目前狀態

  - 在 前端伺服器 或 Standard Edition Server 及 Director 上，讓行動裝置可自動探索行動性資源

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想部署行動性，建議您使用 IIS 7.5。 Lync Server Mobility Service 安裝程式會設定一些 ASP.NET 標幟以提升效能。預設會在 Windows Server 2008 R2 上安裝 IIS 7.5，且 Mobility Service 安裝程式會自動變更 ASP.NET 設定。如果您在 Windows Server 2008 上使用 IIS 7.0，則需要手動變更這些設定。</td>
</tr>
</tbody>
</table>


Lync Server 需要安裝下列 IIS 模組：

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的組織要求您找到系統磁碟機以外之磁碟機上的 IIS 和所有 Web 服務，您可以變更安裝程式對話方塊中 Lync Server 檔案的安裝位置路徑。如果您將安裝檔案 (包括 OCSCore.msi) 安裝到此路徑，其餘的 Lync Server 檔案也會部署到此磁碟機。如需安裝 IIS 時如何重新安置由 Windows 伺服器管理員部署的 INETPUB 的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=216888%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=216888&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


  - 靜態內容

  - 預設文件

  - HTTP 錯誤

  - ASP.NET

  - .NET 擴充性

  - 網際網路伺服器 API (ISAPI) 延伸模組

  - ISAPI 篩選器

  - HTTP 記錄

  - 記錄工具

  - 追蹤

  - Windows 驗證

  - 要求篩選

  - 靜態內容壓縮

  - 動態內容壓縮

  - IIS 管理主控台

  - IIS 管理指令碼及工具

  - 匿名驗證 (在安裝 IIS 時依預設安裝)

  - 用戶端憑證對應驗證

下表列出內部存取之虛擬目錄的 URI 和其代表的檔案系統資源。

### 內部存取的虛擬目錄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>虛擬目錄 URI</th>
<th>代表</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Address Book Server</p></td>
<td><p>https://<em>&lt;Internal FQDN&gt;</em>/ABS/int/Handler</p></td>
<td><p>供內部使用者存取的 Address Book Server 下載檔案所在位置。</p></td>
</tr>
<tr class="even">
<td><p>自動探索服務</p></td>
<td><p>https://<em>&lt;Internal FQDN&gt;</em>/Autodiscover</p></td>
<td><p>尋找內部行動裝置使用者的行動性資源之 Lync Server 自動探索服務的位置。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端更新</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/AutoUpdate/Int</p></td>
<td><p>供內部電腦用戶端存取的更新檔所在位置。</p></td>
</tr>
<tr class="even">
<td><p>會議</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/Conf/Int</p></td>
<td><p>供內部使用者存取的會議資源所在位置。</p></td>
</tr>
<tr class="odd">
<td><p>裝置更新</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/DeviceUpdateFiles_Int</p></td>
<td><p>供內部 UC 裝置存取的整合通訊 (UC) 裝置更新檔所在位置。</p></td>
</tr>
<tr class="even">
<td><p>會議</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/etc/place/null</p></td>
<td><p>供內部使用者存取之會議內容的所在位置。</p></td>
</tr>
<tr class="odd">
<td><p>Mobility Service</p></td>
<td><p>https://<em>&lt;Internal FQDN&gt;</em>/Mcx</p></td>
<td><p>供內部行動裝置使用者存取的 Mobility Service 資源所在位置。</p></td>
</tr>
<tr class="even">
<td><p>群組擴充和通訊錄 Web 查詢服務</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/GroupExpansion/int/service.asmx</p></td>
<td><p>讓內部使用者能擴充群組的 Web 服務所在位置。同樣也是通訊錄 Web 查詢服務所在位置，該服務會提供全域通訊清單資訊給內部 Lync MobileMicrosoft Lync 2010 Mobile 用戶端。</p></td>
</tr>
<tr class="odd">
<td><p>電話會議</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/PhoneConferencing/Int</p></td>
<td><p>供內部使用者存取之電話會議資料所在位置。</p></td>
</tr>
<tr class="even">
<td><p>裝置更新</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/RequestHandler</p></td>
<td><p>裝置更新 Web 服務要求處理常式所在位置，該要求處理常式會讓內部 UC 裝置上傳記錄並檢查更新。</p></td>
</tr>
<tr class="odd">
<td><p>回應群組應用程式</p></td>
<td><p>http://<em>&lt;Internal FQDN&gt;</em>/RgsConfig</p>
<p>http://<em>&lt;Internal FQDN&gt;</em>/RgsClients</p></td>
<td><p>回應群組設定工具所在位置。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於合併設定中的 前端集區，您必須先部署 IIS 才能在集區中新增伺服器。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />安全性 附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用 IIS 系統管理嵌入式管理單元，來指派 IIS Web 元件伺服器所使用的憑證。</td>
</tr>
</tbody>
</table>


---
title: 安裝 Lync Server 2013 監控報告
TOCTitle: 安裝 Lync Server 2013 監控報告
ms:assetid: 6f417569-b100-442c-ad48-fdd794626cf7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204989(v=OCS.15)
ms:contentKeyID: 49291252
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 監控報告

 

_**上次修改主題的時間：** 2015-03-09_

Microsoft Lync Server 2013 監控報告可提供您有關組織中通訊工作階段品質及數量的豐富資訊。但是，在安裝 Lync Server 2013 時，監控報告並不會自動安裝；相反地，您必須個別安裝監控報告，而且只能在將 Lync Server 安裝於電腦後進行。

> [!NOTE]  
> 建議您將監控報告安裝在已安裝監控資料庫之相同電腦上，如此可簡化存取報告的指派權限程序：將監控報告安裝在裝載監控存放區的電腦上，表示您不需要設定權限以允許某一台電腦上的資料庫與在第二台電腦執行的 Reporting Services 進行互動。



Lync Server 監控報告涵蓋超過 30 項報告，旨在提供有關會議、對等 IM 工作階段、使用者註冊、回應群組應用程式等其他更多的詳細資訊。在 2013 版本中，Lync Server 監控報告包含了幾項強化功能：

  - **新的語音品質報告**。這些新的報告內容包含：[Lync Server 2013 中的媒體品質比較報表](lync-server-2013-media-quality-comparison-report.md)，可比較不同通話類型之間的品質 (例如，有線通話與無線通話之間)；以及[會議加入時間報表](lync-server-2013-conference-join-time-report.md)，則可提供使用者加入會議所需時間長度的相關資訊。

  - **針對視訊與應用程式共用工作階段進行分析和疑難排解的改善報告。** [Lync Server 2013 中的媒體品質摘要報告](lync-server-2013-media-quality-summary-report.md) 可提供分析視訊與應用程式共用通話的方法，而[Lync Server 2013 中的伺服器效能報告](lync-server-2013-server-performance-report.md)，則詳述伺服器產生這些通話的效能。[Lync Server 2013 中的對等工作階段詳細資料報告](lync-server-2013-peer-to-peer-session-detail-report.md)及[會議詳細資料報告](lync-server-2013-conference-detail-report.md)現在也提供視訊與應用程式共用計量的報告。

  - **改善報告效能**。包括加速回應與資料擷取時間，以及更迅速而簡便瀏覽報告。

有關個別報告的詳細資訊，可在監控報告文件中取得。

> [!NOTE]  
> 還有一個新報告，也就是 QoE 詳細通話子報表，包含於 Lync Server 2013。但是，此報告主要用於內部，無法直接存取。



有兩種方法可安裝 Lync Server 監控報告：您可使用 Lync Server 部署精靈或 Lync Server 2013 安裝檔案中包含的 Windows PowerShell 指令碼。無論您使用哪一種方法安裝報告，都必須先確認您具備下列條件：

  - 具備將資料庫角色新增至監控資料庫中使用者帳戶的權限。

  - 在 SQL Server Reporting Services 中具有「內容管理員」角色。這個角色會賦予您將報告部署至 SQL Server Reporting Services 的權限。

若要使用部署精靈安裝監控報告，請完成下列步驟：

1.  依序按一下**\[開始\]**、**\[所有程式\]**、**\[Microsoft Lync Server 2013\]**，然後按一下 **\[Lync Server 部署精靈\]**。

2.  在部署精靈中按一下 **\[部署監控報告\]** 以啟動「部署監控報告」精靈。

3.  在部署監控報告精靈中的 **\[指定監控資料庫\]** 頁面上，請確認裝載您監控存放區之電腦的完整網域名稱顯示於 **\[監控資料庫\]** 下拉式清單中。(如果您有多個監控存放區，則必須從下拉式清單選取適當的伺服器。) 確認正確的 SQL Server 執行個體顯示於 **\[SQL Server Reporting Services (SSRS) 執行個體\]** 方塊中 (例如 **atl-sql-001.litwareinc.com/archinst**)，然後按 **\[下一步\]**。

4.  在 **\[指定認證\]** 頁面的 **\[使用者名稱\]** 方塊中，輸入網域名稱及存取監控報告之時所使用的帳戶使用者名稱 (例如 **litwareinc\\kenmyer**)。如果不使用此格式 (網域\\使用者名稱)，將會發生錯誤。
    
    在 **\[密碼\]** 方塊中輸入使用者帳戶密碼，然後按 **\[下一步\]**。請留意，此帳戶不需要任何特殊權限。設定完成時，將會自動授予帳戶所需的登入和資料庫權限。

5.  在 **\[指定唯讀群組\]** 頁面上的使用者群組方塊中，輸入將授與 SQL Server Reporting Services 唯讀存取權的安全性群組名稱。例如，若要指定唯讀系統管理員存取報告，請輸入 **RTCUniversalReadOnlyAdmins**，然後按 **\[下一步\]**。

6.  在 **\[執行命令\]** 頁面上按一下 **\[完成\]**。

亦可透過執行指令碼 DeployReports.ps1 從 Lync Server 管理命令介面安裝監控報告；此 Windows PowerShell 指令碼可見於 \\Setup\\ReportingSetup 資料夾中的 Lync Server 安裝媒體。若要使用 DeployReports.ps1 安裝監控報告，請在管理介面提示中輸入類似下列命令：

    D:\Setup\AMD64\Setp\ReportingSetup\DeployReports.ps1 -storedUserName "litwareinc\kenmyer" -storedPassword "p@ssw0rd" -readOnlyGroupName "RTCUniversalReadOnlyAdmins" -reportServerSqlInstance "atl-sql-001.litwareinc.com" -monitoringDatabaseId "MonitoringDatabase:atl-sql-001.litwareinc.com"

用於以上命令的參數會在下表加以說明：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數名稱</th>
<th>必要</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>storedUserName</p></td>
<td><p>是</p></td>
<td><p>用於存取監控存放區的使用者帳戶 (格式為網域\使用者名稱)；例如：</p>
<pre><code>-storedUserName &quot;litwareinc\kenmyer&quot;</code></pre>
<p>此帳戶必須具有先前指定的 SQL Server 及 SQL Server Reporting Services 權限，否則指令碼將會失敗。</p></td>
</tr>
<tr class="even">
<td><p>storedPassword</p></td>
<td><p>是</p></td>
<td><p>用於存取監控存放區的使用者帳戶密碼。</p></td>
</tr>
<tr class="odd">
<td><p>readOnlyGroupName</p></td>
<td><p>否</p></td>
<td><p>授與成員監控報告唯讀權限的網域或本機安全性群組。請注意，如果指定的群組不存在，指令碼就會失效。如果您稍後決定撤銷這些權限，或是決定將權限授與其他使用者或群組，可使用 SQL Service Reporting Services 報表管理員執行這些動作。</p></td>
</tr>
<tr class="even">
<td><p>reportSqlServerInstance</p></td>
<td><p>否</p></td>
<td><p>託管 Reporting Service 的 SQL Server 執行個體。必須使用 Report Server 的完整網域名稱指定報告執行個體；例如：</p>
<pre><code>-reportServerSqlInstance atl-sql-001.litwareinc.com</code></pre>
<p>如果不包含此參數，指令碼會假定 Reporting Services 由託管監控資料庫之相同的 SQL Server 執行個體託管。</p></td>
</tr>
<tr class="odd">
<td><p>monitoringDatabaseId</p></td>
<td><p>否</p></td>
<td><p>監控資料庫的服務識別。您可執行此命令返回監控資料庫的識別：</p>
<pre><code>Get-CsService -MonitoringDatabase</code></pre></td>
</tr>
</tbody>
</table>


安裝監控報告之後，您必須接著使用 Set-CsReportingConfiguration Cmdlet 以設定用於存取這些報告的 URL。這項工作可透過執行下列 Windows PowerShell 命令從 Lync Server 管理命令介面進行。請注意，建議您在設定報告 URL 時使用 HTTPS 通訊協定 (非必要)：

    Set-CsReportingConfiguration -Identity "MonitoringDatabase:atl-sql-001.litwareinc.com" -ReportingURL "https://atl-sql-001.litwareinc.com:443/Reports_ARCHINST"

以上的命令中，ReportingUrl 屬性應設為 SQL Server 2008 R2 Reporting Services 所使用的報表管理員 URL。您可在已安裝 SQL Server Reporting Services 的電腦上透過完成下列步驟來決定報表管理員 URL：

1.  依序按一下 \[開始\]、\[所有程式\]、\[Microsoft SQL Server 2008 R2\]、\[組態工具\]，然後按一下 \[Reporting Services 組態管理員\]。

2.  在 \[Reporting Services 組態連接\] 對話方塊中，請確定 Reporting Services 電腦名稱顯示於 \[伺服器名稱\] 對話方塊中。從 \[報告伺服器執行個體\] 下拉式清單中選取 SQL Server 執行個體，然後按一下 \[連線\]。

3.  在 \[Reporting Services 組態管理員\] 中，按一下 \[報表管理員 URL\]，\[報表管理員 URL\] 窗格應該會顯示一個以上的 URL。雖然其中任何 URL 皆可作為報告 URL 之用，再一次申明，建議您採用使用 HTTPS 通訊協定的 ReportingUrl 。

如果您已為監控資料庫設定了鏡像資料庫，則您也必須將監控報告與鏡像資料庫建立關聯。請參閱文章＜[將監視報告與鏡像資料庫相關聯](lync-server-2013-associating-monitoring-reports-with-a-mirror-database.md)＞以取得詳細資料。


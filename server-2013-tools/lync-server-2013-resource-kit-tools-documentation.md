---
title: Lync Server 2013 Resource Kit 工具文件
TOCTitle: Lync Server 2013 Resource Kit 工具文件
ms:assetid: b1c341f1-86fa-479d-ba4d-28df5a4c1622
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945604(v=OCS.15)
ms:contentKeyID: 52056019
ms.date: 09/30/2014
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 Resource Kit 工具文件

 

_**上次修改主題的時間：** 2014-01-09_

本主題說明 Lync Server 2013 Resource Kit 的內含工具，包括各項工具的用途以及其使用範例。Lync Server 2013 Resource Kit 工具 可協助負責部署與管理 Lync Server 2013 的 IT 系統管理員簡化例行工作。舉例來說，**Web Conf Data** 工具可用於輕鬆控管使用者在線上會議中所上傳的資料。**SEFAUtil** 工具則可用於為使用者設定委派來電轉接與接聽。建議 IT 系統管理員利用這些工具更加有效地管理 Lync Server 2013。

## 安裝 Resource Kit 工具

若要安裝 Lync Server 2013 Resource Kit 工具，請下載 **OCSReskit.msi**。您可以從下載中心下載 Resource Kit 工具安裝程式：[http://go.microsoft.com/fwlink/p/?LinkID=330429](http://go.microsoft.com/fwlink/p/?linkid=330429))。

執行 **OCSResKit.msi** 以進行簡易安裝。.msi 會在下列路徑中安裝所有工具：**%Program Files%\\Microsoft Lync Server 2013\\ResKit**。若工具為自封式可執行檔，則會位於此資料夾；另有包含檔案的工具則會位於其自身的子資料夾。

## 受支援的環境

為求最佳效能，Lync Server 2013 Resource Kit 工具 應與 Lync Server 2013 安裝於相同的環境，且所需規格也應相同。

## Resource Kit 工具概觀

下列清單說明在 Lync Server 2013 Resource Kit 中所提供的工具。各項工具的說明 (包括需求與使用範例) 則涵蓋於下列章節。

  - ABSConfig

  - Bandwidth Policy Service Monitor

  - Bandwidth Utilization Analyzer

  - Call Parkometer

  - CleanupStorageServiceData

  - DBAnalyze

  - ImportStorageServiceData

  - LCSSync

  - LookupUserConsole

  - MsTurnPing

  - Network Configuration Viewer

  - Response Group Agent Live

  - SEFAUtil

  - SYSPrep.ps1

  - Unassigned Number Announcements Migration

  - Web Conf Data

## ABSConfig

通訊錄服務設定工具 (ABSConfig) 乃是一項系統管理工具，有助系統管理員自訂 Lync Server 2013 中的通訊錄服務設定。這項工具亦可讓 Lync Server 2013 系統管理員還原預設的通訊錄服務設定。

## 說明

ABSConfig 乃是圖形化使用者介面應用程式，能夠讓系統管理員設定與通訊錄服務相關的 Active Directory 網域服務 屬性。

這項工具的主要使用案例如下：

  - 讓系統管理員將 Active Directory 網域服務中的屬性對應至 Lync Server 2013 的屬性。

  - 讓系統管理員指定要在通訊錄服務檔案中納入或排除的 Active Directory 網域服務屬性。

  - 讓系統管理員還原預設的通訊錄服務設定。

透過 absConfig.exe 檔案可以啟動 ABSConfig 工具。這項工具會開啟至 **\[設定屬性\]** 索引標籤。此表格提供選項將 Active Directory 網域服務屬性對應至 Lync Server 2013 的屬性欄位，並根據特定屬性篩選器指定要在通訊錄服務檔案中納入或排除的使用者。另外亦提供選項自訂要在通訊錄檔案中納入的電話號碼值。**\[還原預設值\]** 選項則可讓系統管理員將通訊錄服務設定還原至預設值。

## 與 Lync Server 2010 的差異

在 Lync Server 2013 ABS 設定工具中，取消核取屬性的「啟用」核取方塊即可移除該屬性 (列)。這項操作與在 Lync Server 2010 中刪除屬性列的效果相同。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>「啟用」核取方塊位於最右方的欄位；您可能需要向右捲動才可顯示該欄位</td>
</tr>
</tbody>
</table>


## 輸出

ABSConfig 會將通訊錄服務設定儲存於資料庫中。

    Path: %ProgramFiles%\Microsoft Lync Server 2013\Reskit

## 用途

使用 ABSConfig 即可快速簡便地自訂 Lync Server 2013 通訊錄服務。

## 需求

## 電腦

只有已加入網域並安裝 Lync Server 2013 的電腦才可執行 ABSConfig。如為 Lync Server 2013 Enterprise Edition，在安裝期間啟用通訊錄服務的任何前端伺服器均可執行此工具。

## 網路

電腦應該要能夠連線至前端集區與後端資料庫。

## 軟體

執行 ABSConfig 工具前，必須安裝下列軟體元件：

  - Microsoft Lync Server 2013

## 使用者

擁有權限可以更新 Lync Server 2013 部署的系統管理員。

## 範例

在命令提示字元中輸入 **ABSConfig.exe** 即可啟動 ABSConfig。以下所示為 ABSConfig 工具使用者介面。

![ABSConfig.exe 工具。](images/JJ945604.6fb63a70-7b63-4b8b-b7d1-82fe9aa2028f(OCS.15).jpg "ABSConfig.exe 工具。")

## 總結

ABSConfig 工具可讓系統管理員快速簡便地利用工具自訂 Lync Server 2013 通訊錄服務。

## Bandwidth Policy Service Monitor

Bandwidth Policy Service Monitor 工具旨在讓系統管理員得以檢視以下所列項目：

1.  拓撲中所有已設定的 Lync Server 2013 頻寬原則服務 (驗證與核心)

2.  各服務與其他頻寬原則服務以及 Edge Server 的連線

3.  網路設定文件中所設定的所有連結以及各頻寬原則服務所報告的即時頻寬使用量

## 說明

Bandwidth Policy Service Monitor 工具乃是 GUI 應用程式。系統管理員執行 PDPMonUI.exe 即可啟動此工具。

工具啟動後，會嘗試探索拓撲中的頻寬原則服務清單。初始更新完成後，視窗的左側窗格會填入依照所屬叢集分組的服務清單。

系統管理員選取特定頻寬原則服務後，右側窗格即會顯示該特定服務的相關資訊。該窗格另有顯示相關資訊的兩個主要索引標籤。

## \[機器資訊\] 索引標籤

**\[機器資訊\]** 索引標籤會顯示所選頻寬原則服務的詳細資訊以及所選頻寬原則服務與其他服務之所有連線的清單與狀態。

## \[拓撲資訊\] 索引標籤

**\[拓撲資訊\]** 索引標籤會顯示在網路設定中所設定的所有連結清單。畫面不僅會顯示各個連結的音訊與視訊頻寬容量，另外也會同時以 KB 與容量百分比的形式顯示目前使用的頻寬。這項工具會利用色彩編碼醒目提示使用量逼近容量的連結，讓系統管理員得以快速找出該類連結。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是 Bandwidth Policy Service Monitor 工具在連線至任何已設定的頻寬原則服務時發生失敗，<strong>[機器資訊]</strong> 與 <strong>[拓撲資訊]</strong> 索引標籤就不會填入任何資訊。然而，也有可能工具在開始時能夠連線至服務，而後又失去連線。在這種情況下，系統管理員所看到的可能是過期的資訊。各個索引標籤中所顯示的<strong>上次更新</strong>時間戳記可讓系統管理員瞭解特定頻寬原則服務上次所更新的時間。</td>
</tr>
</tbody>
</table>


## 輸出

沒有命令列輸出；程式輸出會包含在主要圖形化使用者介面 (GUI) 中。

## 用途

Bandwidth Policy Service Monitor 工具的用途在於讓系統管理員得以查看拓撲中所定義之各項頻寬原則服務的狀態。此外，系統管理員亦可查看網路設定文件中所定義之所有連結的即時頻寬使用量。

## 需求

執行 Bandwidth Policy Service Monitor 工具的電腦必須為 Lync Server 拓撲中的一部分。

## 總結

Bandwidth Policy Service Monitor 工具不僅可讓系統管理員檢查拓撲中所有頻寬原則服務的狀態，更重要的是，還可讓系統管理員取得網路設定中所定義之連結的即時頻寬使用量。

## Bandwidth Utilization Analyzer

Bandwidth Utilization Analyzer 乃是可針對企業網路中 WAN 連結之 UC 端點頻寬使用量的各種檢視畫面建立相關報告的工具。這些報告可用於瞭解目前的頻寬使用量模式並有助於頻寬容量規劃。

## 說明

Bandwidth Utilization Analyzer 會建置為 GUI 應用程式。這項工具會特別針對整個網路的音訊使用量而產生報告，進而協助容量規劃。這項工具亦會逐一查看指派至各個連結的頻寬容量。

## 輸出

Bandwidth Utilization Analyzer 會針對系統中所設定之所有 WAN 連結提供頻寬容量與使用量的圖形化繪圖。

## 用途

無論採用何種語音與視訊部署，都必須監視並瞭解整個企業網路之媒體流量的頻寬使用量趨勢，而 Bandwidth Utilization Analyzer 工具正好可讓系統管理員達成此一目標。這項工具所能執行的工作如下：

  - 針對整個網路的音訊使用量產生特定報告

  - 協助高效執行容量規劃並逐一查看指派至各個連結的頻寬容量

Bandwidth Utilization Analyzer 可產生頻寬容量與使用量報告的圖形化繪圖；內容如下：

  - 企業網路中的所有 WAN 連結

  - 依選取的 WAN 連結進行篩選

  - 依超過連結容量的 WAN 連結進行篩選

  - 依低度使用所提供之頻寬的 WAN 連結進行篩選

  - 依達到重大層級的 WAN 連結進行篩選 (頻寬使用量超過 WAN 連結的 90% 頻寬容量)

  - 依 WAN 連結類型進行篩選：網路網站連結、區域間連結，以及網站內連結。

  - 依網路地區進行篩選

## 應用程式

Bandwidth Utilization Analyzer 提供下列兩個應用程式 (工具)：

  - **WanLinkLogCollector.exe**   此工具可讓其使用者輸入所需資訊。

  - **BandwidthUtilizationAnalyzer.xlsm**  Microsoft Excel 試算表軟體報告可透過 WanLinkLogCollector.exe 自動啟動。此應用程式可讓使用者將篩選條件套用至報告中，如後文中所述。

## 使用 Bandwidth Utilization Analyzer 的程序

Bandwidth Utilization Analyzer 分為兩個使用程序：

  - 收集記錄，可透過 WanLinkLogCollector.exe 執行此操作

  - 自訂報告，可透過 BandwidthUtilizationAnalyzer.xlsm 執行此操作

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945592.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議切勿由使用者手動啟動 BandwidthUtilizationAnalyzer.xlsm。</td>
</tr>
</tbody>
</table>


## 啟動 Bandwidth Utilization Analyzer

利用命令提示字元或透過 Windows 檔案總管啟動 WanLinkLogCollector.exe。

**使用 WanLinkLogCollector.exe**

WanLinkLogCollector.exe 的使用步驟有三：

1.  **記錄時間範圍**   提供需要產生報告的時間範圍

2.  **指定檔案目錄**   提供檔案位置資訊

3.  **收集記錄並啟動報告檢視器**  執行命令以產生報告

## 步驟 1 - 記錄時間範圍

記錄時間範圍可讓工具使用者指定下列項目，如下圖所示。

1.  **開始日期** 此為要產生報告之時間範圍的開始日期，例如 August 1, 2010。

2.  **結束日期** 此為要產生報告之時間範圍的結束日期，例如 September 30, 2010。
    
    ![頻寬使用量分析中的開始與結束日期](images/JJ945604.2c597cfc-3372-4d41-816b-26202f607ad8(OCS.15).jpg "頻寬使用量分析中的開始與結束日期")  

## 步驟 2 - 指定檔案目錄

下列檔案目錄可由使用者如示加以指定。

  - **伺服器記錄檔位置** 儲存頻寬原則伺服器記錄的資料夾位置，通常為 \<fileserver\>\\\<choice of FE\>\\AppServerFiles\\PDP。

  - **暫時檔案儲存位置** 產生報告時儲存中繼檔案的暫時檔案位置。

![頻寬使用量分析中的檔案目錄](images/JJ945604.d66daeac-1669-45e3-932d-3f6782840c2a(OCS.15).jpg "頻寬使用量分析中的檔案目錄")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>確認已將足夠的伺服器記錄與暫時檔案存放區資料夾的檔案存取權限提供給工具使用者。</td>
</tr>
</tbody>
</table>


## 步驟 3 - 收集記錄並啟動報告檢視器

若要收集記錄並啟動報告檢視器，請按一下 **\[執行\]** (如下所示)。此步驟會收集所需資料。

![收集頻寬使用量分析中的資料](images/JJ945604.0019cb2c-7c01-4dc9-ac90-ac47c47d1bfd(OCS.15).jpg "收集頻寬使用量分析中的資料")

輸入驗證成功後，畫面即會顯示以下所示的訊息。

![Bandwidth Utilization Analyser 的記錄收集完畢通知](images/JJ945604.eda91da8-3285-4eab-8ccb-c6d89c8cc221(OCS.15).jpg "Bandwidth Utilization Analyser 的記錄收集完畢通知")

按一下 **\[確定\]**。BandwidthUtilizationAnalyzer.xlsm 即會自動啟動。遵循訊息方塊中的指示操作。如需詳細資訊，請參閱下節的「使用 BandwidthUtilizationAnalyzer.xlsm」。


**使用 BandwidthUtilizationAnalyzer.xlsm**

1.  BandwidthUtilizationAnalyzer.xlsm 自動啟動後，按一下 **\[重新整理\]** (如下所示)。
    
    ![BandwidthUtilizationAnalyzer.xlsm](images/JJ945604.c4e675b9-1671-400e-a712-6db82d731b39(OCS.15).jpg "BandwidthUtilizationAnalyzer.xlsm")

2.  檔案資料夾開啟後，從訊息方塊中所指定的位置選取 consolidated.csv (如下所示)。該位置亦會顯示為 **C:\\Temp**。
    
    ![在 BandwidthUtilizationAnalyzer 中開啟資料夾。](images/JJ945604.601cc572-cee9-45fb-9ed1-c4b96a2fa21e(OCS.15).jpg "在 BandwidthUtilizationAnalyzer 中開啟資料夾。")

3.  按一下 **\[匯入\]**。

4.  圖形化繪圖即會自動產生。該繪圖會在背景作業游標消失後顯示。
    
    ![在報表檢視中套用篩選。](images/JJ945604.1416468e-e3ab-478e-b569-e42ba9c27a17(OCS.15).jpg "在報表檢視中套用篩選。")

## 套用篩選條件至報表檢視

以下所示為可供套用至報表檢視的篩選條件，說明如下：

![在報表檢視中套用篩選。](images/JJ945604.1416468e-e3ab-478e-b569-e42ba9c27a17(OCS.15).jpg "在報表檢視中套用篩選。")

1.  **名稱** 依 WAN 連結進行篩選 (該篩選條件位於圖形右側)。前置詞代表下列連結類型；請見垂直 (藍色) 方塊：
    
      - **S 網站** 網路網站至網路地區的 WAN 連結
    
      - **IS 網站間** 兩個網路網站之間的 WAN 連結
    
      - **R 地區間** 兩個網路地區之間的 WAN 連結

2.  **已超出限制** 依頻寬使用量超過頻寬容量的 WAN 連結進行篩選

3.  **重大層級** 依頻寬使用量達到 90% 或超過頻寬容量的 WAN 連結進行篩選

4.  **低度使用** 依頻寬使用量低於 25% 頻寬容量的 WAN 連結進行篩選

5.  **連結類型** 依下列 WAN 連結類型進行篩選：
    
      - **網路網站**類型
    
      - **站台間**類型
    
      - **地區間連結**類型

6.  **地區** 依網路地區進行篩選

以下各圖會說明上述的篩選條件。

依 **\[名稱\]** 進行篩選。選取要在圖形中顯示之連結的清單。

![在 BandwidthUtilizationAnalyzer 中依 \[Name\] (名稱) 篩選。](images/JJ945604.002b7c8e-f0da-48ce-9e1a-5c34d2cab063(OCS.15).jpg "在 BandwidthUtilizationAnalyzer 中依 [Name] (名稱) 篩選。")

依 **\[已超出限制\]** 進行篩選。選取 **True** 以執行篩選條件。

![依 \[Exceeded Limit\] (已超出限制) 篩選。](images/JJ945604.5946c95e-76ce-46ca-8f3e-a79be1e5c527(OCS.15).jpg "依 [Exceeded Limit] (已超出限制) 篩選。")

依 **\[重大層級\]** 進行篩選。選取 **True** 以執行篩選條件。

![依 \[Critical Levels\] (重大層級) 篩選。](images/JJ945604.60771a52-d8ba-4cb9-a02d-d6c888cb5505(OCS.15).jpg "依 [Critical Levels] (重大層級) 篩選。")

依 **\[低度使用\]** 進行篩選。選取 **True** 以執行篩選條件。

![依 \[Under Utilized\] (低度使用) 篩選。](images/JJ945604.95a2bf01-5aba-4927-af47-1ad3c459d791(OCS.15).jpg "依 [Under Utilized] (低度使用) 篩選。")

依 **\[連結類型\]** 進行篩選。選取一或多個所要顯示的類型。

![依 \[Link Type\] (連結類型) 篩選。](images/JJ945604.08757949-06bd-4cf3-809f-d81fd23a6639(OCS.15).jpg "依 [Link Type] (連結類型) 篩選。")

依 **\[地區\]** 進行篩選。選取要顯示其連結之地區的清單。

![依 \[Region\] (地區) 篩選。](images/JJ945604.5de4cec4-6c09-48bb-98c7-b56f7bdb3d5a(OCS.15).jpg "依 [Region] (地區) 篩選。")

## 需求

  - .NET Framework 3.5

  - Microsoft Excel 2010 或 Excel 2007

## 總結

Bandwidth Utilization Analyzer 乃用於繪製整個網路之 UC 流量的音訊頻寬使用量。這項工具另外亦可用於報告網路的視訊頻寬使用量。

## Call Parkometer

Call Parkometer 乃是可簡易存取通話駐留軌道資料庫的命令列應用程式。

## 說明

Call Parkometer 是可追蹤目前駐留通話的工具，另外亦可收集軌道與通話駐留伺服器 (CPS) 使用方式的統計資料。使用這項命令列工具，即可從本機或遠端連線電腦讀取與寫入 CPS 軌道 SQL Server 資料庫。

所有選項均為互斥選項。命令列語法則如下：

  - **–o** 參數：列出針對此集區所設定的所有軌道範圍。

  - **–n** 參數：列出此集區中所有目前使用的軌道。顯示資訊如下：
    
      - 被駐留者與駐留者的 SIP 統一資源識別項 (URI)。
    
      - 通話駐留所在 CPS 的主機名稱。
    
      - 通話駐留時間的時間戳記。

  - **–f** 參數：列出集區中的目前可用軌道數。

  - **–r \<n\>** 參數：列出最後 \<n\> 個駐留通話。顯示資訊如下：
    
      - 被駐留者 SIP URI。
    
      - 駐留者 SIP URI。
    
      - 通話駐留所在 CPS 的主機名稱。
    
      - 擷取或中斷通話時間的時間戳記。

  - **-t\<n\>** 參數：測試在資料庫中保留軌道以顯示已指派之軌道號碼的隨機性。

## 輸出

根據命令提示字元中所指定的輸入參數，Call Parkometer 會顯示下列輸出：

  - 針對此集區所設定的所有軌道範圍

  - 目前的駐留通話

  - 可用的軌道數目

  - 最近的駐留通話

  - 保留的軌道以供測試統一與隨機軌道值

## 用途

CPS 工具的用途在於提供對 CPS 資料庫的命令列存取權限。系統管理員可檢視 CPS 使用方式並決定指派至集區的軌道數。

## 需求

若是這項工具與 CPS 在相同的電腦上執行，則不受任何需求限制。若是這項工具執行於遠端電腦，則 Lync Server 2013 所採用的 SQL Server 資料庫必須設為允許遠端存取。Call Parkometer 必須以 SQL Server 資料庫連接字串加以設定，才可連線至集區的 SQL Server。此 SQL Server 資料庫連接字串定義於設定檔 **parkometer.exe.config**。這個設定檔必須與 parkometer.exe 位於相同的目錄。下列 XML 檔則為 parkometer.exe.config 範例。必須加以設定的參數為使用者名稱 (例如 mydomain\\Administrator)、密碼 (例如 mypassword) 以及主機名稱 (例如 myserver)。

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
       <add key="SQL" value="server=myserver\RTC;
    database=cpsdyn;
    User Id=mydomain\Administrator;
    Password=mypassword.;
    Integrated Security=false;"/>
      </appSettings>
    </configuration>

## 範例

部署的軌道範圍：–o 參數會列出針對此集區所設定的所有軌道範圍，如下所示

![Call Parkometer 中的軌道範圍。](images/JJ945604.9ede64cb-29d9-4782-a34b-b76c42fbdcad(OCS.15).jpg "Call Parkometer 中的軌道範圍。")

目前的駐留通話：–n 參數會列出此集區中所有目前使用的軌道，如下所示

![Call Parkometer 中的目前駐留通話。](images/JJ945604.07a7eec4-7999-4c92-93f0-95525b244b4c(OCS.15).jpg "Call Parkometer 中的目前駐留通話。")

可用的軌道數目：–f 參數會列出集區中目前可用的軌道數，如下所示

![Call Parkometer 中的可用軌道。](images/JJ945604.ecc1d621-0ca0-4ecf-a579-08b41c6f08ed(OCS.15).jpg "Call Parkometer 中的可用軌道。")

最近駐留的通話：–r \<n\> 參數會列出最近 \<n\> 個駐留通話，如下所示

![Call Parkometer 中的最近駐留通話。](images/JJ945604.1c5eb27d-faa1-491b-b4aa-b484255c3353(OCS.15).jpg "Call Parkometer 中的最近駐留通話。")

測試軌道保留：–t \<n\> 參數會測試在資料庫中保留軌道，如下所示

![Call Parkometer 中的測試軌道保留。](images/JJ945604.84c9b69e-7af0-4224-8711-a43a28f08691(OCS.15).jpg "Call Parkometer 中的測試軌道保留。")

## 總結

Call Parkometer 乃是可提供駐留通話伺服器相關詳細資訊的命令列工具。

## CleanupStorageServiceData

CleanupStorageServiceData Resource Kit 工具可用於將孤立的資料從 Lync Server 存放服務 (LYSS) 所採用的資料庫中加以刪除。存放服務的其中一項功能在於緩衝 Lync Server 與各個後端資料存放端點之間的通訊，例如 SQL Server 與 Exchange。

## 說明

為支援高可用性，LYSS 會暫時接受並儲存資料複本於集區中的多個前端伺服器，然後在資料傳送至其最終長期存放位置時加以移除。在未能正常運作的情況下，可能會發生異常情況，例如伺服器可能發生當機或作業問題，導致部分資料可能無法妥善清除。雖然這類資料並不會造成任何負面影響，但確實會佔用到有限的作業資源。一般要求的資料維護大多會自動執行，但這項工具會在無法執行自動移除作業時安全地識別該類孤立資料並加以移除。當發出監控狀況的 System Center Operations Manager (SCOM) 警示，要求系統管理員從集區的本機 LYSS 資料庫中移除非必要的資料時，系統即會指示使用這項工具。觸發警示的前端會在事件記錄檔中顯示相對應的事件。事件詳細資訊將包括前端所含之孤立資料量的相關資訊；若是該類資料超出特定預設閾值即會發出警示。

## 需求

安裝 Lync Server 2013 Resource Kit 工具。這項工具必須執行於已加入網域且安裝 Lync Server 與 Lync Server 2013 管理命令介面的機器。這項工具會透過管理命令介面使用 Cmdlet 找出集區中的所有前端伺服器。再者，執行這項工具的機器所在的集區必須安裝 **RtcLocal** 資料庫。CleanupStorageServiceData 工具將利用此資料庫取得與 Lync Server 路由服務通訊所需的連線詳細資訊。最後，叫用這項工具的帳戶或認證對於要寫入輸出記錄的檔案共用區必須擁有讀取/寫入權限。另外，這項工具依賴集區狀態的穩定。基本上，這表示每個前端伺服器必須為正常啟動與執行，SQL Server LYNCLOCAL 執行個體與 LYSS 資料庫必須能夠加以連線，且各個路由群組必須具有一套完整的伺服器：1 個主要前端伺服器與 2 個次要前端伺服器。

## 範例

C:\\Program Files\\Microsoft Lync Server 2013\\ResKit\\StorageService\> ImportStorageServiceData.exe

    Description:
    This tool will remove orphaned data from the Storage Service database
    for a pool. You are required to run this tool on a machine inside the
    pool which has the Lync Server Management Shell installed and has RtcLocal database installed.
    Usage: Default behavior is to clean up orphaned data from the all the 
           Storage Service databases in the current pool.
    Additional Options:
    -Verbose    : Turn verbose output on.
    -LogPath    : The UNC path to which to write the log.
    ------------------------------------------------------------------------------
    Please wait while we initialize...
    Found 4 front end servers
    Replica Instances for LYSS Service
    Address: server2.vdomain.com - Primaries: 7 Secondaries: 14
    Address: server.vdomain.com - Primaries: 7 Secondaries: 14
    Address: server1.vdomain.com - Primaries: 7 Secondaries: 14
    Address: server3.vdomain.com - Primaries: 7 Secondaries: 14
    Primary Total Count = 28, Secondary Total Count = 56
    Finding and removing orphaned data for 28 routing groups
    Removing 1 stale groups from FE server.vdomain.com
    No stale routing groups detected on FE server2.vdomain.com
    No stale routing groups detected on FE server1.vdomain.com
    No stale routing groups detected on FE server3.vdomain.com
    Searching for stale queue items
    Removed 20 stale queue items for routing group 17D5435AE40259F7BBDF1866776386E4
    No stale queue items found for routing group 1975349662315F90B119DACB4F2AE3AD
    No stale queue items found for routing group 1A23E3D58BDB5A458A0B73F34AB7ACBE
    No stale queue items found for routing group 1AC91E3A1029535A80123121989CEADC
    No stale queue items found for routing group 3313935458E35B9B9759E08A15D251E6
    No stale queue items found for routing group 39BB0035B06B5427873FC6099720462A
    No stale queue items found for routing group 40721948E7B55CE893A53E911F76D185
    No stale queue items found for routing group 4501E04EAE4856059346949FF817C220
    No stale queue items found for routing group 4D833C98801F546F8E45E417EE028E2E
    No stale queue items found for routing group 5AD77443AD955A22A876749BE66D5317
    No stale queue items found for routing group 69844A271E6C5633A1F2B46A42287DD6
    No stale queue items found for routing group 69DA3BE407A95C7284EB4B1337718C93
    No stale queue items found for routing group 8437358AB34A5CC8967D5EF39494AB8D
    No stale queue items found for routing group 8ED455B1789655359816E1C5BF4C430F
    No stale queue items found for routing group 904F6C9B8AC951AE8B3C86684D3832E4
    No stale queue items found for routing group 90AAB3AE9A1950E0ADE7809A27021D63
    No stale queue items found for routing group 944F5724C65C5F93900DC1C8C898B102
    No stale queue items found for routing group 9E8A2630250C51769E39F63F0FB552BA
    No stale queue items found for routing group A11E27AE439A582288D4657EDA86B565
    No stale queue items found for routing group A9B10C76E764556FAEA3E47301EDF518
    No stale queue items found for routing group AEA2699E74ED59848ACEA7896699430D
    No stale queue items found for routing group B269961603E75065AFDA4F4F006DA5E4
    No stale queue items found for routing group BB873D9A3DA959DAB2FD743E5AA619F7
    No stale queue items found for routing group BCC6A48FBA2454B79B9EDB276657A404
    No stale queue items found for routing group C8EF4805722B5F6C876EBC0440B420FD
    No stale queue items found for routing group CA38EBDAC4845489ACE208C2240E4056
    No stale queue items found for routing group F5921887DB025C5F908CE42DB7F1AEE8
    No stale queue items found for routing group F9E606A825395422B3BF7A01ECBB7B1F
    Writing log: M:\Dev\Server\ResKit\StorageService\CleanupStorageServiceData.Log_20121009_151040
    Tool has finished execution.  Errors encountered: 0
    C:\Program Files\Microsoft Lync Server 2013\ResKit\StorageService>

## DBAnalyze

## 說明

DBAnalyze 乃是有助於系統管理員收集 Lync Server 2013 資料庫相關分析報告的命令列工具。DBAnalyze 有下列模式：診斷、使用者資料、會議、MCU 以及磁碟分割：

  - **診斷模式**   建立包含下列相關資訊的報告：表格 (記錄數、分割、資料大小，以及索引大小)、資料與記錄檔大小、上次備份時間、執行 Microsoft Office Communications Server 的伺服器上的連絡人通訊群組、權限平均數、連絡人、容器、訂閱、發行集、每名使用者端點、任何未正確裝載的使用者、無法路由的使用者、每名使用者召集的平均會議數、排程會議、作用中會議，以及資料庫版本。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>執行診斷模式可能會影響伺服器效能。</td>
    </tr>
    </tbody>
    </table>


  - **使用者資料模式**  針對指定的使用者或連絡清單與權限清單中有該名使用者的使用者報告連絡人、容器、訂閱、發行集、權限以及連絡群組資料。此模式另外也會報告使用者召集或受邀之會議的摘要資料。

  - **會議模式**   報告特定會議的詳細資料，包括會議的所有排程時間詳細資料、受邀者清單、會議所允許的媒體類型清單、作用中的 MCU (Multipoint Control Unit)、作用中的參與者清單，以及各個參與者的訊號狀態。

  - **將會議識別碼解碼**  將 **/pstnid** 參數所指定但未連線至後端的公用交換電話網路 (PSTN) 會議識別碼加以解碼。

  - **解析會議**   將 **/pstnid** 參數所指定並顯示識別碼所指示之相關會議資訊的 PSTN 會議識別碼加以解碼。

  - **MCU 模式**  報告集區中各個 MCU 的識別碼、媒體類型、URL、活動訊號狀態、會議負載，以及參與者負載。

  - **磁碟分割模式**  顯示所有磁碟的分割狀態。

這項工具可用於診斷各種問題或協助系統管理員執行容量規劃。例如說，若是位於伺服器 A 的大多數使用者選擇位於伺服器 B 的使用者作為其連絡人，系統管理員可將使用者從伺服器 A 移至伺服器 B 以降低跨伺服器流量。

## 輸出

這項工具會輸出有關 Lync Server 2013 資料庫的預先定義報告。**路徑：**%ProgramFiles%\\Microsoft Lync Server 2013\\Reskit

## 用途

若要安裝 Dbanalyze.exe，請將其複製至本機資料夾，然後執行該工具。若要使用該工具，請透過命令列執行下列命令。`dbanalyze.exe [/v] [/report:value] [/sqlserver:value] [/user:user@domain.com] [/conf:value][/pstnid:Value] [/maxcontacts:value]` 命令列選項的說明如下所示：

![Dbanalyze.exe 的命令列選項。](images/JJ945604.22bf3432-af6d-495b-8f48-d94c5d259523(OCS.15).jpg "Dbanalyze.exe 的命令列選項。")

## 需求

**電腦** 執行 DBAnalyze 的電腦必須已加入網域且安裝 Lync Server 2013。

**網路** 電腦應該要能夠連線至後端資料庫。

**軟體** 必須先安裝 Lync Server 2013 軟體元件才能執行 DBAnalyze。

**使用者** 下表顯示具有必要權限可以存取 Lync Server 2013 資料庫的系統管理員。

![Dbanalyze.exe 的權限表。](images/JJ945604.b8931e9e-834e-4dec-8a84-2fc47d1613e9(OCS.15).jpg "Dbanalyze.exe 的權限表。")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行 <strong>/report:disk</strong> 模式必須要有本機系統管理員帳戶。</td>
</tr>
</tbody>
</table>


## 範例

以下為有效的 Dbanalyze.exe 命令範例：

    dbanalyze.exe /report:diag
    dbanalyze.exe /report:user /user:usera@domainb.com
    dbanalyze.exe /report:conf /user:bob@example.com /conf:1W9J71SKSX2X
    dbanalyze.exe /report:resolve /pstnid:12345
    dbanalyze.exe /report:mcus
    dbanalyze.exe /report:disk

## 總結

DBAnalyzer 可讓系統管理員快速簡便地分析 Lync Server 2013 資料庫。

## ImportStorageServiceData

ImportStorageServiceData Resource Kit 工具可將已從存放服務 (LYSS) 清除的佇列與端點資料重新匯入至存放服務。

## 說明

根據佇列項目狀態或資料庫大小從存放服務清除資料的作業可能為自動 (定期) 作業。這項作業亦可透過手動叫用集區容錯移轉 Cmdlet 或由集區容錯移轉 Cmdlet 所叫用的 StorageServiceFullFlush Cmdlet 而執行。請注意，若是位於前端的任何存放服務 (LYSS ) 資料庫超過一般大小，最好不要重新匯入資料，因為如此可能導致有更多資料遭到匯出。再者，任何可能引發錯誤而導致存放服務佇列增長的問題應先加以解決 (例如 Exchange 端點錯誤、網路問題或其他問題)。

**案例 1：** 集區容錯移轉期間，檔案可能會從各個前端的存放服務中清除。容錯移轉完成後，應執行這項工具以重新匯入資料。

**案例 2：** 資料會每天自動清除或因為存放服務資料庫超過特定大小閾值 (例如 60%、80%、90% 滿) 而清除。這些自動清除的資料應由系統管理員定期重新匯入。在上述情況下，若是未部署監視的 SCOM 套件，即會發生從 Lync Server 存放服務清除資料的相關存放服務事件。事件識別碼有 32075 (完整清除作業已開始)、32076 (完整清除已完成)、32082 (維護層級清除已開始)、32083 (維護層級清除完成)、32089 (由於資料庫填滿而發生清除)。請注意，這些事件識別碼所對應的是 RTM 版本。當系統管理員看到這些事件，代表有檔案遭到清除。請利用這項工具定期匯入這些資料，例如每週一次。

對於線上服務版本，如有部署監控狀況的 Lync Server SCOM 套件，可能會發出新警示，要求系統管理員將遭到清除的資料重新匯入存放服務。觸發警示的前端伺服器也會在事件記錄中顯示相對應的事件。這個事件將提供已清除的資料檔案所在之父路徑以及符合警示準則之檔案數的說明。警示準則內容如下：特定父路徑下有 X 個以上的檔案至少已達 Y 天 (X 與 Y 預設於 StorageService，但可透過變更 APPCONFIG 檔案加以覆寫。) 以下顯示兩個可能觸發狀況警示的事件範例，差異點僅在於其父路徑有所不同：其中一個可能是位於 Web 服務檔案共用區下，另一個可能則是位於各個前端之本機應用程式資料目錄。(例如 c:\\ProgramData\\Microsoft\\Lync Server\\StorageService )。接著系統管理員將執行這項 Reskit 工具。

在資料並非由執行工具所在的前端所擁有的情況下，這項工具將增加執行所在之前端以及其他前端的 CPU 與 IO 負載。建議在前端並未處於 CPU 與 IO 負載過重的情況下執行這項工具，例如非尖峰時間。再者，評估工具執行時間時，請記住這項工具可在 2 至 3 分鐘內匯入一個資料檔案。由這項工具所產生的詳細資訊記錄檔依預設將位於檔案存放區。若是未有回報任何錯誤，請加以刪除，因為記錄檔大小可能超過數十 MB。

![Storage Server 事件記錄事件範例。](images/JJ945604.3a903ef7-ea8a-4606-8229-a3e32f13af3a(OCS.15).jpg "Storage Server 事件記錄事件範例。")

## 需求

安裝 Lync Server 2013 Resource Kit 工具。執行這項工具的機器必須已加入網域且安裝 Lync Server 與 Lync Server 管理命令介面。這項工具會透過管理命令介面而使用 Cmdlet 識別集區中的所有前端伺服器。再者，執行這項工具的機器所在集區必須安裝 **RtcLocal** 資料庫。這項工具將利用這個資料庫擷取集區之 WEBSERVICE 檔案共用區的位置。此外，使用這項工具前，必須先透過 **Enable-PSRemoting** 在各個前端伺服器上啟用 Windows PowerShell，執行工具所在的機器亦是如此。否則，從這項工具遠端執行 Windows PowerShell 命令將會發生失敗。集區中的所有前端伺服器之　Windows PowerShell 遠端執行功能會在完成後加以關閉。最後，叫用這項工具的帳戶或認證對於工具執行所在的集區之網路服務檔案共用區必須擁有讀取/寫入權限，否則這項工具將會因為 IO 權限錯誤而失敗。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Windows Server 2012 中，依預設會啟用 Windows PowerShell 遠端執行功能，但在 Windows Server 2008 作業系統 則不會啟用。</td>
</tr>
</tbody>
</table>


## 範例

    >  C:\StorageService>ImportStorageServiceData.exe
    Description:
    This tool will re-import Storage Service (LYSS) flushed queue data back in.  For a pool: you are required to run this tool on a machine inside the pool which has the Lync Server Management Shell installed.  Additionally, all front end machines need to have Windows Powershell Remoting enabled before executing this tool by executing Enable-PSRemoting.  Also, please ensure that all Storage Service instance DB Size are at the 'Normal' level (verify this by viewing Eventlog events). Otherwise re-importing may cause data to be flushed out again if any Storage Service instance DB size level goes above 'Normal'.
    Usage: Default behavior is to Import data from web service file share as well as any files on all Front End machines in pool.
    Additional Options:
    -Verbose                    : Turn verbose output on.
    
    -StorageServiceHostName     : Host Name of Storage Service WCF endpoint.  ( Default=localhost netnamedpipe binding. )
                                        
    -FileSharePath              : Import only all data from just under the UNC path specified.
    
    ActivityID: cc3b62ff-bb66-4e61-a6e2-96cb3626315c. <-- Use this to correlate with StorageService trace logs if troubleshooting.
    Type Server name (TCP binding) or press <enter> for localhost (NamePipe binding):
    Using NetNamedPipeBinding...
    OnTopologyChanged Event received
    Web Service File Share: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService
    
    Front Ends:
    server.vdomain.com
    server2.vdomain.com
    server1.vdomain.com
    server3.vdomain.com
    Looking under directory: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService for exported data.
    # Files found: 8
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml
    Items deserialized: 20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml
    Items deserialized: 20
    
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server1.vdomain.com, queueItems=20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\904f6c9b8ac951ae8b3c86684d3832e4__0.xml
    
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server1.vdomain.com, queueItems=20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\904f6c9b8ac951ae8b3c86684d
    3832e4__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\904f6c9b8ac951ae8b3c
    86684d3832e4__0.xml
    
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER1.vdomain.com\904f6c9b8ac951ae8b3c86684d3832e4__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER2.vdomain.com\69844a271e6c5633a1f2b46a42287dd6__0.xml
    
    Items deserialized: 20
    
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server2.vdom
    ain.com, queueItems=20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER2.vdomain.com\69844a271e6c5633a1f2b46a42
    287dd6__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER2.vdomain.com\69844a271e6c5633a1f2
    b46a42287dd6__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER2.vdomain.com\69844a271e6c5633a1f2b46a42287dd6__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\3313935458e35b9b9759e08a15d251e6__0.xml
    
    Items deserialized: 20
    
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=1
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\3313935458e35b9b9759e08a15
    d251e6__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\3313935458e35b9b9759
    e08a15d251e6__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\3313935458e35b9b9759e08a15d251e6__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\4501e04eae4856059346949ff817c220__0.xml
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=1
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\4501e04eae4856059346949ff8
    17c220__0.xml
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\4501e04eae4856059346
    949ff817c220__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\4501e04eae4856059346949ff817c220__0.xml: succeeded: 20, failed: 0
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\5ad77443ad955a22a876749be66d5317__0.xml
    
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=20
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\5ad77443ad955a22a876749be6
    6d5317__0.xml
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\5ad77443ad955a22a876
    749be66d5317__0.xml
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\5ad77443ad955a22a876749be66d5317__0.xml: succeeded: 20, failed: 0
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\a11e27ae439a582288d4657eda86b565__0.xml
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=20
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\a11e27ae439a582288d4657eda
    86b565__0.xml
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\a11e27ae439a582288d4
    657eda86b565__0.xml
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\a11e27ae439a582288d4657eda86b565__0.xml: succeeded: 20, failed: 0
    All files have been imported into Storage Service for path: \\dc.vdomain.com\OcsFileStore\co1-WebSer
    vices-1\StorageService
    Importing files for: server.vdomain.com
    No files founds.
    Importing files for: server2.vdomain.com
    No files founds.
    Importing files for: server1.vdomain.com
    No files founds.
    Importing files for: server3.vdomain.com
    No files founds.
    Writing log: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\ImportStorageServiceData
    Log20120910_1609SS
    Tool has finished execution.
    >  C:\StorageService>

## LCSSync

LCSSync 工具可協助在多樹系環境中部署 Lync Server 2013 通訊軟體。這項工具可用於將來自不同使用者樹系的使用者與群組同步化為 Lync Server 2013 安裝所在中央樹系的 Active Directory 網域服務連絡人物件。

## 說明

LCSSync 會透過中央樹系中經過同步化的 Active Directory 網域服務連絡人物件而針對 Lync Server 啟用使用者。若要提供單一登入功能，主要使用者帳戶必須對應至 Lync Server 2013 之中央樹系中的 Active Directory 網域服務連絡人物件。這項工具可協助執行該對應作業。這項工具會提供在 Microsoft Identity Integration Server 中建立管理代理程式的範本。

## 總結

LCSSync 工具可協助在多樹系環境中部署 Lync Server。

## LookupUserConsole

LookupUserConsole 工具會顯示特定使用者的內部 Lync Server 路由資訊。這項資訊可能有助於 Microsoft 支援人員診斷有關部署與路由的問題。

## 說明

執行 LookupUserConsole.exe 將開啟接受 SIP 位址的命令提示字元並嘗試顯示相關的內部 Lync Server 路由資訊。輸入 **exit** 即可結束 LookupUserConsole 工具。

## 需求

安裝 Lync Server 2013 Resource Kit 工具。執行這項工具的機器必須已加入網域且安裝 Lync Server。

## 範例

C:\\Program Files\\Microsoft Lync Server 2013\\ResKit\>LookupUserConsole.exe

    > sip:john.doe@vdomain.com
    
      Execution time (ms):                            171.094
      Exeuction result:                               Success
      SIP URI:                                        sip:john.doe@vdomain.com
      User info:
        SID:                                          S-1-5-21-2831376166-29632525...    Display name:                                     John Doe
        Grouping ID:                                  00000000-0000-0000-0000-...
        Line URI:                                     <null>
        Policy assignment:                            TenantId={00000000--0000-000....
        SIP enabled:                                  True
        UC enabled:                                   False
        Tenant ID:                                    00000000-0000-0000-0000-...  Cluster info:
        Active cluster:                               pool0.vdomain.com
        Backup registrar cluster:                     <null>
        Deployment location:                          <null>
        Home Front-End FQDN:                          SERVER.vdomain.com
        Primary Registrar cluster:                    pool0.vdomain.com
        Remote Director external SIP FQDN:            <null>
        Remote Director internal SIP FQDN:            <null>
        Remote Director Web FQDN:                     <null>
        Routing group ID:                             4501e04e-ae48-5605-9346...
        Service tag ID:                               1266953005
        User Front-End resolved:                      True
        User in local forest:                         True
        User in remote forest:                        False
        User in split domain:                         False
        User-Services cluster:                        pool0.vdomain.com
    
    > sip:nouser@vdomain.com
    
      Execution time (ms):                            948.7574
      Exeuction result:                               UserDoesNotExist
    
    > exit

## MsTurnPing

MSTurnPing 工具可讓 Microsoft Lync Server 2013 通訊軟體系統管理員檢查下列伺服器狀態：執行 Audio/Video Edge 與 Audio/Video 驗證服務的伺服器，以及在拓撲中執行頻寬原則服務的伺服器。

## 說明

MSTurnPing 工具可讓 Lync Server 2013 通訊軟體系統管理員檢查下列伺服器狀態：執行 Audio/Video Edge 與 Audio/Video 驗證服務的伺服器，以及在拓撲中執行頻寬原則服務的伺服器。

這項工具可讓系統管理員執行下列測試：

1.  A/V Edge Server 測試：這項工具可針對拓撲中的所有 A/V Edge Server 進行下列操作以執行測試：
    
      - 確認 Lync Server Audio/Video 驗證服務已啟動並可發出正確認證。
    
      - 確認 Lync Server Audio/Video Edge Service 已啟動並可成功在外部 Edge 上配置資源。

2.  頻寬原則服務測試：這項工具可針對拓撲中執行頻寬原則服務的所有伺服器進行下列操作以執行測試：
    
      - 確認 Lync Server 頻寬原則服務 (驗證) 已啟動並可發出正確認證。
    
      - 確認 Lync Server 頻寬原則服務 (核心) 已啟動並可成功執行頻寬檢查。

執行這項工具的電腦必須為拓撲的一部分，並且已安裝本機存放區。

## 輸出

這項工具會輸出各個作業的結果。

  - 若是執行 **AudioVideoEdgeServer** 測試，這項工具會輸出下列內容：
    
      - 在拓撲中提供 Lync Server Audio/Video 驗證服務之電腦的測試結果
    
      - 在拓撲中提供 Lync Server Audio/Video Edge Service 之電腦的測試結果

  - 若是執行 **BandwidthPolicyServer** 測試，這項工具會輸出下列內容：
    
      - 在拓撲中提供 Lync Server 頻寬原則服務 (驗證) 之電腦的測試結果
    
      - 在拓撲中提供 Lync Server 頻寬原則服務 (核心) 之電腦的測試結果

## 需求

  - 執行這項工具的電腦必須位於拓撲中，並有本機存放區。

  - 必須以系統管理員身分執行這項工具，並有本機存放區的存取權限。

## 範例

以下為工具輸入範例：

    MsTurnPing -ServerRole AudioVideoEdgeServer
    
    MsTurnPing -ServerRole BandwidthPolicyServer

## 總結

若是 Lync Server 2013 系統管理員需要檢查執行 Audio/Video 與頻寬原則服務之伺服器的狀態，這項工具將會是相當實用的資源。

## Network Configuration Viewer

Microsoft Lync Server 2013 通訊軟體系統管理員利用 Network Configuration Viewer 即可針對佈建為允許即時通訊工作階段的企業而檢視通話許可控制服務 (CAC) 網路拓撲，例如根據指定的頻寬容量而提供的語音或視訊通話。Lync Server 2013 系統管理員所定義的 CAC 原則將由與 Lync Server 2013 一併安裝的頻寬原則服務加以執行。

## 說明

Network Configuration Viewer (NetworkConfigurationViewer.exe) 可讓系統管理員執行下列工作：

  - 以圖形格式從 Lync Server 2013 部署中載入並檢視 CAC 網路拓撲。

  - 以圖形格式從頻寬原則伺服器記錄檔中載入並檢視 CAC 網路拓撲。

  - 以 XML 格式將 CAC 網路拓撲儲存在磁碟中。

  - 以 JPG 或 BMP 格式儲存 CAC 網路拓撲圖表。

  - 檢視 CAC 網路拓撲設定資料。

  - 以樹狀檢視的形式檢視 CAC 網路拓撲。

  - 定義 CAC 網路拓撲連結 (例如網站對地區、地區對地區，以及網站對網站的連結) 的自訂連接器。

  - 檢視 CAC 網路拓撲的網站資訊、地區資訊，以及佈建的頻寬原則與網路連結。

## 用途

在圖形化介面中檢視企業 CAC 網路拓撲連結。

## 範例

**以圖形格式從 Lync Server 2013 部署中載入並檢視 CAC 網路拓撲：** Lync Server 2013 系統管理員若要在任何 Lync Server 2013 電腦上載入並檢視 CAC 網路拓撲設定，可利用 **\[下載網路設定\]** 選項加以執行，如下圖所示。若是這項工具部署於無法連線至 Lync 設定存放區的電腦，將無法下載或檢視這類設定。

![下載網路設定。](images/JJ945604.8d126d3f-2545-4f13-a244-974f09614982(OCS.15).jpg "下載網路設定。")

**以圖形格式從頻寬原則伺服器記錄檔中載入並檢視 CAC 網路拓撲：** Lync Server 2013 頻寬原則伺服器會透過記錄機制而將 CAC 網路拓撲儲存於 Lync Server 2013 檔案共用區位置下。Lync Server 系統管理員若要以圖形格式檢視這類檔案，可利用 **\[開啟網路設定\]** 選項加以執行，如下所示。

![開啟 Bandwidth Policy Server 記錄檔。](images/JJ945604.3e503e92-aacb-4921-a8d2-23f860fe2df6(OCS.15).jpg "開啟 Bandwidth Policy Server 記錄檔。")

以 XML 格式將 CAC 網路拓撲儲存在磁碟中：Lync Server 2013 系統管理員若要以 XML 格式儲存 CAC 網路拓撲設定檔，可利用 **\[儲存網路設定複本\]** 選項加以執行，如下所示。儲存的設定檔接著即可用於離線圖形檢視用途。

![將網路設定儲存為 XML 檔。](images/JJ945604.6eeef3b0-78b5-4ee6-8d94-1a4ddf3d8676(OCS.15).jpg "將網路設定儲存為 XML 檔。")

以 JPG 或 BMP 格式儲存 CAC 網路拓撲圖表：Lync Server 2013 系統管理員若要以圖形格式 (JPG 與 BMP 檔案格式) 儲存 CAC 網路拓撲設定，可利用 **\[將網路設定圖表儲存為圖片\]** 選項加以執行，如下所示。

![將網路設定儲存為圖片。](images/JJ945604.145a6fb9-58b1-46b1-bbd5-a661ceba07b4(OCS.15).jpg "將網路設定儲存為圖片。")

**檢視 CAC 網路拓撲設定資料：** Lync Server 2013 系統管理員若要以文字格式檢視相關的網路設定資料，例如網路地區、網路網站、頻寬設定檔，以及站台子網路 IP 位址，可利用 \[檢視網路設定資料\] 選項加以執行，如下所示。

![檢視網路設定資料。](images/JJ945604.b72a4c21-a042-4d91-bf96-fcb396af0679(OCS.15).jpg "檢視網路設定資料。")

**以樹狀檢視的形式檢視 CAC 網路拓撲：** Lync Server 2013 系統管理員若要以圖形樹狀檢視的形式檢視相關的網路設定資料，可利用工具視窗左側的控制面板加以執行，如下所示。

![以樹狀檢視的形式檢視網路設定資料。](images/JJ945604.4d924ac9-fd96-430f-b211-ee35b7ef9a23(OCS.15).jpg "以樹狀檢視的形式檢視網路設定資料。")

**定義 CAC 網路拓撲連結 (例如網站對地區、地區對地區，以及網站對網站的連結) 的自訂連接器：** Lync Server 2013 系統管理員若要針對 CAC 網路設定 WAN 連結定義自訂圖形連接器，可利用 \[設定\] 選項加以執行，如下所示。如此有助於區分佈建於網路設定中之網路連結的各種類型。

![為 CAC 網路拓撲定義自訂連接器](images/JJ945604.b20bea67-c8e1-453e-b1dd-e2aa17b62566(OCS.15).jpg "為 CAC 網路拓撲定義自訂連接器")

**檢視 CAC 網路拓撲的網站資訊、地區資訊，以及佈建的頻寬原則：** Lync Server 2013 系統管理員若要檢視相關的 CAC 網路地區資訊、網站資訊，以及 CAC 頻寬佈建資訊，可利用以下所示的選項。(例如說，在網路地區或網路網站物件中按一下 **\[資訊\]**。)

![為您的網路定義自訂連接器。](images/JJ945604.26262c75-4342-41c3-bc98-1793aa6a7713(OCS.15).jpg "為您的網路定義自訂連接器。")

## 總結

若是 Lync Server 2013 系統管理員需要以圖形格式檢視其部署的 CAC 網路拓撲，這項工具將會是相當實用的資源。

## Response Group Agent Live

回應群組應用程式可讓專員得以利用其內建的 Web 服務而存取實用的即時資訊；然而，以圖形檢視這類資料的功能無法脫離這個應用程式存在。Response Group Agent Live Resource Kit 工具則可提供這類資訊的簡易圖形存取功能，再加上 Microsoft Lync 2013 通訊軟體即時資訊 (例如其他專員的目前狀態) 的輔助，進而解決上述問題。

## 說明

Response Group Agent Live 乃是提供登入與登出功能以及部分即時資訊 (例如群組成員資格與目前通話數) 給回應群組專員的 Windows 應用程式，其用意在於作為強化版的 \[專員群組\] 頁面 (可從 Lync 2013 中存取)。

## 用途

回應群組應用程式會將來電排入佇列，然後路由至專員群組。專員對於要處理哪些通話，若要做出周延的決策，可存取其專員群組的相關即時資訊，例如其他有哪些專員有空，以及各個佇列所等候的電話數。這項資訊原本僅可透過回應群組服務加以存取，現在可利用 Response Group Agent Live 以直覺方式進行瞭解。

## 功能

Response Group Agent Live 工具建置於回應群組服務與 Microsoft Lync 2013 SDK。這項工具可將回應群組服務中的可用資訊與功能，提供給回應群組專員 (例如群組成員資格、其他專員的目前狀態，以及等候中電話數)。

下圖說明 Response Group Agent Live 的主要介面。

![Response Group Agent Live 工具。](images/JJ945604.63cb0374-a6ef-4a59-b60e-bec86a880d09(OCS.15).jpg "Response Group Agent Live 工具。")

以下為專員在 Response Group Agent Live 中所能使用的三個主要功能：

  - **登入/登出：** 相對於 \[專員群組\] 頁面 (可從 Lync 2013 中存取)，Response Group Agent Live 僅供專員同時登入或登出所有專員群組。這項應用程式提供專員三種快速登入或登出的方式：
    
      - 按一下應用程式中的 \[登入/登出\] (綠色與紅色) 按鈕。
    
      - 以滑鼠右鍵按一下系統匣圖示，然後選取登入或登出。
    
      - 使用可供設定的鍵盤快速鍵。

  - **群組成員資格：** 選取專員群組後，Response Group Agent Live 即會在右側窗格中顯示群組專員清單。若是 Lync 2013 與這個應用程式執行於相同的電腦，Response Group Agent Live 中即會顯示目前狀態資訊以及連絡人卡片。專員可直接從該處傳送 IM 或致電給其他專員。

  - **即時統計資料：** Response Group Agent Live 可提供所有專員群組的即時統計資料。更新頻率為一分鐘。當回應群組接聽通話後，具有目前佇列通話數的群組名稱旁即會新增視覺指示器。另外，將游標停留於群組上方亦可顯示最長等候時間。

## 需求

執行 Response Group Agent Live 需要安裝 .NET Framework 4.0。此外，為善用目前狀態與連絡人卡片的功能，必須在本機安裝 (並執行) Lync 2013。

## 設定

使用應用程式中的 \[選項\] 對話方塊可將 Response Group Agent Live 自訂為個人偏好設定。此外，系統管理員可直接編輯 RGAgentLive.exe.config 檔中的 defaultHostAddress 屬性以定義預設的主機位址。

下圖說明專員可用於設定主機位址與快速鍵的 \[選項\] 對話方塊。按一下主要介面右上方的 \[選項\] 按鈕即可存取這個對話方塊。

![Response Group Agent Live \[Options\] (選項) 對話方塊。](images/JJ945604.3cc15e29-8699-45ab-90c3-e1565fa6ebf6(OCS.15).jpg "Response Group Agent Live [Options] (選項) 對話方塊。")

以下列出可在 Response Group Agent Live 設定中加以自訂的三個設定：

  - 主機位址：一般為屬於專員之主集區的網路集區 FQDN。系統會利用這項資訊而自動在背景中導出正確的回應群組服務位址 (在主機後面接上正確路徑)。

  - 快速鍵：登入/登出的確切快速鍵均可加以自訂。唯一的限制在於，兩個快速鍵都必須包含「Windows 標誌」按鍵 (另外加上至少一個按鍵)。

  - 隨 Windows 啟動：此應用程式可設為自動與 Windows 一併啟動。

## 範例

下圖說明如何致電或傳送 IM 給其他專員：以滑鼠右鍵按一下右側窗格中的連絡人。

![撥打電話或傳送 IM。](images/JJ945604.009cebe0-5a93-4745-89c3-8a16c7c13009(OCS.15).jpg "撥打電話或傳送 IM。")

下圖說明 Response Group Agent Live 會如何顯示佇列中的目前通話數以及在這些來電中最長的等候時間。

![檢視佇列資訊。](images/JJ945604.131d7f79-b7ed-41f5-a9da-ffc556e31037(OCS.15).jpg "檢視佇列資訊。")

## 總結

快速登入與登出、群組成員資格，以及基本的即時統計資料均為回應群組專員的特色功能，僅可透過回應群組服務而在應用程式外部使用。Lync 系統管理員可利用 Response Group Agent Live Resource Kit 工具而讓其專員得以使用 Windows 應用程式，進而以更加快速的圖形化方式執行工作。

## SEFAUtil

SEFAUtil (次要擴充功能啟用) 為命令列工具，可讓 Microsoft Lync Server 2013 通訊軟體系統管理員與服務台專員代表 Lync Server 2013 使用者設定代理人響鈴、來電轉接、同時響鈴、小組通話設定以及群組來電接聽。這項工具亦可讓系統管理員查詢針對特定使用者所發佈的電話路由設定。SEFAUtil 工具可讓系統管理員代表使用者啟用/停用/修改來電轉接或同時響鈴。系統管理員可自行指定目標 (採取 SIP URI 的形式) 或使用由使用者所發佈的目標。這項工具亦可讓系統管理員代表使用者新增或移除代理人或小組通話群組成員。這項工具建置於 Microsoft Unified Communications Managed API (UCMA) 3.0，且要求系統管理員在 SEFAUtil 的中央管理存放區中建立信任的應用程式

SEFAUtil (次要擴充功能啟用) 可讓 Lync Server 2013 系統管理員與服務台專員代表 Lync Server 2013 使用者設定代理人響鈴、來電轉接、同時響鈴、小組通話設定以及群組來電接聽。這項工具亦可讓系統管理員查詢針對特定使用者所發佈的來電路由設定。

## 說明

目前的 SEFAUtil 版本僅為命令列工具；並未有支援的圖形使用者介面。這項工具建置基礎為 Microsoft Unified Communications Managed API (UCMA) 3.0。工具所提供的功能可讓系統管理員與服務台專員執行下列操作：

  - 檢視使用者的所有電話路由設定 (包括來電轉接、委派、同時響鈴、小組通話以及群組來電接聽)

  - 啟用/停用/修改來電轉接設定 (包括目的號碼與無人接聽計時器)

  - 啟用/停用/修改來電轉接立即設定

  - 啟用/停用/修改委派設定

  - 啟用/停用/修改小組通話群組設定
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 SEFAUtil 工具的新功能</td>
    </tr>
    </tbody>
    </table>


  - 啟用/停用/修改同時響鈴設定 (包括目的號碼)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 SEFAUtil 工具的新功能</td>
    </tr>
    </tbody>
    </table>


  - 啟用/停用/修改群組來電接聽設定
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945596.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 SEFAUtil 工具的新功能</td>
    </tr>
    </tbody>
    </table>


這項工具有下列限制：

  - 僅有位於 Lync Server 集區的使用者受到支援

  - 大量編輯多名使用者的電話路由設定不受支援

## 輸出

這項工具的目前版本僅會在命令提示字元視窗中提供輸出。如需詳細資訊，請參閱本文件稍後所述的「範例」章節。

## 用途

以下列出這項工具的主要使用案例：

  - Bob 擔任主管職，剛移至 Lync Server 電話語音。他在既有的 PBX 系統中設有委派功能。在移至 Lync 時，系統管理員可設定 Bob 的路由以反映其既有的委派設定。

  - Alice 在外出旅行時發現她要等一通重要的客戶電話。然而，身在飯店的她沒有電腦可用，於是她致電給服務台，要求將撥打至她的公司電話的所有來電一律轉接至她的手機。服務台人員可代為執行這項設定。

  - Joe 在工作時，撥打至他的公司電話的來電會轉至他的手機語音信箱；然而，這只有在其他地點時才多半適用。服務台技術人員可檢視 Joe 的路由設定，發現 Joe 設有同時響鈴至他的手機的功能。技術人員詢問 Joe 有關辦公室的行動覆蓋範圍，判定在他的網路覆蓋範圍不佳的情況下，同時響鈴規則會導致來電轉至 Joe 的手機語音信箱。

  - Mike 是 Contoso 的新進職員，而他所加入的新團隊會將所有成員設為小組通話。Microsoft Lync 功能啟用後，系統管理員可將他的小組通話群組設定設為包含所有的新團隊成員，再者，系統管理員亦可為團隊中的各個成員，將 Mike 新增為小組通話群組成員。

  - Contoso 人資部門的客服會在來電者的首通來電起提供個人服務。由於該部門的所有成員彼此座位非常接近，在小組通話時，所有電話同時響鈴會對小組造成相當程度的打擾。為提供完美的服務，同時又不打擾到小組成員，Lync 系統管理員會利用群組來電接聽功能。系統管理員會將所有部門成員新增為接聽群組，並將接聽群組號碼提供給該部門。當 Samantha 不在座位時，Joe 發現她的電話在響，即可從他的座位接聽該通電話。

## 需求

執行 SEFAUtil 工具的電腦必須屬於信任的應用程式集區。該電腦上必須安裝 UCMA 3.0。該集區則必須以 SEFAUtil 應用程式識別碼建立新信任的應用程式，才可執行這項工具。

**針對 SEFAUtil 工具建立新信任的應用程式**

1.  執行 SEFAUTil 工具的電腦必須屬於信任的應用程式集區。如有需要，可透過 Lync Server 管理命令介面而利用下列 Cmdlet 將集區新增為新信任的應用程式集區：
    
        New-CsTrustedApplicationPool -id <Pool FQDN> -Registrar <Pool Registrar FQDN> -site Site:<Pool Site>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用於執行 SEFAUtil 工具的電腦均必須安裝 UCMA 3.0</td>
    </tr>
    </tbody>
    </table>


2.  在拓撲中必須針對 SEFAUtil 工具定義信任的應用程式。為了將 SEFAUtil 定義為新信任的應用程式，請使用 Lync Server 管理命令介面並執行下列 Cmdlet：
    
        New-CsTrustedApplication -ApplicationId sefautil -TrustedApplicationPoolFqdn <Pool FQDN>  -Port 7489
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如有需要，可使用其他連接埠。</td>
    </tr>
    </tbody>
    </table>


3.  拓撲變更需要加以啟用。若要啟用拓撲變更，可透過 Lync Server 管理命令介面執行下列 Cmdlet 而完成：
    
        Enable-CsToplogy

4.  如有需要，在用於執行 SEFAUtil 工具的伺服器上安裝 Lync Server 2013 Resource Kit 工具 (該伺服器必須屬於信任的應用程式集區)。

5.  確認 SEFAUtil 正確執行。為執行這項操作，請以系統管理員權限透過 Windows 命令提示字元執行這項工具，以顯示使用者在部署中的來電轉接設定。依預設，這項工具會位於：“…\\Program Files\\Microsoft Lync Server 2013\\Reskit”。為顯示使用者的來電轉接設定，請使用下列命令：
    
        SEFAUtil.exe <user SIP address> /server:<Lync Server/Pool FQDN>
    
    畫面應會顯示使用者的來電轉接設定。

## 群組來電接聽

群組來電接聽功能需要在 Lync Server 中額外進行設定，該功能才會完整啟用。將接聽群組指派給使用者之前，請參閱群組來電接聽的產品文件，瞭解這個功能的規劃與部署步驟。

## 範例

## 顯示目前通話處理設定

下列命令會顯示使用者的通話處理。`SEFAUtil.exe /server:lyncserver.contoso.com katarina@contoso.com`

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此範例會使用 <strong>/server</strong> 參數指定所要連線的 Lync Server。</td>
</tr>
</tbody>
</table>


**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:20
    Call Forward No Answer to: voicemail

## 設定來電轉接/沒有接聽的目的號碼

此範例會設定來電轉接/沒有接聽的目的號碼以及響鈴延遲。在此，並未提供 /server 參數；SEFAUtil 會嘗試自動探索 Lync Server。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /enablefwdnoanswer /callanswerwaittime:30 /setfwddestination:+1425555 0126@contoso.com;user=phone

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: sip:+14255550126@contoso.com;user=phone

## 立即啟用來電轉接

此範例會立即啟用來電轉接至其他使用者的功能。

    SEFAUtil.exe sip:katarina@contoso.com /enablefwdimmediate /setfwddestination:anders@contoso.com

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    Forward immediate to: sip:anders@contoso.com

## 立即停用來電轉接

此範例會立即停用來電轉接的功能。

    SEFAUtil.exe /server:lyncserver.contoso.com katarina@contoso.com  /disablefwdimmediate

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail

## 新增使用者為代理人並設定代理人同時響鈴

此範例會將使用者新增為代理人並設定代理人同時響鈴。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /adddelegate:joe@contoso.com /simulringdelegates

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simultaneously Ringing Delegates: sip:joe@contoso.com

## 變更代理人的同時響鈴規則

此範例會將在上個範例中所設定的同時響鈴規則變更為延遲響鈴規則。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /delayringdelegates:10

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    Delay Ringing Delegates (delay:10 seconds): sip:joe@contoso.com

## 移除代理人

此範例會移除代理人。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>移除最後一個代理人後，代理人響鈴功能也會自動停用。</td>
</tr>
</tbody>
</table>


    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /removedelegate:joe@contoso.com

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail

## 新增代理人並設定來電轉接至代理人的規則

此範例會新增代理人並設定來電轉接至代理人的規格。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /adddelegate:anders@contoso.com /fwdtodelegates

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Forwarding calls to Delegates: sip:anders@contoso.com

## 啟用同時響鈴並設定目的號碼

此範例會啟用同時響鈴並設定同時響鈴的目的號碼。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /setsimulringdestination:+14255550126 /enablesimulring

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於啟用同時響鈴的使用者，若要變更同時響鈴的目的號碼，請以 /enablesimulring 參數保留命令，否則目的號碼將無法變更。</td>
</tr>
</tbody>
</table>


**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: True
    Simul_Ringing to: sip:+14255550126@contoso.com;user=phone

## 停用同時響鈴

此範例會停用同時響鈴。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /disablesimulring

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail

## 新增小組通話的小組成員並設定同時響鈴至小組通話成員群組

此範例會將小組成員新增至使用者的小組通話群組並啟用同時響鈴功能至小組通話群組。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /addteammember:anders@contoso.com /simulringteam

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>將成員新增至使用者的小組通話群組會將使用者的同時響鈴設定自動切換至小組通話群組的響鈴。</td>
</tr>
</tbody>
</table>


**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Team ringing enabled. Team: sip:anders@contoso.com

## 移除小組通話群組中的成員

此範例會從使用者的小組通話群組中移除小組成員。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /removeteammember:anders@contoso.com

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是所要移除的成員為小組通話群組的唯一成員，則小組通話群組的同時響鈴功能將會自動停用。</td>
</tr>
</tbody>
</table>


**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail

## 設定小組通話群組的延遲響鈴功能

此範例會變更延遲響鈴至小組通話群組的時間設定。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /delayringteam:5

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Delay Ringing Team (delay:5 seconds). Team: sip:anders@contoso.com

## 啟用小組通話

此範例會啟用特定使用者的小組通話功能。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /simulringteam

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是該名使用者的小組通話群組沒有成員，小組通話功能將無法啟用。</td>
</tr>
</tbody>
</table>


**輸出**

## 停用小組通話

此範例會停用特定使用者的小組通話功能。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /disableteamcall

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail

## 啟用群組來電接聽並將接聽群組指派給使用者

此範例會將接聽群組指派給使用者並啟用群組來電接聽。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /enablegrouppickup:199

**輸出**

    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Group Pickup Orbit: sip:199;phone-context=user-default@ contoso.com;user=phone

## 停用群組來電接聽

此範例會停用特定使用者的群組來電接聽功能。

    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /disablegrouppickup

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用使用者的群組來電接聽功能後，系統不會保留指派給該使用者的群組號碼。若是稍後要重新啟用該使用者的群組來電接聽功能，您必須以 /enablegrouppickup 參數重新指派群組號碼。</td>
</tr>
</tbody>
</table>


    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True

## SYSPrep.ps1

## 說明

SYSPrep.ps1 乃是 Windows PowerShell 指令碼，會將下列 Lync Server 2013 先決條件安裝於您的 Windows Server 2008 作業系統機器。

  - Microsoft .Net Framework 4.5

  - Microsoft SQL Server Express

  - Windows Powershell 版本 3.0

  - Visual C++ 2010 可轉散發元件

  - Internet Information Server 更新

  - Windows Identity Foundation

  - Lync Server 2013 核心檔案

雖然指令碼的名稱類似 Microsoft Windows 作業系統的系統準備工具，但兩者並不相同。這個指令碼僅會安裝 Lync Server 2013 的必要先決條件。先決條件安裝完成後，Windows SYSPrep 工具即可用於建立伺服器影像。

## 需求

執行 SYSPrep.ps1 指令碼前，您必須將先決條件檔案複製至 Windows Server 2008 作業系統 機器的本機資料夾 (例如 **D:\\Setup)**。這個資料夾必須另外包含 Lync Server 2013 檔案的複本，特別是 **Setup.exe。** 先決條件檔案可從下列位置進行下載：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>先決條件</th>
<th>位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft .Net Framework 4.5</p></td>
<td><p>http://go.microsoft.com/?linkid=9816306</p></td>
</tr>
<tr class="even">
<td><p>Microsoft SQL Server Express 2008 R2</p></td>
<td><p>http://www.microsoft.com/en-us/download/details.aspx?id=23650</p></td>
</tr>
<tr class="odd">
<td><p>Windows Powershell 版本 3.0</p></td>
<td><p>http://www.microsoft.com/en-us/download/details.aspx?id=34595</p></td>
</tr>
<tr class="even">
<td><p>Visual C++ 2010 可轉散發元件</p></td>
<td><p>http://www.microsoft.com/en-us/download/details.aspx?id=5555</p></td>
</tr>
<tr class="odd">
<td><p>Internet Information Server 更新</p></td>
<td><p>http://www.microsoft.com/en-us/download/details.aspx?id=34869</p></td>
</tr>
<tr class="even">
<td><p>Windows Identity Foundation</p></td>
<td><p>http://www.microsoft.com/en-us/download/details.aspx?id=17331</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013 Setup.exe</p></td>
<td><p>從 Lync Server 2013 媒體進行複製</p></td>
</tr>
</tbody>
</table>


## 參數

**–SetupFolder** 參數將作為先決條件檔案之目錄位置的引數。

## 範例

若要執行 SYSPrep.ps1 指令碼並安裝 Lync Server 2013 先決條件，請透過提升權限的命令提示字元執行下列命令：

    ./SysPrep.PS1 -SetupFolder D:\Setup

## Unassigned Number Announcements Migration

Unassigned Number Announcements Migration 工具可讓 Lync 系統管理員將宣告應用程式所處理之未指派的號碼設定從來源 Lync Server 或集區移至目的地 Lync Server 或集區。

## 說明

Unassigned Number Announcements Migration 工具為 Windows PowerShell 指令碼，可將宣告應用程式所處理之未指派的號碼設定從來源伺服器或集區移至其他伺服器或集區。

執行後，Unassigned Number Announcements Migration 指令碼將執行下列操作：

1.  將位於來源伺服器或集區的宣告應用程式之未指派的號碼宣告所使用的所有音訊檔案移至目的地伺服器或集區的檔案存放區。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>音訊檔案在複製至目的地集區後，即會從來源集區中移除。</td>
    </tr>
    </tbody>
    </table>


2.  將位於來源伺服器或集區的宣告應用程式所設定之所有未指派的號碼宣告移至目的地伺服器或集區。

3.  將位於來源伺服器或集區的宣告應用程式所處理之所有未指派的號碼範圍重新指派至目的地伺服器或集區。

成功執行指令碼後，由位於來源伺服器或集區的宣告應用程式所處理之所有未指派的號碼範圍現在將由目的地伺服器或集區以相同設定加以處理。

## 輸出

**Move-CsAnnouncementConfiguration** 指命碼會在其執行所在的 Lync 管理命令介面視窗中表示移轉作業的成功與否。

若是執行作業因錯誤而中斷，成功移至目的地之未指派的號碼範圍將以運作形式保留於目的地，而所要移轉之其他未指派的號碼範圍將以運作形式保留於來源中。為了完整移轉其他設定，請在解決錯誤後重新執行指令碼。

## 用途

Unassigned Number Announcements Migration 指令碼可用於下列三個使用案例：

  - **移轉組態設定至新版的 Lync Server：** Contoso 目前正在移轉至 Lync Server 2013，在移轉程序期間，Lync Server 系統管理員要將宣告應用程式所處理之未指派的號碼設定從 Lync Server 2010 部署移至新的 Lync Server 2013 部署。為了移動組態設定，Lync Server 系統管理員會使用 Unassigned Number Announcements Migration 工具。

  - **從 Lync Server 2013 回復至 Lync Server 2010 的部署：** 由於非預期的因素，Contoso 需要將移轉作業回復至新的 Lync Server 2013 部署。為了盡可能減少服務中斷情形，Lync Server 系統管理員會使用 Unassigned Number Announcements Migration 工具從 Lync Server 2013 部署的設定回復至 Lync Server 2010 部署。

  - **在 Lync 部署之間移動資料：** Contoso 目前正以較新的伺服器取代單一集區中的所有伺服器。Contoso 的策略在於部署新版的 Lync Server 2013 集區，將所有資料從舊集區移至新集區，接著取代舊集區運作。新集區部署完成後，會使用 Unassigned Number Announcements Migration 工具將設定從舊集區移至新集區。

## 需求

以下為成功執行這項工具的主要需求：

1.  執行指令碼的電腦必須安裝 Lync Server 2013 管理命令介面。

2.  宣告應用程式必須成功部署於來源與目的地 Lync Servers 或集區。

## Move-CsAnnouncementConfiguration 指令碼

Move-CsAnnouncementConfiguration 指令碼需要下表中所述的兩個參數。

![Move-CsAnnouncementConfiguration 參數。](images/JJ945604.7ab66ad3-d0db-4d77-8b93-ebccf0cb0663(OCS.15).jpg "Move-CsAnnouncementConfiguration 參數。")

## 範例

## 將未指派的號碼宣告設定從 Lync Server 2010 集區移至 Lync Server 2013 集區

此範例會將未指派的號碼宣告從來源集區 (Lync Server 2010) 移至目的地集區 (Lync Server 2013)。

    Move-CsAnnouncementConfiguration.ps1 -Source LS2010Pool.contoso.com -Destination LS2013Pool.contoso.com

## 將未指派的號碼宣告設定從 Lync Server 2013 集區移至 Lync Server 2010 集區

此範例會將未指派的號碼宣告從來源集區 (Lync Server 2013) 移至目的地集區 (Lync Server 2010)。

    Move-CsAnnouncementConfiguration.ps1 -Source LS2013Pool.contoso.com -Destination LS2010Pool.contoso.com

## Web Conf Data

針對召集人的 Web 會議，Web Conf Data 工具可讓 Lync Server 2013 通訊軟體系統管理員更能控管相關聯的資料。使用案例包括根據時間戳記準則而刪除特定使用者的會議資料。

## 說明

這項工具可讓系統管理員執行下列操作：

1.  尋找與單一使用者相關聯的所有 Web 會議資料。

2.  刪除與單一使用者相關聯的所有 Web 會議資料。

3.  刪除與單一使用者相關聯且時間早於特定日期的所有 Web 會議資料。

4.  在集區之間移動單一使用者時一併移動與該使用者相關聯的所有 Web 會議資料。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945612.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在集區之間移動單一使用者時，Lync Server 2010 的 Resource Kit 工具 支援移動與該使用者相關聯的所有 Web 會議資料。該功能在這項工具中現已取代為 <strong>MoveConferenceData</strong> 參數。如需這項參數的詳細資訊，請見 <a href="https://technet.microsoft.com/zh-tw/library/gg398528(v=ocs.15)">Move-CsUser</a> Cmdlet。</td>
</tr>
</tbody>
</table>


這項工具僅會刪除非使用中會議的會議資料。作用中會議 (或工作階段中的會議) 無法刪除。

執行這項工具的電腦必須與目標使用者位於相同集區。其會議內容資料由這項工具加以管理的使用者必須位於相同的使用者集區。

## 輸出

這項工具會輸出各個作業的結果：

  - 若是執行查詢，這項工具會輸出以該名使用者作為召集人之所有非使用中會議資料的資料夾清單。

  - 若是執行刪除，這項工具會輸出將會遭到刪除之所有會議資料的資料夾清單。

## 需求

執行這項工具的集區必須與召集人目前所在的集區相同。

必須以具有內容檔案存放區存取權限的系統管理員權限執行這項工具。

## 範例

下表說明參數資訊，部分參數用於範例中。

![Web Conf Data 工具參數。](images/JJ945604.a733c1c6-5dfc-4874-a74f-bfdee81c1401(OCS.15).jpg "Web Conf Data 工具參數。")

    WebConfDataTool.exe /User:user0@contoso.com /Action:query ""/ExpirationDate:08/09/2010 12:00:00""

上述範例顯示查詢命令的運作方式。該類命令的輸出會列出將受到這項工具影響的所有會議內容資料夾。

    WebConfDataTool.exe /User:user0@contoso.com /Action:delete

上述為刪除命令的範例。刪除命令會將所有非使用中的會議資料夾從該使用者中移除。

## 總結

若是系統管理員對於會議資料需要擁有更加精準的控制能力，這項工具將會是相當實用的資源。


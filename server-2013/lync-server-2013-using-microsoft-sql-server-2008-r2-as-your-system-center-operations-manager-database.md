---
title: 使用 Microsoft SQL Server 2008 R2 當成 System Center Operations Manager 資料庫
TOCTitle: 使用 Microsoft SQL Server 2008 R2 當成 System Center Operations Manager 資料庫
ms:assetid: 0efe76da-8854-499e-bdc7-3623244a8e85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687969(v=OCS.15)
ms:contentKeyID: 49889940
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Microsoft SQL Server 2008 R2 當成 System Center Operations Manager 資料庫

 

_**上次修改主題的時間：** 2013-07-29_

若要使用 SQL Server 2008 R2 作為後端資料庫，請完成本主題中詳述的步驟。

## 設定 SQL Server 2008 R2 及 SQL Server Reporting Services

在開始安裝 System Center Operations Manager 之前，您必須先對 SQL Server 2008 R2 和 SQL Server Reporting Services 設定進行兩項變更。(唯有當您使用 SQL Server 2008 R2 作為 Operations Manager 資料庫時，才需要這些變更。) 首先，請在將要裝載 Operations Manager 資料庫的電腦上執行下列作業：

1.  按一下 \[開始\]，然後按一下 \[執行\]。

2.  在 \[執行\] 對話方塊中，輸入 **C:\\Program Files\\Microsoft SQL Server\\ MSRS10\_50.ARCHINST\\Reporting Services\\ReportServer**，然後按 ENTER 。

3.  在 **ReportServer** 資料夾中，以 \[記事本\] 或任何其他文字編輯器來開啟 **rsreportserver.config** 檔案。

4.  您會在靠近檔案開頭的地方，看到一連串的 "Add Key" 節點。請尋找以 **\<Add Key="SecureConnectionLevel"** 開頭的項目，並將該值設為 **0**：
    
        <Add Key="SecureConnectionLevel" Value="0"/>

5.  儲存 **rsreportserver.config** 檔案，然後關閉文字編輯器。

更新報告伺服器組態檔之後，您必須指派正確的憑證給 SQL Server Reporting Services。若要執行這項作業，請完成下列程序：

1.  依序按一下 \[開始\]、\[所有程式\]、\[Microsoft SQL Server 2008 R2\]、\[設定工具\] 及 \[Reporting Services 組態管理員\]。

2.  在 \[Reporting Services 組態連接\] 對話方塊中，確定您的伺服器名稱出現在 \[伺服器名稱\] 方塊中。從 \[報告伺服器執行個體\] 下拉式清單中，選取將要裝載 Operations Manager 資料庫 (例如，**ARCHINST**) 的 SQL Server 執行個體，然後按一下 \[連線\]。

3.  在 Reporting Services 組態管理員中，按一下 \[Web 服務 URL\]。

4.  在「Web 服務 URL」頁面上，從 \[SSL 憑證\] 下拉式清單中選取要用於 Reporting Services 的憑證，然後按一下 \[套用\]。幾秒鐘之後，您就會看到 \[報告伺服器 Web 服務 URL\] 底下列出一對 URL。

5.  在兩個 URL 上都按一下，以確認您可以存取 SQL Server Reporting Services。

6.  關閉 Reporting Services 組態管理員。

## 建立 System Center Operations Manager 資料庫以用於 SQL Server 2008 R2

如果您想要設定 System Center Operations Manager 來使用 SQL Server 2008 R2 資料庫，則需要在執行 SQL Server 2008 R2 的電腦上，「手動」建立 Operations Manager 資料庫 (再強調一次，如果您是使用 SQL Server 2005 或 SQL Server 2008 作為後端資料庫，就不需要這些步驟)。

若要手動建立 Operations Manager 資料庫，請執行下列動作：

1.  在 System Center Operations Manager 2007 R2 安裝媒體上的 SupportTools\\AMD64 資料夾中，按兩下 **DBCreateWizard.exe**。

2.  在 \[資料庫設定精靈\] 的「歡迎使用資料庫設定精靈」頁面上，按 \[下一步\]。

3.  在「資料庫資訊」頁面上，將所有設定保留原狀，然後按 \[下一步\]。

4.  在「管理群組設定」頁面上的 \[管理群組名稱\] 方塊中，輸入管理群組的名稱 (例如，**Lync Server Monitoring**)，然後按 \[下一步\]。

5.  在「Operations Manager 錯誤報告」頁面上，按 \[下一步\]。

6.  在「摘要」頁面上，按一下 \[完成\]。

## 建立 System Center Operations Manager 資料倉儲以用於 SQL Server 2008 R2

Microsoft Lync Server 2013 隨附三個新的 System Center Operations Manager 報告：

  - **端對端案例可用性報告**   此報告詳述主要 Lync Server 服務的可用性/上線時間，例如註冊或目前狀態。

  - **容量報告**   此報告使用效能計數器資訊，會顯示系統元件的趨勢，例如記憶體可用性及處理器使用量。

  - **元件報告**   此報告會列出依 Lync Server 元件分組的首要警示產生器。

若要使用這些新報告，您必須安裝 System Center Operations Manager 資料倉儲。(資料倉儲可供長期儲存作業資料。) 若要使用資料倉儲來搭配 SQL Server 2008 R2，您必須在裝載 SQL Server 資料庫的電腦上執行下列步驟：

1.  在 System Center Operations Manager 安裝媒體上的 Setup\\SupportTools\\AMD64 資料夾中，按兩下 **DBCreateWizard.exe**。

2.  在 \[資料庫設定精靈\] 的「歡迎使用資料庫設定精靈」頁面上，按 \[下一步\]。

3.  在「資料庫資訊」頁面上，從 \[資料庫類型\] 下拉式清單中選取 \[Operations Manager 資料倉儲資料庫\]，然後按 \[下一步\]。

4.  在「摘要」頁面上，按一下 \[完成\]。

## 安裝 System Center Operations Manager 主控台

Operations Manager 主控台是用來管理 System Center Operations Manager 的主要工具。在安裝 Operations Manager 主控台之前，請確定您已經隨 SQL Server Reporting Service 安裝支援的 SQL Server 版本。此外，也建議您執行 SQL Server 的 Reporting Services 組態管理員，以確認 Reporting Service 已正確安裝及設定。

若要安裝 System Center Operations Manager 主控台，請執行下列動作：

1.  在 System Center Operations Manager 安裝媒體上，按兩下 **SetupOM.exe**。

2.  在 System Center Operations Manager 2007 R2 安裝程式中，按一下 \[檢查必要條件\]。

3.  在 System Center Operations Manager 必要條件檢視器中，選取所要安裝的 System Center 元件：(\[伺服器\]、\[主控台\] 及 \[PowerShell\]) ，然後按一下 \[檢查\]。確認沒有報告任何封鎖問題，然後按一下 \[關閉\]。如果有報告封鎖問題，請更正問題，然後按一下 \[檢查\]，重新執行必要條件測試。

4.  在 System Center Operations Manager 安裝程式中，按一下 \[安裝 Operations Manager\]。

5.  在 \[System Center Operations Manager 安裝精靈\] 中的「歡迎使用 System Center Operations Manager 安裝精靈」頁面上，按 \[下一步\]。

6.  在「使用者授權合約」頁面上，選取 \[我接受授權合約中的條款\]，然後按 \[下一步\]。

7.  在「產品註冊」頁面上的 \[使用者名稱\] 方塊中，輸入您的名稱，並且在 \[組織\] 方塊中輸入組織的名稱。在 \[輸入您的 25 位數產品識別碼\] 方塊中，輸入 System Center Operations Manager 產品金鑰，然後按 \[下一步\]。

8.  在「自訂安裝程式」頁面上，選取所要安裝的 System Center 選項，然後按 \[下一步\]。您應選取 \[管理伺服器\]、\[資料庫使用者介面\] 及 \[Web 主控台\] 以進行安裝。不應選取 \[資料庫\]，也不應安裝。

9.  在「SC 資料庫伺服器執行個體」頁面上，確認安裝 Operations Manager 資料庫的電腦名稱出現在 \[System Center 資料庫伺服器\] 方塊中。按 \[下一步\]。

10. 在「管理伺服器動作帳戶」頁面上，選取 \[網域或本機電腦帳戶\]，然後在 \[使用者帳戶\]、\[密碼\] 及 \[網域或本機電腦\] 方塊中輸入適當的值。按 \[下一步\]。

11. 在「SDK 和設定服務帳戶」頁面上，選取 \[網域或本機電腦帳戶\]，然後在 \[使用者帳戶\]、\[密碼\] 及 \[網域或本機電腦\] 方塊中輸入適當的值。按 \[下一步\]。

12. 在「Operations Manager 錯誤報告」頁面上，按 \[下一步\]。

13. 在「客戶經驗改進計畫」頁面上，按 \[下一步\]。

14. 在「已完成安裝程式的準備工作」頁面上，按一下 \[安裝\]。

15. 在「正在完成 System Center Operations Manager 安裝程式」頁面上，清除 \[備份加密金鑰\] 及 \[啟動主控台\] 核取方塊，然後按一下 \[完成\]。

16. 在 System Center Operations Manager 安裝程式中，按一下 \[結束\]。

## 安裝 System Center Reporting Services

安裝及設定 System Center Operations Manager 主控台之後，您必須安裝 System Center Reporting Services。如果您是使用 SQL Server 2008 R2 作為 Operations Manager 後端資料庫，則表示您必須先暫時變更與 SQL Server Reporting Services 相關聯的安全性群組。如果您是使用 SQL Server 2008 R2，必須執行下列動作：

1.  按一下 \[開始\]，指向 \[系統管理工具\]，然後按一下 \[伺服器管理員\]。

2.  在伺服器管理員中，依序展開 \[設定\] 及 \[本機使用者和群組\]，然後按一下 \[群組\]。

3.  尋找下列群組，其中 atl-sc-001 代表電腦的名稱，而 ARCHINST 代表 System Center 資料庫的 SQL Server 執行個體：**SQLServerReportServerUser$atl-sc-001$MSRS10\_50.ARCHINST**。

4.  以滑鼠右鍵按一下該群組，然後按一下 \[重新命名\]。將群組名稱中的 **\_50** 刪除，以重新命名群組。例如，**SQLServerReportServerUser$atl-sc-001$MSRS10.ARCHINST**。

5.  關閉伺服器管理員。

這時候，您已經準備好可以安裝 System Center Reporting Services。若要執行這項作業，請完成下列程序：

1.  在 System Center Operations Manager 2007 R2 安裝媒體上，按兩下 **SetupOM.exe**。

2.  在 System Center Operations Manager 2007 R2 安裝程式中，按一下 \[安裝 Operations Manager 報告\]。

3.  在 \[System Center Operations Manager 2007 R2 報告安裝精靈\] 中的「歡迎使用 Operations Manager 報告安裝程式」頁面上，按 \[下一步\]。

4.  在「使用者授權合約」頁面上，選取 \[我接受授權合約中的條款\]，然後按 \[下一步\]。

5.  在「產品註冊」頁面上，確定您的名稱和組織的名稱分別出現在 \[使用者名稱\] 和 \[組織\] 方塊中，然後按 \[下一步\]。

6.  在「自訂安裝程式」頁面上，按一下 \[報告伺服器\]，並選取 \[這個元件以及所有相依的元件會安裝到本機硬碟\]。按一下 \[資料倉儲\]，並選取 \[這個元件將無法使用\]，然後按 \[下一步\]。

7.  在「連線至 Root Management Server」頁面上的 \[Root Management Server\] 方塊中，輸入 Operations Manager Root Management Server 的名稱，然後按 \[下一步\]。

8.  在「連線到 Operations Manager 資料倉儲」頁面上的 \[SQL Server 執行個體\] 方塊中，輸入資料倉儲所在的 SQL Server 執行個體。(如果資料倉儲位在預設執行個體中，則直接輸入伺服器名稱即可；例如：atl-sql-001。) 確認資料庫名稱 **OperationsManagerDW** 出現在 \[名稱\] 方塊中，而且連接埠 **1433** 出現在 \[SQL Server 連接埠\] 方塊中。按 \[下一步\]。

9.  在「SQL Server 報告執行個體」頁面上，從 \[輸入 SQL Server Reporting Services 伺服器\] 下拉式清單中選取 SQL Server 報告伺服器，然後 \[下一步\]。

10. 在「資料倉儲寫入帳戶」頁面上的 \[使用者帳戶\] 和 \[密碼\] 方塊中，輸入一開始要為其指派資料倉儲寫入權限的使用者名稱和密碼。從 \[網域\] 下拉式清單中選取使用者的網域，然後按 \[下一步\]。

11. 在「資料讀取器帳戶」頁面上的 \[使用者帳戶\] 和 \[密碼\] 方塊中，輸入當 SQL Reporting Services 查詢資料倉儲時，所要使用之使用者帳戶的名稱和密碼。從 \[網域\] 下拉式清單中選取帳戶網域，然後按 \[下一步\]。

12. 在「操作資料報告」頁面上，按 \[下一步\]。

13. 在「Microsoft Update」頁面上，按 \[下一步\]。

14. 在「已完成安裝程式的準備工作」頁面上，按一下 \[安裝\]。

15. 在「正在完成 Operations Manager 報告元件安裝精靈」頁面上，按一下 \[完成\]。

16. 在 System Center Operations Manager 2007 R2 安裝程式中，按一下 \[結束\]。

安裝 System Center Reporting 之後，請使用下列程序來重設與 SQL Server Reporting 相關聯之安全性群組的名稱。再強調一次，唯有當您使用 SQL Server 時，才需要此程序：

1.  按一下 \[開始\]，指向 \[系統管理工具\]，然後按一下 \[伺服器管理員\]。

2.  在伺服器管理員中，依序展開 \[設定\] 及 \[本機使用者和群組\]，然後按一下 \[群組\]。

3.  尋找下列群組，其中 atl-sc-001 代表電腦的名稱，而 ARCHINST 代表封存及監控資料庫的 SQL Server 執行個體：**SQLServerReportServerUser$atl-sc-001$MSRS10.ARCHINST**。

4.  以滑鼠右鍵按一下該群組，然後按一下 \[重新命名\]。在群組名稱結尾 (就在 SQL Server 執行個體名稱前面) 加上 **\_50**，以重新命名群組。例如：**SQLServerReportServerUser$atl-sc-001$MSRS10\_50.ARCHINST**。

5.  關閉伺服器管理員。

如果 System Center 操作主控台開啟，則您需要關閉應用程式，然後再重新啟動；如果不這麼做，\[報告\] 索引標籤不會出現在操作主控台使用者介面中。請注意，第一次重新啟動操作主控台之後，可能需要幾分鐘的時間，監視報告才會全部出現在 \[報告\] 索引標籤中。


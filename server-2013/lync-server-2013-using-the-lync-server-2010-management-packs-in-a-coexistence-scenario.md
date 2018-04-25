---
title: 在共存案例中使用 Lync Server 2010 管理套件
TOCTitle: 在共存案例中使用 Lync Server 2010 管理套件
ms:assetid: 8b792503-bd88-47fe-9d97-b071e8d429a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205078(v=OCS.15)
ms:contentKeyID: 49291603
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在共存案例中使用 Lync Server 2010 管理套件

 

_**上次修改主題的時間：** 2012-10-22_

許多客戶會在他們的企業內部採用首度發行計劃，讓使用者逐漸從 Microsoft Lync Server 2010 移轉至 Lync Server 2013。這些公司的系統管理員將會注意監控這兩個版本的 Lync Server，以協助確定所有使用者都會獲得前所未有的最佳通訊體驗。針對這個案例，Lync Server 2013 管理組件支援與 Lync Server 2010 管理組件的並存移轉路徑。

在 Lync Server 2010 中，可以透過利用中央管理存放區儲存的拓撲文件來探索 Lync Server 電腦。在此設定中，單一電腦會報告所有現有的其他 Lync Server 電腦。

Lync Server 2013 的管理組件現在會使用電腦層級探索，而不是 Lync Server 2010 中所使用的集中探索機制。這表示每個 System Center 代理程式基本上會探索它自己，並向 System Center Operations Manager 報告它的存在。使用電腦層級探索可簡化您的 System Center 基礎結構管理，也能讓各種版本的 Lync Server 管理組件 (例如，Lync Server 2010 的管理組件和 Lync Server 2013 的管理組件) 更容易共存。

若要支援此移轉，您首先需要升級現有的 Lync Server 2010 監控，以避免在涵蓋範圍中產生落差。若要執行此動作，請先選取現有的 Lync Server 2010 電腦，以服務 Lync Server 2010 的集中探索指令碼，然後再將您的中央管理存放區升級至 Lync Server 2013。此為四步驟的程序：

1.  將 Lync Server 2010 管理組件升級至累計更新 7。

2.  指示 Lync Server 2010 電腦執行集中探索指令碼。

3.  在 Microsoft Lync Server 2010 管理組件中，覆寫集中探索候選項目。

4.  確認已探索到新的集中探索候選項目。

## 指示 Lync Server 2010 電腦執行集中探索指令碼

若要指定非中央管理存放區電腦 (例如，Lync Server 前端) 伺服器來處理集中探索，您需要在非中央管理存放區伺服器上建立下列登錄機碼：

HKLM\\Software\\Microsoft\\Real-Time Communications\\Health\\CentralDiscoveryCandidate

您可以藉由完成下列程序來建立此登錄機碼：

1.  按一下 \[開始\]，然後再按一下 \[執行\]。

2.  在 \[執行\] 對話方塊中，輸入 \[regedit\]，然後按 ENTER。

3.  在登錄編輯程式中，依序展開 \[HKEY\_LOCAL\_MACHINE\]、\[SOFTWARE\]、\[Microsoft\] 及 \[即時通訊\]。

4.  以滑鼠右鍵按一下 \[健康情況\]、按一下 \[新增\]，然後按一下 \[機碼\]。如果 \[健康情況\] 機碼不存在，則使用滑鼠右鍵按一下 \[即時通訊\]、指向 \[新增\]，然後按一下 \[機碼\]。建立新機碼時，輸入 Health，然後按 ENTER。
    
    建立新機碼之後，輸入 **CentralDiscoveryCandidate**，然後按 ENTER，將該機碼重新命名。

電腦可能需要數小時的時間，才能取得此項變更。若要讓變更立即生效，請先停止然後重新啟動 \[健康情況代理程式\] 服務，若要重新啟動 \[健康情況代理程式\] 服務，請在 Lync Server 2010 電腦上完成下列程序：

1.  依序按一下 \[開始\]、\[所有程式\] 及 \[附屬應用程式\]，再以滑鼠右鍵按一下 \[命令提示字元\]，然後按一下 \[以系統管理員身分執行\]。

2.  在主控台視窗中，輸入下列命令，然後按 ENTER：
    
        Net stop HealthService

3.  您將會看見一則訊息，說明「正在停止 System Center 管理服務」，後面接著第二則訊息，告知您服務已停止。在服務停止之後，您可以輸入下列命令並按 ENTER，來重新啟動服務：
    
        Net start HealthService

## 覆寫 Lync Server 2010 管理組件中的集中探索候選項目

指示 Lync Server 2010 電腦在 Lync Server 2010 電腦上進行報告之後，您還需要通知 Lync Server 2010 管理組件關於此項變更的資訊。若要執行此動作，您需要在管理組件中建立覆寫。您可以藉由完成下列程序來完成此動作：

1.  在 Operations Manager 主控台中，按一下 \[撰寫\]。

2.  在 \[撰寫\] 索引標籤上，展開 \[管理組件物件\]、按一下 \[物件探索\]，然後按一下 \[範圍\]。

3.  在 \[為管理群組件物件決定領域\] 對話方塊中，選取含 \[目標 LS 探索候選項目\] 的項目，然後按一下 \[確定\]。請注意，只有在您已安裝 Lync Server 2010 管理組件時，\[LS 探索候選項目\] 才會出現。

4.  在 Operations Manager 主控台中，以滑鼠右鍵按一下 \[LS 探索候選項目\]，依序指向 \[覆寫\] 和 \[覆寫物件探索\]，然後按一下 \[針對類別的所有物件：LS 探索候選項目\]。

5.  在 \[覆寫內容\] 對話方塊中，選取參數 \[集中探索 WatcherNode Fqdn\] 旁的 \[覆寫\] 核取方塊。在 \[覆寫值\] 和 \[生效值\] 方塊中輸入 Lync Server 2010 電腦的完整網域名稱。選取 \[強制\] 核取方塊，然後按一下 \[確定\]。

當您建立覆寫之後，需要在 Root Management Server 上重新啟動健康情況服務。若要重新啟動健康情況服務，請在 Root Management Server 上完成下列程序：

1.  依序按一下 \[開始\]、\[所有程式\] 及 \[附屬應用程式\]，再以滑鼠右鍵按一下 \[命令提示字元\]，然後按一下 \[以系統管理員身分執行\]。

2.  在主控台視窗中，輸入下列命令，然後按 ENTER：
    
        Net stop HealthService

3.  您將會看見一則訊息，說明「正在停止 System Center 管理服務」，後面接著第二則訊息，告知您服務已停止。在服務停止之後，您接著可以輸入下列命令並按 ENTER，來重新啟動服務：
    
        Net start HealthService

## 確認已探索到新的集中探索候選項目

升級中央管理存放區前的最後一個步驟是確定 Lync Server 2010 管理組件已探索到新的集中探索候選項目。若要執行此動作，請開啟 Operations Manager 主控台，然後按一下 \[監控\]。在 \[監控\] 索引標籤上，依序展開 \[Microsoft Lync Server 2010 健康情況\] 和 \[拓撲探索\]，然後按一下 \[探索狀態檢視\]。確認顯示中的某一列含有一個 \[路徑\]，其中列出集中探索候選項目的完整網域名稱。您也應該確認電腦狀態已報告為 \[狀況良好\]。

